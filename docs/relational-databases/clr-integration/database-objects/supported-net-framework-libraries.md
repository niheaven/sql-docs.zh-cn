---
title: 支持的.NET Framework 库 |Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- common language runtime [SQL Server], .NET Framework libraries
- .NET Framework [CLR Integration]
ms.assetid: 417544ff-c25c-496e-add4-2f278f8a4911
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 800b2f3bbfe5547931bc66322817f9a221cf3a8a
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47704015"
---
# <a name="supported-net-framework-libraries"></a>支持的 .NET Framework 库
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  借助驻留在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 中的公共语言运行时 (CLR)，您可以采用托管代码创作存储过程、触发器、用户定义函数、用户定义类型和用户定义聚合。 利用 .NET Framework 类库中的功能，您可以访问提供字符串操作、高级数学运算、文件访问和密码系统等功能的预建类。 可通过任何托管存储过程、用户定义类型、触发器、用户定义函数或用户定义聚合访问这些类。  
  
> [!NOTE]  
>  如果在全局程序集缓存 (GAC) 中对不支持的程序集提供服务或升级，[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 应用程序可能会停止运行。 其原因在于在 GAC 中对库提供服务或升级并不会更新 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 中的相应程序集。 如果某一程序集存在于 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 数据库和 GAC 中，该程序集的两个副本必须完全匹配。 如果不一致，当 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] CLR 集成功能使用该程序集时，将发生错误。 如果服务或升级，还会在数据库中，包括不受支持的.NET Framework 程序集注册任何程序集位于 GAC 中请确保还提供服务或升级中的程序集复制你[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]数据库与**ALTER ASSEMBLY**语句。 有关详细信息，请参阅[知识库文章 949080](http://support.microsoft.com/kb/949080)。  
  
## <a name="supported-libraries"></a>支持的库  
 从 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 开始，[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 包含一系列支持的 .NET Framework 库，已对这些库进行测试，确保它们满足与 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 集成的可靠性和安全性标准。 在代码中使用支持的库之前，您不需要在服务器上显式注册这些库；[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 从全局程序集缓存 (GAC) 中直接加载这些库。  
  
 在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 中，CLR 集成支持的库/命名空间包括：  
  
-   CustomMarshalers  
  
-   Microsoft.VisualBasic  
  
-   Microsoft.VisualC  
  
-   mscorlib  
  
-   系统  
  
-   System.Configuration  
  
-   System.Data  
  
-   System.Data.OracleClient  
  
-   System.Data.SqlXml  
  
-   System.Deployment  
  
-   System.Security  
  
-   System.Transactions  
  
-   System.Web.Services  
  
-   System.Xml  
  
-   System.Core.dll  
  
-   System.Xml.Linq.dll  
  
## <a name="unsupported-libraries"></a>不支持的库  
 通过托管存储过程、触发器、用户定义函数、用户定义类型和用户定义聚合仍可以调用不支持的库。 不支持的库必须首先注册[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]数据库，请使用**CREATE ASSEMBLY**语句，然后可以在代码中使用它。 对于在服务器上注册和运行的任何不支持的库，应检查和测试其安全性和可靠性。  
  
 例如， **System.DirectoryServices**不支持命名空间。 必须注册 System.DirectoryServices.dll 程序集与**UNSAFE**权限才能在代码中调用。 **UNSAFE**必要权限，是因为中的类**System.DirectoryServices**命名空间不满足的要求**安全**或**EXTERNAL_ACCESS**。 有关详细信息，请参阅[CLR 集成编程模型限制](../../../relational-databases/clr-integration/database-objects/clr-integration-programming-model-restrictions.md)并[CLR 集成代码访问安全性](../../../relational-databases/clr-integration/security/clr-integration-code-access-security.md)。  
  
## <a name="see-also"></a>请参阅  
 [创建程序集](../../../relational-databases/clr-integration/assemblies/creating-an-assembly.md)   
 [CLR 集成代码访问安全性](../../../relational-databases/clr-integration/security/clr-integration-code-access-security.md)   
 [CLR 集成编程模型限制](../../../relational-databases/clr-integration/database-objects/clr-integration-programming-model-restrictions.md)  
  
  
