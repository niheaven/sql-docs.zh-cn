---
title: "视图 （Integration Services 目录） |Microsoft 文档"
ms.custom: 
ms.date: 12/16/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords:
- views [Integration Services]
ms.assetid: d0294d43-4852-46dc-9afa-d0c19ea9aa03
caps.latest.revision: 18
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: b7293a70046df19eef816d3e7830518959ecbc98
ms.contentlocale: zh-cn
ms.lasthandoff: 09/26/2017

---
# <a name="views-integration-services-catalog"></a>视图（Integration Services 目录）
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  本节介绍可用于管理已部署到 [!INCLUDE[tsql](../../includes/tsql-md.md)] 实例的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 项目的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 视图。  
  
 查询[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]视图以检查对象、 设置和操作数据存储在**SSISDB**目录。  
  
 该目录的默认名称是 SSISDB。 目录中存储的对象包括项目、包、参数环境和操作历史记录。  
  
 您可以直接使用数据库视图和存储过程，或者编写调用托管 API 的自定义代码。 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 和托管 API 查询这些视图，并调用本节中介绍的存储过程来执行许多任务。  
  
## <a name="in-this-section"></a>本节内容  
 [catalog.catalog_properties &#40;SSISDB 数据库 &#41;](../../integration-services/system-views/catalog-catalog-properties-ssisdb-database.md)  
 显示 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 目录的属性。  
  
 [catalog.effective_object_permissions &#40;SSISDB 数据库 &#41;](../../integration-services/system-views/catalog-effective-object-permissions-ssisdb-database.md)  
 显示 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 目录中所有对象的当前主体的有效权限。  
  
 [catalog.environment_variables（SSISDB 数据库）](../../integration-services/system-views/catalog-environment-variables-ssisdb-database.md)  
 显示 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 目录中所有环境的环境变量详细信息。  
  
 [catalog.environments（SSISDB 数据库）](../../integration-services/system-views/catalog-environments-ssisdb-database.md)  
 显示 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 目录中所有环境的环境详细信息。 环境包含可由 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 项目引用的变量。  
  
 [catalog.execution_parameter_values（SSISDB 数据库）](../../integration-services/system-views/catalog-execution-parameter-values-ssisdb-database.md)  
 显示 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 包在执行实例过程中使用的实际参数值。  
  
 [catalog.executions（SSISDB 数据库）](../../integration-services/system-views/catalog-executions-ssisdb-database.md)  
 在 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 目录中显示包执行的实例。 通过“执行包”任务执行的包在同一个执行实例中作为父包运行。  
  
 [catalog.explicit_object_permissions &#40;SSISDB 数据库 &#41;](../../integration-services/system-views/catalog-explicit-object-permissions-ssisdb-database.md)  
 仅显示已显式分配给此用户的权限。  
  
 [catalog.extended_operation_info（SSISDB 数据库）](../../integration-services/system-views/catalog-extended-operation-info-ssisdb-database.md)  
 显示 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 目录中所有操作的扩展信息。  
  
 [catalog.folders &#40;SSISDB 数据库 &#41;](../../integration-services/system-views/catalog-folders-ssisdb-database.md)  
 显示 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 目录中的文件夹。  
  
 [catalog.object_parameters（SSISDB 数据库）](../../integration-services/system-views/catalog-object-parameters-ssisdb-database.md)  
 显示 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 目录中所有包和项目的参数。  
  
 [catalog.object_versions（SSISDB 数据库）](../../integration-services/system-views/catalog-object-versions-ssisdb-database.md)  
 显示 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 目录中对象的版本。 在此版本中，此视图只支持项目的版本。  
  
 [catalog.operation_messages（SSISDB 数据库）](../../integration-services/system-views/catalog-operation-messages-ssisdb-database.md)  
 显示在 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 目录中执行操作期间记录的消息。  
  
 [catalog.operations（SSISDB 数据库）](../../integration-services/system-views/catalog-operations-ssisdb-database.md)  
 显示 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 目录中所有操作的详细信息。  
  
 [catalog.packages（SSISDB 数据库）](../../integration-services/system-views/catalog-packages-ssisdb-database.md)  
 显示 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 目录中显示的所有包的详细信息。  
  
 [catalog.environment_references（SSISDB 数据库）](../../integration-services/system-views/catalog-environment-references-ssisdb-database.md)  
 显示 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 目录中所有项目的环境引用。  
  
 [catalog.projects（SSISDB 数据库）](../../integration-services/system-views/catalog-projects-ssisdb-database.md)  
 显示 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 目录中显示的所有项目的详细信息。  
  
 [catalog.validations &#40;SSISDB 数据库 &#41;](../../integration-services/system-views/catalog-validations-ssisdb-database.md)  
 显示 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 目录中所有项目和包验证的详细信息。  
  
[catalog.master_properties &#40;SSISDB 数据库 &#41;](../../integration-services/system-views/catalog-master-properties-ssisdb-database.md)  
显示的属性[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]缩放出 Master。

[catalog.worker_agents &#40;SSISDB 数据库 &#41;](../../integration-services/system-views/catalog-worker-agents-ssisdb-database.md)  
显示的信息[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]横向扩展辅助进程。  
