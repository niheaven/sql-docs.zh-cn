---
title: "@@VERSION (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- '@@VERSION'
- '@@VERSION_TSQL'
dev_langs:
- TSQL
helpviewer_keywords:
- '@@VERSION function'
- current SQL Server installation information
- versions [SQL Server], @@VERSION
- processors [SQL Server], types
ms.assetid: 385ba80e-7c28-41a5-9cdb-5648f3785983
caps.latest.revision: 40
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: b8367bb24a37996b2956e3107113812a32086fed
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="version---transact-sql-configuration-functions"></a>版本-Transact SQL 配置函数
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  返回 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的当前安装的系统和生成信息。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
-- Syntax for SQL Server, Azure SQL Database, Azure SQL Data Warehouse, Parallel Data Warehouse  
  
@@VERSION  
```  
  
## <a name="return-types"></a>返回类型  
 **nvarchar**  
  
## <a name="remarks"></a>注释  
 @@VERSION结果显示为一个 nvarchar 字符串。 你可以使用[SERVERPROPERTY &#40;Transact SQL &#41;](../../t-sql/functions/serverproperty-transact-sql.md)函数来检索单个属性值。  
  
 对于 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，返回以下信息。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]版本  
  
-   处理器体系结构  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 生成日期  
  
-   版权声明  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本  
  
-   操作系统版本  
  
 对于 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]，返回以下信息。  
  
-   版本 -“Windows Azure SQL Database”  
  
-   产品级别 -“(CTP)”或“(RTM)”  
  
-   产品版本  
  
-   生成日期  
  
-   版权声明  
  
## <a name="examples"></a>示例  
  
### <a name="a-return-the-current-version-of-includessnoversionincludesssnoversion-mdmd"></a>答： 返回的当前版本[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
 以下示例显示返回当前安装的版本信息。  
  
```  
SELECT @@VERSION AS 'SQL Server Version';  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>示例：[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]和[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="b-return-the-current-version-of-includessdwincludesssdw-mdmd"></a>B. 返回当前版本的[!INCLUDE[ssDW](../../includes/ssdw-md.md)]  
  
```  
SELECT @@VERSION AS 'SQL Server PDW Version';  
```  
  
## <a name="see-also"></a>另请参阅  
 [SERVERPROPERTY (Transact-SQL)](../../t-sql/functions/serverproperty-transact-sql.md)  
  
  

