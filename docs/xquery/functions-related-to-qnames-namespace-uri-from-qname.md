---
title: 命名空间的 uri-从的 QName (XQuery) |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- fn:namespace-uri-from-QName function
- namespace-uri-from-QName function
ms.assetid: 4ab3f003-2a3b-4268-9e88-b615e35701b2
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: ff8783eee040064e016becebc64e041e1dca4ce0
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47808065"
---
# <a name="functions-related-to-qnames---namespace-uri-from-qname"></a>与 QName 相关的函数 - namespace-uri-from-QName
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  返回一个字符串，表示指定的 QName 的命名空间 uri *$arg*。 如果，则结果为空序列 *$arg*是空序列。  
  
## <a name="syntax"></a>语法  
  
```  
namespace-uri-from-QName($arg as xs:QName?) as xs:string?  
```  
  
## <a name="arguments"></a>参数  
 *$arg*  
 是返回其命名空间 URI 的 QName。  
  
## <a name="examples"></a>示例  
 本主题提供了一些针对 XML 实例存储在各种中的 XQuery 示例**xml**类型列中的 AdventureWorks 数据库。  
  
### <a name="a-retrieve-the-namespace-uri-from-a-qname"></a>A. 检索 QName 的命名空间 URI  
 有关工作示例，请参阅[本地名称从 QName &#40;XQuery&#41;](../xquery/functions-related-to-qnames-local-name-from-qname.md)。  
  
### <a name="implementation-limitations"></a>实现限制  
 限制如下：  
  
-   **Namespace-uri-from-qname （)** 函数将返回而不是 xs: anyuri xs: string 的实例。  
  
## <a name="see-also"></a>请参阅  
 [与 Qname 相关的函数&#40;XQuery&#41;](http://msdn.microsoft.com/library/7e07eb26-f551-4b63-ab77-861684faff71)  
  
  
