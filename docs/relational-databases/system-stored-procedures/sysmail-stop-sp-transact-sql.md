---
title: sysmail_stop_sp (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysmail_stop_sp_TSQL
- sysmail_stop_sp
dev_langs:
- TSQL
helpviewer_keywords:
- sysmail_stop_sp
ms.assetid: 045ee36f-5bf0-4626-b5ee-e84db06ce16f
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 254d2f0338361287fd603c3562c3585b30d7ed7b
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47815035"
---
# <a name="sysmailstopsp-transact-sql"></a>sysmail_stop_sp (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  通过停止外部程序所用的 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 对象来停止数据库邮件。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sysmail_stop_sp  
```  
  
## <a name="arguments"></a>参数  
 None  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="remarks"></a>备注  
 此存储的过程是在**msdb**数据库。  
  
 此存储过程可停止保留待发消息请求的数据库邮件队列，并对外部程序禁用 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 激活。  
  
 当队列停止后，数据库邮件外部程序将不会处理消息。 通过此存储过程可以停止数据库邮件，以进行故障排除或维护。  
  
 若要启动数据库邮件，请使用**sysmail_start_sp**。 请注意， **sp_send_dbmail**仍会接受邮件时[!INCLUDE[ssSB](../../includes/sssb-md.md)]对象已停止。  
  
> [!NOTE]  
>  此存储过程只停止用于数据库邮件的队列， 它不会停用数据库中的 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 消息传递功能。 此存储过程不会禁用数据库邮件扩展存储过程以减少外围应用。 若要禁用扩展存储的过程，请参阅[Database Mail XPs 选项](../../database-engine/configure-windows/database-mail-xps-server-configuration-option.md)的**sp_configure**系统存储过程。  
  
## <a name="permissions"></a>Permissions  
 执行此过程默认情况下的成员的权限**sysadmin**固定的服务器角色。  
  
## <a name="examples"></a>示例  
 下面的示例演示正在停止数据库邮件**msdb**数据库。 该示例假设数据库邮件已启用。  
  
```  
USE msdb ;  
GO  
  
EXECUTE dbo.sysmail_stop_sp ;  
GO  
```  
  
## <a name="see-also"></a>请参阅  
 [数据库邮件](../../relational-databases/database-mail/database-mail.md)   
 [sysmail_start_sp &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sysmail-start-sp-transact-sql.md)   
 [数据库邮件存储过程&#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/database-mail-stored-procedures-transact-sql.md)  
  
  
