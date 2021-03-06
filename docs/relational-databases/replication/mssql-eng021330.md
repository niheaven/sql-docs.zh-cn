---
title: MSSQL_ENG021330 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- MSSQL_ENG021330 error
ms.assetid: e2bb2e21-62a7-4689-b68b-bdfba3fdd985
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 05a2b45668efdd1bcef6b30e009d8248cb96e2be
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47620966"
---
# <a name="mssqleng021330"></a>MSSQL_ENG021330
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
## <a name="message-details"></a>消息详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|21330|  
|事件源|MSSQLSERVER|  
|组件|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|符号名称||  
|消息正文|无法在复制工作目录下创建子目录。(%ls)|  
  
## <a name="explanation"></a>解释  
 当手动初始化订阅而且创建存储复制脚本的目录有问题时，会出现此错误。 权限问题可导致此错误：在不使用快照的情况下初始化订阅时，在发布服务器上运行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服务的帐户对分发服务器上的快照文件夹必须具有写权限。  
  
## <a name="user-action"></a>用户操作  
 请确保已为快照文件夹指定正确的路径，并且在发布服务器上运行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服务的帐户具有足够的权限。  
  
## <a name="see-also"></a>另请参阅  
 [指定默认快照位置 (SQL Server Management Studio)](../../relational-databases/replication/specify-the-default-snapshot-location-sql-server-management-studio.md)   
 [错误和事件参考（复制）](../../relational-databases/replication/errors-and-events-reference-replication.md)   
 [初始化事务订阅（不使用快照）](../../relational-databases/replication/initialize-a-transactional-subscription-without-a-snapshot.md)  
  
  
