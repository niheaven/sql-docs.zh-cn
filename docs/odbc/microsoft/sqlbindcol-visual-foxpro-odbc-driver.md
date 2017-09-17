---
title: "SQLBindCol （Visual FoxPro ODBC 驱动程序） |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQLBindCol function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: 984d6605-39ba-4d33-ac94-22625bfa6107
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 8f08ffe2a80f89040dc148543c2b3a3985b76eca
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="sqlbindcol-visual-foxpro-odbc-driver"></a>SQLBindCol （Visual FoxPro ODBC 驱动程序）
> [!NOTE]  
>  本主题包含 Visual FoxPro ODBC 驱动程序相关的信息。 有关此函数的常规信息，请参阅下的相应主题[ODBC API 参考](../../odbc/reference/syntax/odbc-api-reference.md)。  
  
 支持： 完整  
  
 ODBC API 一致性： 核心级别  
  
 分配的结果列的存储空间，并指定结果的类型。 当[SQLFetch](../../odbc/microsoft/sqlfetch-visual-foxpro-odbc-driver.md)或[SQLExtendedFetch](../../odbc/microsoft/sqlextendedfetch-visual-foxpro-odbc-driver.md)是调用，该驱动程序在分配的位置放置的所有绑定的列的数据。 请参阅[SQLGetTypeInfo](../../odbc/microsoft/sqlgettypeinfo-visual-foxpro-odbc-driver.md) ODBC 和 Visual FoxPro 数据类型之间的映射。  
  
 有关详细信息，请参阅[SQLBindCol](../../odbc/reference/syntax/sqlbindcol-function.md)中*ODBC 程序员参考*。