---
title: char 和 varchar (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 10/22/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- varchar
- varchar_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- fixed-length data types [SQL Server]
- character data type
- char data type
- varchar(max) data type
- variable-length data types [SQL Server]
- varchar data type
- utf8
ms.assetid: 282cd982-f4fb-4b22-b2df-9e8478f13f6a
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: c6bba11fe5be282ad804fc6dee03229312ec1d37
ms.sourcegitcommit: b58d514879f182fac74d9819918188f1688889f3
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/02/2018
ms.locfileid: "50970909"
---
# <a name="char-and-varchar-transact-sql"></a>char 和 varchar (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

> [!div class="nextstepaction"]
> [请帮助改进 SQL Server 文档！](https://80s3ignv.optimalworkshop.com/optimalsort/36yyw5kq-0)

字符数据类型 char（长度固定）或 varchar（长度可变）。 从 [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] 起，使用启用了 UTF-8 的排序规则时，这些数据类型会存储 [Unicode](../../relational-databases/collations/collation-and-unicode-support.md#Unicode_Defn) 字符数据的整个范围，并使用 [UTF-8](http://www.wikipedia.org/wiki/UTF-8) 字符编码。 若指定了非 UTF-8 排序规则，则这些数据类型仅会存储该排序规则的相应代码页支持的字符子集。
  
## <a name="arguments"></a>参数  
char [ ( n ) ] 固定长度字符串数据。 n 用于定义字符串长度（以字节为单位），并且它必须为 1 到 8,000 之间的值。 对于单字节编码字符集（如拉丁文），存储大小为 n 个字节，并且可存储的字符数也为 n。 对于多字节编码字符集，存储大小仍为 n 个字节，但可存储的字符数可能小于 n。 char 的 ISO 同义词是 character。 有关字符集的详细信息，请参阅[单字节和多字节字符集](/cpp/c-runtime-library/single-byte-and-multibyte-character-sets)。

varchar [ ( n | max ) ] 可变长度字符串数据。 n 用于定义字符串长度（以字节为单位），并且它可以为 1 到 8,000 之间的值。 max 指示最大存储大小是 2^31-1 个字节 (2 GB)。 对于单字节编码字符集（如拉丁文），存储大小为 n + 2 个字节，并且可存储的字符数也为 n。 对于多字节编码字符集，存储大小仍为 n + 2 个字节，但可存储的字符数可能小于 n。 varchar 的 ISO 同义词是 charvarying 或 charactervarying。 有关字符集的详细信息，请参阅[单字节和多字节字符集](/cpp/c-runtime-library/single-byte-and-multibyte-character-sets)。

## <a name="remarks"></a>Remarks  
如果没有在数据定义或变量声明语句中指定 n，则默认长度为 1。 如果在使用 CAST 和 CONVERT 函数时未指定 n，则默认长度为 30。
  
为使用 char 或 varchar 的对象分配的是默认的数据库排序规则，但可使用 COLLATE 子句分配特定的排序规则。 该排序规则控制用于存储字符数据的代码页。

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中的多字节编码包括：
-   使用代码页 936 及 950（中文）、932（日文）或 949（韩文）的某些东亚语言的双字节字符集 (DBCS)。
-   使用代码页 65001 的 UTF-8。 适用范围：[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]（从 [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] 开始）

若你拥有支持多种语言的站点：
- 从 [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] 开始，考虑使用已启用 UTF-8 的排序规则，以支持 Unicode 并最大程度地减少字符转换问题。 
- 若使用较低版本的 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]，请考虑使用 Unicode nchar 或 nvarchar 数据类型，以最大程度地减少字符转换问题。   

若使用 char 或 varchar，则建议：
- 如果列数据项的大小一致，则使用 char。  
- 如果列数据项的大小差异相当大，则使用 varchar。  
- 如果列数据项大小相差很大，而且字符串长度可能超过 8,000 字节，请使用 varchar(max)。  
  
当执行 CREATE TABLE 或 ALTER TABLE 时，如果 SET ANSI_PADDING 为 OFF，则定义为 NULL 的 char 列将作为 varchar 处理。
  
> [!WARNING]
> 每个非 null varchar(max) 或 nvarchar(max) 列都需要 24 个字节的附加固定分配，这将在执行排序操作期间根据 8,060 字节行限制进行计数。 这样一来，可能会为非 null varchar(max) 或 nvarchar(max)（可在表格中进行创建）列数创建隐式限制。  
在以下情况下不提供特殊错误：创建表格（最大行大小超过允许的最大 8,060 字节时出现的一般警告除外）时，或插入数据时。 这一较大的行大小可能会导致在执行某些正常操作（例如聚集索引键更新或完整列集排序）期间出现错误（例如错误 512），使得用户在执行操作前无法预料到此类错误。
  
##  <a name="_character"></a>转换字符数据  
如果将字符表达式转换为不同大小的字符数据类型，则对于新数据类型而言过长的值将被截断。 出于从字符表达式转换的目的将 uniqueidentifier 类型视为字符类型，因此在转换到字符类型时要遵循截断规则。 请参阅后面的“示例”一节。
  
如果将某个字符表达式转换为不同数据类型或大小的字符表达式（例如从 char(5) 转换为 varchar(5) 或从 char(20) 转换为 char(15)），则输入值的排序规则会被分配给经过转换的值。 如果将非字符表达式转换为字符数据类型，则当前数据库的默认排序规则会被分配给经过转换的值。 在任意一种情况下，都可以使用 [COLLATE](../../t-sql/statements/collations.md) 子句分配特定的排序规则。
  
> [!NOTE]  
> char 和 varchar 数据类型支持代码页转换，但是 text 数据类型不支持。 与 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的早期版本一样，将不报告代码页转换期间的数据丢失。  
  
要转换为近似 numeric 数据类型的字符表达式包含可选的指数符号 [一个大写或小写的字母 E 后跟可选的加号 (+) 或减号 (-)，然后再跟一个数字]。
  
要转换为精确 numeric 数据类型的字符表达式必须包含数字、小数点和可选的加号 (+) 或减号 (-)。 将忽略前导空格。 逗号分隔符（例如 123,456.00 中的千位分隔符）在字符串中禁用。
  
要转换为 money 或 smallmoney 数据类型的字符表达式还可以包含可选的小数点和美元符号 ($)。 可以使用逗号分隔符（如在 $123,456.00 中）。
  
## <a name="examples"></a>示例  
  
### <a name="a-showing-the-default-value-of-n-when-used-in-variable-declaration"></a>A. 在变量声明中显示 n 的默认值。  
以下示例显示在变量声明中使用 `char` 和 `varchar` 数据类型时，n 的默认值为 1。
  
```sql
DECLARE @myVariable AS varchar = 'abc';  
DECLARE @myNextVariable AS char = 'abc';  
--The following returns 1  
SELECT DATALENGTH(@myVariable), DATALENGTH(@myNextVariable);  
GO  
```  
  
### <a name="b-showing-the-default-value-of-n-when-varchar-is-used-with-cast-and-convert"></a>B. 在 CAST 和 CONVERT 中使用 varchar 时，显示 n 的默认值。  
以下示例显示在 `CAST` 和 `CONVERT` 函数中使用 `char` 或 `varchar` 数据类型时，n 的默认值为 30。
  
```sql
DECLARE @myVariable AS varchar(40);  
SET @myVariable = 'This string is longer than thirty characters';  
SELECT CAST(@myVariable AS varchar);  
SELECT DATALENGTH(CAST(@myVariable AS varchar)) AS 'VarcharDefaultLength';  
SELECT CONVERT(char, @myVariable);  
SELECT DATALENGTH(CONVERT(char, @myVariable)) AS 'VarcharDefaultLength';  
```  
  
### <a name="c-converting-data-for-display-purposes"></a>C. 转换数据以便于显示  
以下示例将两列转换为字符类型并应用一种样式，该样式将特定格式应用于所显示的数据。 money 类型转换为字符数据并应用样式 1，这会对小数点左侧的每三个数字和对小数点右侧的每两个数字加一个逗号来显示值。 datetime 类型转换为字符数据并应用样式 3，这会以格式 dd/mm/yy 来显示数据。 在 WHERE 子句中，money 类型强制转换为字符类型，以执行字符串比较操作。
  
```sql
USE AdventureWorks2012;  
GO  
SELECT  BusinessEntityID,   
   SalesYTD,   
   CONVERT (varchar(12),SalesYTD,1) AS MoneyDisplayStyle1,   
   GETDATE() AS CurrentDate,   
   CONVERT(varchar(12), GETDATE(), 3) AS DateDisplayStyle3  
FROM Sales.SalesPerson  
WHERE CAST(SalesYTD AS varchar(20) ) LIKE '1%';  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```
BusinessEntityID SalesYTD              DisplayFormat CurrentDate             DisplayDateFormat  
---------------- --------------------- ------------- ----------------------- -----------------  
278              1453719.4653          1,453,719.47  2011-05-07 14:29:01.193 07/05/11  
280              1352577.1325          1,352,577.13  2011-05-07 14:29:01.193 07/05/11  
283              1573012.9383          1,573,012.94  2011-05-07 14:29:01.193 07/05/11  
284              1576562.1966          1,576,562.20  2011-05-07 14:29:01.193 07/05/11  
285              172524.4512           172,524.45    2011-05-07 14:29:01.193 07/05/11  
286              1421810.9242          1,421,810.92  2011-05-07 14:29:01.193 07/05/11  
288              1827066.7118          1,827,066.71  2011-05-07 14:29:01.193 07/05/11  
```  
  
### <a name="d-converting-uniqueidentifer-data"></a>D. 转换 Uniqueidentifer 数据  
以下示例将 `uniqueidentifier` 值转换为 `char` 数据类型。
  
```sql
DECLARE @myid uniqueidentifier = NEWID();  
SELECT CONVERT(char(255), @myid) AS 'char';  
```  
  
以下示例演示在值过长而无法转换数据类型时如何截断数据。 因为 uniqueidentifier 类型限制为 36 个字符，所以，将截断超过该长度的字符。
  
```sql
DECLARE @ID nvarchar(max) = N'0E984725-C51C-4BF4-9960-E1C80E27ABA0wrong';  
SELECT @ID, CONVERT(uniqueidentifier, @ID) AS TruncatedValue;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```
String                                       TruncatedValue  
-------------------------------------------- ------------------------------------  
0E984725-C51C-4BF4-9960-E1C80E27ABA0wrong    0E984725-C51C-4BF4-9960-E1C80E27ABA0  
  
(1 row(s) affected)  
```  
  
## <a name="see-also"></a>另请参阅
[nchar 和 nvarchar (Transact-SQL)](../../t-sql/data-types/nchar-and-nvarchar-transact-sql.md)  
[CAST 和 CONVERT (Transact-SQL)](../../t-sql/functions/cast-and-convert-transact-sql.md)  
[COLLATE (Transact-SQL)](../../t-sql/statements/collations.md)  
[数据类型转换（数据库引擎）](../../t-sql/data-types/data-type-conversion-database-engine.md)  
[数据类型 (Transact-SQL)](../../t-sql/data-types/data-types-transact-sql.md)  
[估计数据库的大小](../../relational-databases/databases/estimate-the-size-of-a-database.md)     
[排序规则和 Unicode 支持](../../relational-databases/collations/collation-and-unicode-support.md)    
[单字节和多字节字符集](/cpp/c-runtime-library/single-byte-and-multibyte-character-sets)
  
