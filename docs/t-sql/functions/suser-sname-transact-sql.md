---
title: "SUSER_SNAME (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 07/29/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- SUSER_SNAME_TSQL
- SUSER_SNAME
dev_langs:
- TSQL
helpviewer_keywords:
- security identification names [SQL Server]
- logins [SQL Server], users
- SIDs [SQL Server]
- SUSER_SNAME function
- users [SQL Server], logins
- logins [SQL Server], names
- IDs [SQL Server], logins
- identification numbers [SQL Server], logins
- names [SQL Server], logins
ms.assetid: 11ec7d86-d429-4004-a436-da25df9f8761
caps.latest.revision: 24
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 35e3429d49940cd863cd04fc336226268ddf61c9
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="susersname-transact-sql"></a>SUSER_SNAME (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  返回与安全标识号 (SID) 关联的登录名。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
-- Syntax for SQL Server, Azure SQL Database, Azure SQL Data Warehouse, Parallel Data Warehouse  
  
SUSER_SNAME ( [ server_user_sid ] )   
```  
  
## <a name="arguments"></a>参数  
 *server_user_sid*  
**适用于**:[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]通过[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]
  
 可选的登录安全标识号。 *server_user_sid*是**varbinary(85)**。 *server_user_sid*可以是任意的安全标识号[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]登录名或[!INCLUDE[msCoName](../../includes/msconame-md.md)]Windows 用户或组。 如果*server_user_sid*是未指定，返回有关当前用户的信息。 如果此参数包含词 NULL，将返回 NULL。  
  
## <a name="return-types"></a>返回类型  
 **nvarchar （128)**  
  
## <a name="remarks"></a>注释  
 SUSER_SNAME 在 ALTER TABLE 或 CREATE TABLE 中可用作 DEFAULT 约束。 SUSER_SNAME 可以在选择列表、WHERE 子句和任何允许使用表达式的地方使用。 SUSER_SNAME 必须始终后跟括号，即使在未指定参数的情况下也是如此。  
  
 在无参数的情况下调用时，SUSER_SNAME 返回当前安全上下文的名称。 当通过使用 EXECUTE AS 切换上下文的批中无参数调用 SUSER_SNAME 时，将返回模拟上下文的名称。 从模拟上下文中调用时，ORIGINAL_LOGIN 将返回原始上下文的名称。  
  
## <a name="includesssdsfullincludessssdsfull-mdmd-remarks"></a>[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] 备注  
 SUSER_NAME 始终返回当前安全上下文的登录名。  
  
 SUSER_SNAME 语句不支持通过 EXECUTE AS 使用模拟安全上下文执行。  
  
## <a name="examples"></a>示例  
  
### <a name="a-using-susersname"></a>A. 使用 SUSER_SNAME  
 下面的示例返回当前安全上下文的登录名。  
  
```  
SELECT SUSER_SNAME();  
GO  
```  
  
### <a name="b-using-susersname-with-a-windows-user-security-id"></a>B. 使用带 Windows 用户安全 ID 的 SUSER_SNAME  
 以下示例返回与 Windows 安全标识号关联的登录名。  
  
**适用于**:[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]通过[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]
  
```  
SELECT SUSER_SNAME(0x010500000000000515000000a065cf7e784b9b5fe77c87705a2e0000);  
GO  
```  
  
### <a name="c-using-susersname-as-a-default-constraint"></a>C. 将 SUSER_SNAME 用作 DEFAULT 约束  
 下面的示例在 `SUSER_SNAME` 语句中使用 `DEFAULT` 作为 `CREATE TABLE` 约束。  
  
```  
USE AdventureWorks2012;  
GO  
CREATE TABLE sname_example  
(  
login_sname sysname DEFAULT SUSER_SNAME(),  
employee_id uniqueidentifier DEFAULT NEWID(),  
login_date  datetime DEFAULT GETDATE()  
);   
GO  
INSERT sname_example DEFAULT VALUES;  
GO  
```  
  
### <a name="d-calling-susersname-in-combination-with-execute-as"></a>D. 与 EXECUTE AS 一起调用 SUSER_SNAME  
 该示例显示了从模拟上下文调用时的 SUSER_SNAME 的行为。  
  
**适用于**:[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]通过[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]
  
```  
SELECT SUSER_SNAME();  
GO  
EXECUTE AS LOGIN = 'WanidaBenShoof';  
SELECT SUSER_SNAME();  
REVERT;  
GO  
SELECT SUSER_SNAME();  
GO  
  
```  
  
 下面是结果。  
  
 `sa`  
  
 `WanidaBenShoof`  
  
 `sa`  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>示例：[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]和[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="e-using-susersname"></a>E. 使用 SUSER_SNAME  
 以下示例返回值为 `0x01` 的安全标识号的登录名。  
  
```  
SELECT SUSER_SNAME(0x01);  
GO  
```  
  
### <a name="f-returning-the-current-login"></a>F. 返回当前的登录名  
 下面的示例返回当前的登录名的登录名。  
  
```  
SELECT SUSER_SNAME() AS CurrentLogin;  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
 [SUSER_SID &#40;Transact SQL &#41;](../../t-sql/functions/suser-sid-transact-sql.md)   
 [主体（数据库引擎）](../../relational-databases/security/authentication-access/principals-database-engine.md)   
 [sys.server_principals (Transact-SQL)](../../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md)   
 [执行 AS &#40;Transact SQL &#41;](../../t-sql/statements/execute-as-transact-sql.md)  
  
  

