---
title: sp_replmonitorchangepublicationthreshold (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology:
- replication
ms.topic: language-reference
f1_keywords:
- sp_replmonitorchangepublicationthreshold_TSQL
- sp_replmonitorchangepublicationthreshold
helpviewer_keywords:
- sp_replmonitorchangepublicationthreshold
ms.assetid: 2c3615d8-4a1a-4162-b096-97aefe6ddc16
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 0bb8c060963f92ec14d140cf3b8649216fd89bf8
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47850575"
---
# <a name="spreplmonitorchangepublicationthreshold-transact-sql"></a>sp_replmonitorchangepublicationthreshold (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  更改发布的监视阈值标准。 在分发服务器的分发数据库上执行此存储过程，用于监视复制。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_replmonitorchangepublicationthreshold [ @publisher = ] 'publisher'  
        , [ @publisher_db = ] 'publisher_db'  
        , [ @publication = ] 'publication'   
    [ , [ @publication_type = ] publication_type ]   
    [ , [ @metric_id = ] metric_id ]   
    [ , [ @thresholdmetricname = ] 'thresholdmetricname'   
    [ , [ @value = ] value ]   
    [ , [ @shouldalert = ] shouldalert ]   
    [ , [ @mode = ] mode ]  
```  
  
## <a name="arguments"></a>参数  
 [ **@publisher** = ] **'***publisher***'**  
 发布服务器的名称。 *发布服务器*是**sysname**，无默认值。  
  
 [ **@publisher_db** = ] **'***publisher_db***'**  
 已发布数据库的名称。 *publisher_db*是**sysname**，无默认值。  
  
 [ **@publication** = ] **'***publication***'**  
 正在更改其监视阈值属性的发布的名称。 *发布*是**sysname**，无默认值。  
  
 [ **@publication_type** =] *publication_type*  
 发布的类型。 *publication_type*是**int**，可以是下列值之一。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|**0**|事务发布。|  
|**1**|快照发布。|  
|**2**|合并发布。|  
|NULL（默认值）|复制尝试确定发布类型。|  
  
 [ **@metric_id** =] *metric_id*  
 正在更改的发布阈值标准的 ID。 *metric_id*是**int**，默认值为 NULL 和可以是下列值之一。  
  
|ReplTest1|标准名称|  
|-----------|-----------------|  
|**1**|**expiration** - 监视对事务发布的订阅是否即将过期。|  
|**2**|**latency** - 监视对事务发布的订阅的性能。|  
|**4**|**mergeexpiration** - 监视对合并发布的订阅是否即将过期。|  
|**5**|**mergeslowrunduration** -监视通过低带宽 （拨号） 连接的合并同步的持续时间。|  
|**6**|**mergefastrunduration** -监视通过高带宽局域网 (LAN) 连接的合并同步的持续时间。|  
|**7**|**mergefastrunspeed** - 监视通过高带宽 (LAN) 连接进行的合并同步的同步速率。|  
|**8**|**mergeslowrunspeed** -监视通过低带宽 （拨号） 连接的合并同步的同步速率。|  
  
 您必须指定这两*metric_id*或*thresholdmetricname*。 如果*thresholdmetricname*指定了，则*metric_id*应为 NULL。  
  
 [ **@thresholdmetricname** =] **'***thresholdmetricname*****  
 正在更改的发布阈值标准的名称。 *thresholdmetricname*是**sysname**，默认值为 NULL。 您必须指定这两*thresholdmetricname*或*metric_id*。 如果*metric_id*指定了，则*thresholdmetricname*应为 NULL。  
  
 [ **@value** =]*值*  
 是发布阈值标准的新值。 *值*是**int**，默认值为 NULL。 如果**null**，则不更新指标值。  
  
 [ **@shouldalert** =] *shouldalert*  
 指示达到发布阈值标准时是否生成警报。 *shouldalert*是**位**，默认值为 NULL。 值为**1**意味着，会生成警报，并将值**0**意味着不会生成警报。  
  
 [ **@mode** =]*模式*  
 指示是否启用发布阈值标准。 *模式*是**tinyint**，默认值为**1**。 值为**1**方法，启用该标准的监视，并将值**2**表示禁用该标准的监视。  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="remarks"></a>备注  
 **sp_replmonitorchangepublicationthreshold**用于所有类型的复制。  
  
## <a name="permissions"></a>Permissions  
 只有的成员**db_owner**或**replmonitor**分发数据库中的固定的数据库角色可以执行**sp_replmonitorchangepublicationthreshold**。  
  
## <a name="see-also"></a>请参阅  
 [以编程方式监视复制](../../relational-databases/replication/monitor/programmatically-monitor-replication.md)  
  
  
