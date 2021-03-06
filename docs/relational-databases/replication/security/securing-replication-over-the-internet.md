---
title: 保护通过 Internet 进行的复制 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- security [SQL Server replication], Internet
- Internet [SQL Server replication], security
ms.assetid: 25b7af05-2721-4b24-9083-fb671e8bf4e0
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: e66b0eda909ced92ac1c61fcabc9f25f91068fce
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47762925"
---
# <a name="securing-replication-over-the-internet"></a>Securing Replication Over the Internet
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Internet 上的复制非常灵活，对移动订阅方而言尤为如此，但必须适当地配置 Internet 复制以确保具有足够的安全性。 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] 建议使用下列两种技术之一在 Internet 上安全地共享信息：  
  
-   虚拟专用网络 (VPN)  
  
-   合并复制的 Web 同步选项  
  
## <a name="virtual-private-network"></a>虚拟专用网络  
 虚拟专用网络为在 Internet 上复制 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 数据提供了简便安全的分层方法。 Internet 上的 VPN 连接逻辑上可以像站点间的广域网 (WAN) 链接一样使用。  
  
 其实现方法是允许用户使用如 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows NT 4.0 或 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows 2000 操作系统中的 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] 点对点隧道协议 (PPTP) 或者 Windows 2000 操作系统中的第二层隧道协议 (L2TP)，将 Internet 或另一公用网络作为通道。 此过程提供类似于专用网络中的安全性和功能。  
  
 有关设置 VPN 的详细信息，请参阅 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows 文档。  
  
## <a name="web-synchronization-through-iis"></a>通过 IIS 的 Web 同步  
 合并复制的 Web 同步选项提供了用 HTTPS 协议复制数据的功能，这是一种通过防火墙复制数据的简便方法。 有关详细信息，请参阅[配置 Web 同步](../../../relational-databases/replication/configure-web-synchronization.md)和 [Web 同步的安全体系结构](../../../relational-databases/replication/security/security-architecture-for-web-synchronization.md)。  
  
## <a name="see-also"></a>另请参阅  
 [Replication Security Best Practices](../../../relational-databases/replication/security/replication-security-best-practices.md)   
 [安全性和保护（复制）](../../../relational-databases/replication/security/security-and-protection-replication.md)  
  
  
