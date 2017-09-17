---
title: "ADORecordsetConstruction 接口 |Microsoft 文档"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- ADORecordsetConstruction
helpviewer_keywords:
- ADORecordsetConstruction interface [ADO]
ms.assetid: 08386eba-f1f7-4879-8ffd-8733930ecb2f
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 3da6260d5e0d4e503dae54e6ffc13f6d35f1890d
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="adorecordsetconstruction-interface"></a>ADORecordsetConstruction 接口
**ADORecordsetConstruction**接口用于构造 ADO**记录集**从 OLE DB 对象**行集**C/c + + 应用程序中的对象。  
  
 此接口支持下列属性：  
  
## <a name="properties"></a>属性  
  
|||  
|-|-|  
|[章](../../../ado/reference/ado-api/chapter-property-ado.md)|读/写。<br />获取/设置 OLE DB**章**对象从/上此 ADO**记录集**对象。|  
|[RowPosition](../../../ado/reference/ado-api/rowposition-property-ado.md)|读/写。<br />获取/设置 OLE DB **RowPosition**对象从/上此 ADO**记录集**对象。|  
|[行集](../../../ado/reference/ado-api/rowset-property-ado.md)|读/写。<br />获取/设置 OLE DB**行集**对象从/上此 ADO**记录集**对象。|  
  
## <a name="methods"></a>方法  
 无。  
  
## <a name="events"></a>事件  
 无。  
  
## <a name="remarks"></a>注释  
 提供 OLE DB**行集**对象 (`pRowset`)，构造的 ADO**记录集**对象 (`adoRs`) 都可对以下三个基本操作：  
  
1.  创建 ADO**记录集**对象：  
  
    ```  
    Recordset20Ptr adoRs;  
    adoRs.CreateInstance(__uuidof(Recordset));  
    ```  
  
2.  查询**IADORecordsetConstruction**接口**记录集**对象：  
  
    ```  
    adoRecordsetConstructionPtr adoRsConstruct=NULL;  
    adoRs->QueryInterface(__uuidof(ADORecordsetConstruction),  
                         (void**)&adoRsConstruct);  
    ```  
  
3.  调用`IADORecordsetConstruction::put_Rowset`属性方法以设置 OLE DB`Rowset`上 ADO 对象`Recordset`对象：  
  
    ```  
    IUnknown *pUnk=NULL;  
    pRowset->QueryInterface(IID_IUnknown, (void**)&pUnk);  
    adoRsConstruct->put_Rowset(pUnk);  
    ```  
  
 所产生的`adoRs`对象现在表示 ADO**记录集**构造从 OLE DB 对象**行集**对象。  
  
 你还可以构造 ADO**记录集**从 OLE DB 对象**章**或**RowPosition**对象。  
  
## <a name="requirements"></a>要求  
 **版本：** ADO 2.0 及更高版本  
  
 **库：** msado15.dll  
  
 **UUID:** 00000283-0000-0010-8000-00AA006D2EA4  
  
## <a name="see-also"></a>另请参阅  
 [记录集对象 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)   
 [行集属性 (ADO)](../../../ado/reference/ado-api/rowset-property-ado.md)