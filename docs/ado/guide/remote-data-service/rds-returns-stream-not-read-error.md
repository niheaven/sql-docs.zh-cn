---
title: RDS 返回&quot;Stream 未读取&quot;错误 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- stream not read error in RDS [ADO]
ms.assetid: cb5a68f8-dba4-41da-bafd-04efe53706b7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: bc2944e213e2a6a8ba3f9dc51a9a23b496f4e31a
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47613915"
---
# <a name="rds-returns-quotstream-not-readquot-error"></a>RDS 返回&quot;Stream 未读取&quot;错误
"Stream 对象无法进行读取，因为它为空，或者当前位于末尾的 Stream。 对于非空流，设置 Position 属性与当前的位置。 若要确定 Stream 是否为空，请检查大小属性。"  
  
 如果看到此错误消息，你可能已尝试通过 http 使用参数化的分层查询。 RDS 不允许你使用远程参数化层次结构。  
  
> [!IMPORTANT]
>  从 Windows 8 和 Windows Server 2012 开始，不再在 Windows 操作系统中包含 RDS 服务器组件 (请参阅 Windows 8 和[Windows Server 2012 兼容性指南](https://www.microsoft.com/en-us/download/details.aspx?id=27416)以了解详细信息)。 将 Windows 的未来版本中删除 RDS 客户端组件。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 使用 RDS 的应用程序应迁移到[WCF 数据服务](http://go.microsoft.com/fwlink/?LinkId=199565)。  
  
## <a name="see-also"></a>请参阅  
 [RDS 基础知识](../../../ado/guide/remote-data-service/rds-fundamentals.md)


