---
title: 发布属性 - 常规 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql13.rep.newpubwizard.pubproperties.general.f1
ms.assetid: 7912362f-c4d6-4f60-bd39-dee1f656ed18
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 6bbcd23aa185e9d311fbc8b81d9ab167717997b2
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47718755"
---
# <a name="publication-properties-general"></a>发布属性，常规
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  **“发布属性”** 对话框的 **“常规”** 页包含发布的基本信息，包括名称、说明和订阅过期策略。  
  
## <a name="options"></a>选项  
 **名称**  
 发布的名称（只读）。  
  
 **“数据库”**  
 发布数据库的名称（只读）。  
  
 **Description**  
 发布的说明。  
  
 **类型**  
 发布的类型（只读）。  
  
 **订阅过期**  
 选择以下订阅过期选项之一： **“订阅永不过期”** 或 **“订阅过期”**，并明确指定时间段（**“间隔”**）。  
  
 对于快照和事务发布， [!INCLUDE[msCoName](../../includes/msconame-md.md)] 建议您接受默认选项 **“订阅永不过期”**。  
  
 对于合并复制， [!INCLUDE[msCoName](../../includes/msconame-md.md)] 建议您接受默认选项 **“订阅过期”** ，并设置尽可能低的 **“间隔”**。 元数据的存储量会随着订阅过期时间的增加而增加，这会影响性能。 这需要在要求订阅服务器在更长的时间内保持断开或不同步与存储和处理大量元数据所带来的性能问题之间取得平衡。  
  
 有关详细信息，请参阅 [Subscription Expiration and Deactivation](../../relational-databases/replication/subscription-expiration-and-deactivation.md)。  
  
 **兼容级别**  
 仅限[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 和更高版本；仅限合并发布。 选择与此发布同步的订阅服务器所需的最低 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本。 有多个与确定兼容级别有关的规则。  
  
## <a name="see-also"></a>另请参阅  
 [Create a Publication](../../relational-databases/replication/publish/create-a-publication.md)   
 [查看和修改发布属性](../../relational-databases/replication/publish/view-and-modify-publication-properties.md)   
 [发布数据和数据库对象](../../relational-databases/replication/publish/publish-data-and-database-objects.md)  
  
  
