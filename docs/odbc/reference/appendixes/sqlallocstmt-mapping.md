---
title: SQLAllocStmt 映射 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- mapping deprecated functions [ODBC], SQLAllocStmt
- SQLAllocStmt function [ODBC], mapping
ms.assetid: a2449dbb-1b6c-4b49-81b9-ebdddd4442fd
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 330c245d8b5839fd8a721a7399a22edea78a2417
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47819965"
---
# <a name="sqlallocstmt-mapping"></a>SQLAllocStmt 映射
当应用程序调用**SQLAllocStmt**通过 ODBC 3 *.x*驱动程序，将会调用：  
  
```  
SQLAllocStmt(hdbc, phstmt)  
```  
  
 映射到**SQLAllocHandle**由驱动程序管理器中的驱动程序，如下所示：  
  
```  
SQLAllocHandle(SQL_HANDLE_STMT, InputHandle, OutputHandlePtr)  
```  
  
 与*InputHandle*设置为*hdbc*并*OutputHandlePtr*设置为*phstmt*。
