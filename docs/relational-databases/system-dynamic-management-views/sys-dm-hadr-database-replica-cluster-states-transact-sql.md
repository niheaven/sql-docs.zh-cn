---
title: sys.dm_hadr_database_replica_cluster_states (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_hadr_database_replica_cluster_states
- dm_hadr_database_replica_cluster_states_TSQL
- sys.dm_hadr_database_replica_cluster_states_TSQL
- dm_hadr_database_replica_cluster_states
dev_langs:
- TSQL
helpviewer_keywords:
- Availability Groups [SQL Server], monitoring
- Availability Groups [SQL Server], WSFC clusters
- sys.dm_hadr_database_replica_cluster_states dynamic management view
ms.assetid: 6f719071-ebce-470d-aebd-1f55ee8cd70a
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 253959175db3519c00874db43466fa21c31cf5e0
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47636675"
---
# <a name="sysdmhadrdatabasereplicaclusterstates-transact-sql"></a>sys.dm_hadr_database_replica_cluster_states (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  返回的行中包含的信息旨在让您洞察 Windows Server 故障转移群集 (WSFC) 群集上每个 Always On 可用性组中的 Alwayson 可用性组中的可用性数据库的运行状况。 查询**sys.dm_hadr_database_replica_states**回答以下问题：  
  
-   可用性组中的所有数据库是否都已做好故障转移准备？  
  
-   执行强制故障转移之后，辅助数据库是否在本地挂起自身并向新的主副本确认了其挂起状态？  
  
-   如果主副本当前不可用，哪一个辅助副本在成为主副本后允许最低限度的数据丢失？  
  
-   时的值[sys.databases](~/relational-databases/system-catalog-views/sys-databases-transact-sql.md)**log_reuse_wait_desc**列为"AVAILABILITY_REPLICA"，可用性组中的哪一个辅助副本正在阻止给定主数据库上的日志截断?     
   
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**replica_id**|**uniqueidentifier**|可用性组内可用性副本的标识符。|  
|**group_database_id**|**uniqueidentifier**|可用性组内数据库的标识符。 在此数据库联接到的每个副本上，该标识符都是相同的。|  
|**database_name**|**sysname**|属于可用性组的数据库的名称。|  
|**is_failover_ready**|**bit**|指示辅助数据库是否与相应的主数据库同步。 其中一种：<br /><br /> 0 = 该数据库在群集中未标记为已同步。 数据库尚未做好故障转移准备。<br /><br /> 1 = 该数据库在群集中标记为已同步。 数据库已做好故障转移准备。|  
|**is_pending_secondary_suspend**|**bit**|指示强制故障转移后，数据库是否正待挂起，可为下列值之一：<br /><br /> 0 = HADR_SYNCHRONIZED_ SUSPENDED 之外的任何状态。<br /><br /> 1 = HADR_SYNCHRONIZED_ SUSPENDED。 强制故障转移完成后，每个辅助数据库将设置为 ADR_SYNCHONIZED_SUSPENDED 并保持此状态，直到新的主副本收到该辅助数据库关于 SUSPEND 消息的确认。<br /><br /> NULL = 未知（无仲裁）|  
|**is_database_joined**|**bit**|指示此可用性副本上的数据库是否已联接到可用性组，可为下列值之一：<br /><br /> 0 = 数据库未联接到此可用性副本上的可用性组。<br /><br /> 1 = 数据库联接到此可用性副本上的可用性组。<br /><br /> NULL = 未知（可用性副本缺少仲裁。）|  
|**recovery_lsn**|**numeric(25,0)**|在主副本上，在恢复或故障转移后、但在副本写入任何新日志记录前事务日志的结尾。 在主副本上，某一给定辅助数据库的行将具有主副本需要辅助副本同步到（即，还原到且重新初始化到）的值。<br /><br /> 在辅助副本上此值为 NULL。 请注意，每个辅助副本将具有 MAX 值或是主副本通知辅助副本返回到的较低值。|  
|**truncation_lsn**|**numeric(25,0)**|[!INCLUDE[ssHADR](../../includes/sshadr-md.md)] 日志截断值，如果阻止本地日志截断（例如由备份操作阻止），该值可能高于本地截断 LSN。|  
  
## <a name="security"></a>安全性  
  
### <a name="permissions"></a>Permissions  
 要求具有服务器的 VIEW SERVER STATE 权限。  
  
## <a name="see-also"></a>请参阅  
 [AlwaysOn 可用性组动态管理视图和函数 (Transact-SQL)](../../relational-databases/system-dynamic-management-views/always-on-availability-groups-dynamic-management-views-functions.md)   
 [AlwaysOn 可用性组目录视图 (Transact-SQL)](../../relational-databases/system-catalog-views/always-on-availability-groups-catalog-views-transact-sql.md)   
 [监视可用性组 (Transact-SQL)](../../database-engine/availability-groups/windows/monitor-availability-groups-transact-sql.md)   
 [AlwaysOn 可用性组 (SQL Server)](../../database-engine/availability-groups/windows/always-on-availability-groups-sql-server.md)   
 [sys.dm_hadr_database_replica_states (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-hadr-database-replica-states-transact-sql.md)  
  
  
