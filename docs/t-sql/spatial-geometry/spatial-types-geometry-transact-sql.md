---
title: "geometry (TRANSACT-SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- geometry
dev_langs:
- TSQL
helpviewer_keywords:
- spatial data types [SQL Server]
- geometry data type [SQL Server], Transact-SQL
ms.assetid: 3fefdf7b-f931-404c-821c-82c0375eaf51
caps.latest.revision: 20
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 2ba0303292df8bb8610831594393f6ec3072b5f3
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="spatial-types---geometry-transact-sql"></a>空间类型的几何图形 (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  平面空间数据类型，**几何图形**，作为公共语言运行时 (CLR) 数据类型中实现[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 此类型表示欧几里得（平面）坐标系中的数据。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]支持的方法的一组**几何图形**空间数据类型。 这些方法包括方法上**几何图形**由开放地理空间联盟 (OGC) 标准和一组定义[!INCLUDE[msCoName](../../includes/msconame-md.md)]该标准的扩展。  
 
 最大为 1.0 e 可以几何图形方法的错误容差-7 * 扩展盘区。 范围，该引用的点之间的近似的最大距离**几何图形**对象。
  
## <a name="registering-the-geometry-type"></a>注册 geometry 类型  
 **geometry** 类型已进行预定义，可在每个数据库中使用。 您可以创建 **geometry** 类型的表列并对 **geometry** 数据进行操作，就像使用其他 CLR 类型一样。 可以用在持久化和非持久化计算列中。  
  
## <a name="examples"></a>示例  
  
### <a name="a-showing-how-to-add-and-query-geometry-data"></a>A. 显示如何添加和查询几何图形数据  
 以下两个示例显示了如何添加和查询几何图形数据。 第一个示例创建包含一个标识列和一个 `geometry` 列 `GeomCol1` 的表。 第三列将 `geometry` 列呈现为其开放地理空间信息联盟 (OGC) 熟知文本 (WKT) 表示形式，并使用 `STAsText()` 方法。 接下来将插入两行：一行包含 `LineString` 类型的 `geometry`实例，一行包含 `Polygon` 实例。  
  
```tsql 
IF OBJECT_ID ( 'dbo.SpatialTable', 'U' ) IS NOT NULL   
    DROP TABLE dbo.SpatialTable;  
GO  
  
CREATE TABLE SpatialTable   
    ( id int IDENTITY (1,1),  
    GeomCol1 geometry,   
    GeomCol2 AS GeomCol1.STAsText() );  
GO  
  
INSERT INTO SpatialTable (GeomCol1)  
VALUES (geometry::STGeomFromText('LINESTRING (100 100, 20 180, 180 180)', 0));  
  
INSERT INTO SpatialTable (GeomCol1)  
VALUES (geometry::STGeomFromText('POLYGON ((0 0, 150 0, 150 150, 0 150, 0 0))', 0));  
GO  
```  
  
### <a name="b-returning-the-intersection-of-two-geometry-instances"></a>B. 返回两个几何图形实例的交集  
 第二个示例使用 `STIntersection()` 方法返回此前插入的两个 `geometry` 实例相交的点。  
  
```tsql  
DECLARE @geom1 geometry;  
DECLARE @geom2 geometry;  
DECLARE @result geometry;  
  
SELECT @geom1 = GeomCol1 FROM SpatialTable WHERE id = 1;  
SELECT @geom2 = GeomCol1 FROM SpatialTable WHERE id = 2;  
SELECT @result = @geom1.STIntersection(@geom2);  
SELECT @result.STAsText();  
```  
  
### <a name="c-using-geometry-in-a-computed-column"></a>C. 在计算列中使用几何图形数据  
 下面的示例创建一个表与持久化计算的列使用**几何图形**类型。  
  
```tsql  
IF OBJECT_ID ( 'dbo.SpatialTable', 'U' ) IS NOT NULL   
    DROP TABLE dbo.SpatialTable;  
GO  
  
CREATE TABLE SpatialTable  
(  
    locationId int IDENTITY(1,1),  
    location geometry,  
    deliveryArea as location.STBuffer(10) persisted  
)  
```  
  
## <a name="see-also"></a>另请参阅  
  [空间数据 (SQL Server)](../../relational-databases/spatial/spatial-data-sql-server.md)  
  
  
