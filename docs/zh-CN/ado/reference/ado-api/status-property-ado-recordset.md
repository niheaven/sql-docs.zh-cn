---
title: 状态属性 （ADO 记录集） |Microsoft 文档
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::GetStatus
- Recordset15::Status
helpviewer_keywords:
- Status property [ADO Recordset]
ms.assetid: 41d70d89-880f-4850-9d17-19d9790cc8eb
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a1a3c09b9613c2fe9bd84ea921aef8a3e09a14b7
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="status-property-ado-recordset"></a>状态属性 （ADO 记录集）
指示相对于批处理更新的当前记录或其他大容量操作的状态。  
  
## <a name="return-value"></a>返回值  
 返回一个或多个总和[RecordStatusEnum](../../../ado/reference/ado-api/recordstatusenum.md)值。  
  
## <a name="remarks"></a>注释  
 使用**状态**属性以查看哪些更改处于挂起状态在批更新期间修改的记录。 你还可以使用**状态**属性以查看在大容量操作，例如，当调用期间失败的记录的状态[重新同步](../../../ado/reference/ado-api/resync-method.md)， [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md)，或[执行](../../../ado/reference/ado-api/cancelbatch-method-ado.md)方法[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)对象，或设置[筛选器](../../../ado/reference/ado-api/filter-property.md)属性**记录集**到数组中的书签的对象。 通过此属性，可以确定如何给定的记录失败 ѕ в ѕ ц。  
  
## <a name="applies-to"></a>适用范围  
 [记录集对象 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>另请参阅  
 [状态属性示例 （记录集） (VB)](../../../ado/reference/ado-api/status-property-example-recordset-vb.md)   
 [State 属性示例 (VC++)](../../../ado/reference/ado-api/status-property-example-vc.md)   