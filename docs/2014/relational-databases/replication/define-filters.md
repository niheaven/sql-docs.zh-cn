---
title: 定义筛选器 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- replication
ms.topic: conceptual
f1_keywords:
- sql12.rep.replconflictviewer.definefilters.f1
helpviewer_keywords:
- Define Filters dialog box
ms.assetid: 1fa71d22-ce5a-4aae-ba05-4d755842aeac
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 0f20cb709176b96aa850aa616d7bf57218137896
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48201347"
---
# <a name="define-filters"></a>定义筛选器
  可以使用 **“定义筛选器”** 对话框定义筛选器，然后将筛选器应用于数据冲突以在网格中查看冲突的子集。 若要定义筛选器，请从 **“运算符”** 下拉列表框中选择运算符，然后输入值。 例如，若要只显示冲突解决落选方为服务器 **ReplTest1**的那些冲突，请从 **“运算符”** 下拉列表框中选择 **“等于”** ，然后在第一个 **“值”** 列中输入 **ReplTest1** 。  
  
## <a name="options"></a>选项  
 **“运算符”**  
 为筛选器选择一个运算符，例如 **“小于或等于”**。  
  
 **ReplTest1**  
 为筛选器输入一个值。 大多数运算符只需要在第一个 **“值”** 列中输入值，但 **“介于”** 和 **“不介于”** 运算符需要在两个 **“值”** 列中都输入值。  
  
 **Clear**  
 单击此按钮可以清除先前定义的所有筛选器。  
  
## <a name="see-also"></a>请参阅  
 [Microsoft 复制冲突查看器（合并复制）](microsoft-replication-conflict-viewer-merge-replication.md)   
 [Microsoft 复制冲突查看器（事务复制）](microsoft-replication-conflict-viewer-transactional-replication.md)  
  
  
