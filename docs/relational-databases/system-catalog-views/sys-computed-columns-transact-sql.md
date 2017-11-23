---
title: "sys.computed_columns (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.computed_columns_TSQL
- sys.computed_columns
- computed_columns_TSQL
- computed_columns
dev_langs: TSQL
helpviewer_keywords: sys.computed_columns catalog view
ms.assetid: c962c619-e18f-4315-9251-8d9862462299
caps.latest.revision: "48"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: d8614fe85f562c9b3ffdbbb10e5451464564b9e2
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2017
---
# <a name="syscomputedcolumns-transact-sql"></a>sys.computed_columns (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  有关每个列在表中占一行**sys.columns** ，它是一个计算列。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**\<继承列 >**||**Sys.computed_columns**视图返回中的所有列**sys.columns**视图。 它还返回如下所述的其他列。 有关列的说明， **sys.computed_columns**视图继承自**sys.columns**，请参阅[sys.columns &#40;Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-columns-transact-sql.md). 值**is_computed**列始终设置为 1 **sys.computed_columns**视图。|  
|**定义**|**nvarchar(max)**|定义该计算列的 SQL 文本。|  
|**uses_database_collation**|**bit**|1 = 列定义依赖数据库的默认排序规则进行正确计算；否则为 0。 这种相关性可防止更改数据库默认排序规则。|  
|**is_persisted**|**bit**|计算列是持久化的。|  
  
## <a name="permissions"></a>Permissions  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 有关详细信息，请参阅 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  
  
## <a name="see-also"></a>另请参阅  
 [对象目录视图 &#40;Transact SQL &#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [目录视图 (Transact-SQL)](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  