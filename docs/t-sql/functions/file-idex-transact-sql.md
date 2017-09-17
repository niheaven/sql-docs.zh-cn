---
title: "改用 FILE_IDEX (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- FILE_IDEX
- FILE_IDEX_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- FILE_IDEX function
- IDs [SQL Server], files
- file IDs [SQL Server]
- names [SQL Server], files
- identification numbers [SQL Server], files
- file names [SQL Server], FILE_IDEX
ms.assetid: 7532fea5-ee5e-4edd-b98b-111a7ba56c8e
caps.latest.revision: 35
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: df818b30ca850fbb3b7cb0df816aacb6afa12a76
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="fileidex-transact-sql"></a>FILE_IDEX (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  返回当前数据库中的数据、日志或全文文件的指定逻辑文件名的文件标识 (ID) 号。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
FILE_IDEX ( file_name )  
```  
  
## <a name="arguments"></a>参数  
 *文件名*  
 类型的表达式**sysname** ，表示为其返回文件 id。 该文件的名称  
  
## <a name="return-types"></a>返回类型  
 **int**  
  
 **NULL**错误  
  
## <a name="remarks"></a>注释  
 *file_name*对应于显示中的逻辑文件名称**名称**中的列[sys.master_files](../../relational-databases/system-catalog-views/sys-master-files-transact-sql.md)或[sys.database_files](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md)目录视图。  
  
 FILE_IDEX 可以在选择列表、WHERE 子句和允许使用表达式的任何地方使用。 有关详细信息，请参阅[表达式 (Transact-SQL)](../../t-sql/language-elements/expressions-transact-sql.md)。  
  
## <a name="examples"></a>示例  
  
### <a name="a-retrieving-the-file-id-of-a-specified-file"></a>A. 检索指定文件的文件 ID  
 以下示例返回 `AdventureWorks_Data` 文件的文件 ID。  
  
```tsql  
USE AdventureWorks2012;  
GO  
SELECT FILE_IDEX('AdventureWorks2012_Data')AS 'File ID';  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
File ID   
-------   
1  
(1 row(s) affected)  
```  
  
### <a name="b-retrieving-the-file-id-when-the-file-name-is-not-known"></a>B. 在文件名未知时检索文件 ID  
 以下示例通过从文件类型等于 `AdventureWorks`（日志）的 `sys.database`_`files` 目录视图中选择逻辑文件名来返回 `1` 日志文件的文件 ID。  
  
```tsql  
USE AdventureWorks2012;  
GO  
SELECT FILE_IDEX((SELECT TOP(1)name FROM sys.database_files   
WHERE type = 1))AS 'File ID';  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
File ID   
-------   
2  
```  
  
### <a name="c-retrieving-the-file-id-of-a-full-text-catalog-file"></a>C. 检索全文目录文件的文件 ID  
 以下示例通过从文件类型等于 `sys.database`（全文本）的 `files`_`4` 目录视图中选择逻辑文件名来返回全文本文件的文件 ID。 如果全文目录不存在，则此示例将返回 NULL。  
  
```tsql  
SELECT FILE_IDEX((SELECT name FROM sys.master_files WHERE type = 4))  
AS 'File_ID';  
```  
  
## <a name="see-also"></a>另请参阅  
 [元数据函数 &#40;Transact SQL &#41;](../../t-sql/functions/metadata-functions-transact-sql.md)   
 [sys.database_files (Transact-SQL)](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md)   
 [sys.master_files (Transact-SQL)](../../relational-databases/system-catalog-views/sys-master-files-transact-sql.md)  
  
  