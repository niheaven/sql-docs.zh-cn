---
title: 处理挖掘结构 |Microsoft 文档
ms.custom: ''
ms.date: 03/13/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: data-mining
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- mining structures [Analysis Services], processing
ms.assetid: 4162f33e-c23f-4293-8905-271781e45fa4
caps.latest.revision: 31
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: d47f0b304e96231af7db50861ac7d2612567986c
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="process-a-mining-structure"></a>处理挖掘结构
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  必须先部署 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 项目并处理挖掘结构和挖掘模型，然后才能浏览或使用与挖掘结构关联的挖掘模型。 此外，如果更改了挖掘结构或挖掘模型，则系统会提示您重新对其进行部署和处理。 处理 **中数据挖掘设计器的** “挖掘结构” [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 选项卡中的结构时，也会处理所有关联的模型。  
  
 可以使用这些工具处理挖掘结构：  
  
-   [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]  
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]  
  
-   XMLA：“处理”命令  
  
 有关如何处理单个模型的信息，请参阅 [处理挖掘模型](../../analysis-services/data-mining/process-a-mining-model.md)。  
  
### <a name="to-process-a-mining-structure-and-all-associated-mining-models-using-sql-server-data-tools"></a>使用 SQL Server Data Tools 处理挖掘结构和所有关联的挖掘模型  
  
1.  从 **中的** “挖掘模型” **菜单项中，选择** “处理挖掘结构和所有模型” [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]。  
  
     如果更改了结构，则在处理模型之前，系统会提示您重新部署该结构。 单击 **“是”**。  
  
2.  单击**运行**中**处理挖掘结构\<结构 >** 对话框。  
  
     **“处理进度”** 对话框将打开以显示有关模型处理的详细信息。  
  
3.  模型处理完成后，在 **“处理进度”** 对话框中单击 **“关闭”** 。  
  
4.  单击**关闭**中**处理挖掘结构\<结构 >** 对话框。  
  
## <a name="see-also"></a>另请参阅  
 [挖掘结构任务和操作指南](../../analysis-services/data-mining/mining-structure-tasks-and-how-tos.md)  
  
  