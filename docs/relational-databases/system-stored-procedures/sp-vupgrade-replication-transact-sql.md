---
title: sp_vupgrade_replication (Transact SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology:
- replication
ms.topic: language-reference
f1_keywords:
- sp_vupgrade_replication_TSQL
- sp_vupgrade_replication
helpviewer_keywords:
- sp_vupgrade_replication
ms.assetid: d2c0ed66-07d1-4adc-82e5-a654376879bc
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: e6ece6875e89f684bf0c98f54319e519a648fd84
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47640365"
---
# <a name="spvupgradereplication-transact-sql"></a>sp_vupgrade_replication (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  升级复制服务器时由安装程序激活。 根据需要升级架构和系统数据，以支持当前产品级别上的复制。 在系统和用户数据库中创建新的复制系统对象。 此存储过程在要发生复制升级的计算机上执行。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_vupgrade_replication [ [@login=] 'login' ]  
    [ , [ @password= ] 'password' ]  
    [ , [ @ver_old= ] 'old_version' ]  
    [ , [ @force_remove= ] 'force_removal' ]  
    [ , [ @security_mode= ] security_mode ]  
```  
  
## <a name="arguments"></a>参数  
 [  **@login=**] **'***登录*****  
 在分发数据库中创建新的系统对象时使用的系统管理员登录名。 login 的数据类型为 sysname，默认值为 NULL。 如果不需要此参数*security_mode*设置为**1**，这是 Windows 身份验证。  
  
> [!NOTE]  
>  在升级到 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 和更高版本后将忽略此参数。  
  
 [  **@password=**] **'***密码*****  
 是分发数据库中创建新的系统对象时要使用的系统管理员密码。 *密码*是**sysname**，默认值为 **'** （空字符串）。 如果不需要此参数*security_mode*设置为**1**，这是 Windows 身份验证。  
  
> [!NOTE]  
>  在升级到 SQL [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 和更高版本后将忽略此参数。  
  
 [  **@ver_old=**] **'***old_version*****  
 [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
 不推荐使用此存储过程，在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的未来版本中将删除它。  
  
 [  **@force_remove=**] **'***force_removal*****  
 [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
 [  **@security_mode=**] **'***security_mode*****  
 在分发数据库中创建新的系统对象时要使用的登录安全模式。 *security_mode*是**位**默认值为**0**。 如果**0**，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]将使用身份验证。 如果**1**，将使用 Windows 身份验证。  
  
> [!NOTE]  
>  在升级到 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 和更高版本后将忽略此参数。  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="remarks"></a>备注  
 **sp_vupgrade_replication**用于升级所有类型的复制。  
  
## <a name="permissions"></a>Permissions  
 只有的成员**sysadmin**固定的服务器角色可以执行**sp_vupgrade_replication**。  
  
## <a name="see-also"></a>请参阅  
 [复制存储过程 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)   
 [验证已复制的数据](../../relational-databases/replication/validate-replicated-data.md)  
  
  
