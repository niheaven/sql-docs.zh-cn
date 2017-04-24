---
title: "修改作业 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- jobs [SQL Server Agent], modifying
- modifying jobs
- SQL Server Agent jobs, modifying
ms.assetid: dd5e5f20-20c4-4ab9-a19a-db87577dcd43
caps.latest.revision: 5
author: stevestein
ms.author: sstein
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 34e8c912bf0499166a20fc49fd807544d2b808bd
ms.lasthandoff: 04/11/2017

---
# <a name="modify-a-job"></a>Modify a Job
本主题介绍如何在 [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 、 [!INCLUDE[ssCurrent](../../includes/sscurrent_md.md)] 或 SQL Server 管理对象更改 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)], [!INCLUDE[tsql](../../includes/tsql_md.md)]， or SQL Server Management Objects.  
  
**本主题内容**  
  
-   **开始之前：** ，  
  
    [限制和局限](#Restrictions)  
  
    [Security](#Security)  
  
-   **若要修改作业，可使用：**  
  
    [SQL Server Management Studio](#SSMS)  
  
    [Transact-SQL](#TSQL)  
  
    [SQL Server 管理对象](#SMO)  
  
## <a name="BeforeYouBegin"></a>开始之前  
  
### <a name="Restrictions"></a>限制和局限  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 代理主作业不能同时把本地服务器和远程服务器作为目标。  
  
### <a name="Security"></a>Security  
除非您是 **sysadmin** 固定服务器角色的成员，否则您只能修改自己拥有的作业。 有关详细信息，请参阅 [Implement SQL Server Agent Security](../../ssms/agent/implement-sql-server-agent-security.md)。  
  
## <a name="SSMS"></a>使用 SQL Server Management Studio  
  
#### <a name="to-modify-a-job"></a>修改作业  
  
1.  在 **“对象资源管理器”** 中，连接到 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion_md.md)]的实例，然后展开该实例。  
  
2.  展开“SQL Server 代理”，再展开“作业”，然后右键单击要修改的作业，再单击“属性”。  
  
3.  在 **“作业属性”** 对话框中，使用相应的页来更新作业的属性、步骤、计划、警报和通知。  
  
## <a name="TSQL"></a>使用 Transact-SQL  
  
#### <a name="to-modify-a-job"></a>修改作业  
  
1.  在对象资源管理器中，连接到数据库引擎实例，然后展开该实例。  
  
2.  在工具栏上，单击 **“新建查询”**。  
  
3.  在查询窗口中，使用以下系统存储过程修改作业。  
  
    -   执行 [sp_update_job (TRANSACT-SQL)](http://msdn.microsoft.com/en-us/cbdfea38-9e42-47f3-8fc8-5978b82e2623) 更改作业属性。  
  
    -   执行 [sp_update_schedule (Transact-SQL)](http://msdn.microsoft.com/en-us/97b3119b-e43e-447a-bbfb-0b5499e2fefe) 更改作业定义的计划详细信息。  
  
    -   执行 [sp_add_jobstep (Transact-SQL)](http://msdn.microsoft.com/en-us/97900032-523d-49d6-9865-2734fba1c755) 添加新的作业步骤。  
  
    -   执行 [sp_update_jobstep (Transact-SQL)](http://msdn.microsoft.com/en-us/e158802c-c347-4a5d-bf75-c03e5ae56e6b) 更改原先存在的作业步骤。  
  
    -   执行 [sp_delete_jobstep (TRANSACT-SQL)](http://msdn.microsoft.com/en-us/421ede8e-ad57-474a-9fb9-92f70a3e77e3) 从作业中删除作业步骤。  
  
    -   修改任何 SQLServer 代理主作业的其他存储过程：  
  
        -   执行 [sp_delete_jobserver (Transact-SQL)](http://msdn.microsoft.com/en-us/6d63ed32-68cf-4d8f-aa40-05a3826e05b8) 删除当前与作业相关联的服务器。  
  
        -   执行 [sp_add_jobserver (Transact-SQL)](http://msdn.microsoft.com/en-us/485252cc-0081-490a-9bd1-cbbd68eea286) 将某个服务器与当前作业相关联。  
  
## <a name="SMO"></a>使用 SQL Server 管理对象  
**修改作业**  
  
通过使用所选编程语言（如 Visual Basic、Visual C# 或 PowerShell）来使用 **Job** 类。 有关详细信息，请参阅 [SQL Server 管理对象 (SMO)](http://msdn.microsoft.com/library/ms162169.aspx)。  
  
