---
title: 'Pdostatement:: Closecursor |Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 8997ab61-e948-4d54-8d32-fc080d55525c
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 94fc874de4136d2eb078711b135a291425b6ddb8
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47682537"
---
# <a name="pdostatementclosecursor"></a>PDOStatement::closeCursor
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

关闭游标，此时将再次执行语句。  
  
## <a name="syntax"></a>语法  
  
```  
  
bool PDOStatement::closeCursor();  
```  
  
## <a name="return-value"></a>返回值  
如果成功，则为 true；否则为 false。  
  
## <a name="remarks"></a>Remarks  
当 MultipleActiveResultSets 连接选项设置为 false 时，closeCursor 将起作用。  有关 MultipleActiveResultSets 连接选项的详细信息，请参阅[如何：禁用多个活动的结果集 (MARS)](../../connect/php/how-to-disable-multiple-active-resultsets-mars.md)。  
  
也可以只将语句句柄设置为 null，而不是调用 closeCursor。  
  
已在 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]的版本 2.0 中添加了对 PDO 的支持。  
  
## <a name="example"></a>示例  
  
```  
<?php  
$database = "AdventureWorks";  
$server = "(local)";  
$conn = new PDO( "sqlsrv:server=$server ; Database = $database", "", "", array('MultipleActiveResultSets' => false ) );  
  
$stmt = $conn->prepare('SELECT * FROM Person.ContactType');  
  
$stmt2 = $conn->prepare('SELECT * FROM HumanResources.Department');  
  
$stmt->execute();  
  
$result = $stmt->fetch();  
print_r($result);  
  
$stmt->closeCursor();  
  
$stmt2->execute();  
$result = $stmt2->fetch();  
print_r($result);  
?>  
```  
  
## <a name="see-also"></a>另请参阅  
[PDOStatement 类](../../connect/php/pdostatement-class.md)

[PDO](http://php.net/manual/book.pdo.php)  
  
