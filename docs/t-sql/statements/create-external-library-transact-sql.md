---
title: CREATE EXTERNAL LIBRARY (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/05/2018
ms.prod: sql
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- CREATE EXTERNAL LIBRARY
- CREATE_EXTERNAL_LIBRARY_TSQL
- EXTERNAL LIBRARY
- EXTERNAL_LIBRARY_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- CREATE EXTERNAL LIBRARY
author: HeidiSteen
ms.author: heidist
manager: cgronlund
monikerRange: '>=sql-server-2017||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 0e6154611d2579706f3da4f9159e5d1bfce41bb7
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47741125"
---
# <a name="create-external-library-transact-sql"></a>CREATE EXTERNAL LIBRARY (Transact-SQL)  

[!INCLUDE[tsql-appliesto-ss2017-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-xxxx-xxxx-xxx-md.md)]  

将 R 包从指定的字节流或文件路径上传到数据库。

数据库管理员上传任何新的外部语言运行时（R、Python、Java 等）以及 [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)] 支持的操作系统平台所需的项目时，此语句可作为通用机制发挥作用。 

当前仅支持 R 包和 Windows 平台。 计划在之后发布的版本中提供对 Python 和 Linux 的支持。

## <a name="syntax"></a>语法

```text
CREATE EXTERNAL LIBRARY library_name  
    [ AUTHORIZATION owner_name ]  
FROM <file_spec> [,…2]  
WITH ( LANGUAGE = 'R' )  
[ ; ]  

<file_spec> ::=  
{  
(CONTENT = { <client_library_specifier> | <library_bits> }  
[, PLATFORM = WINDOWS ])  
}  

<client_library_specifier> :: =  
  '[\\computer_name\]share_name\[path\]manifest_file_name'  
| '[local_path\]manifest_file_name'  
| '<relative_path_in_external_data_source>'  

<library_bits> :: =  
{ varbinary_literal | varbinary_expression }  
```

### <a name="arguments"></a>参数

**library_name**

将库添加到作用域为该用户的数据库中。 在特定用户或所有者的上下文中，库名称必须是唯一的。 例如，两个用户 RUser1 和 RUser2 可以分别独立上传 R 库 `ggplot2`。 不过，如果 RUser1 要上传新版 `ggplot2`，第二个实例要么必须以不同方式命名，要么必须替换现有库。 

不能随意分配库名称；库名称应与从 R 上传 R 库时所需的名称相同。

**owner_name**

指定拥有外部库的用户或角色的名称。 如果未指定，则所有权授予当前用户。

对于数据库和运行时，数据库所有者所拥有的库均视为全局性的库。 换言之，数据库所有者可以创建库，而这些库包含一组由许多用户共享的公共库或包。 当由用户而不是 `dbo` 用户创建外部库时，该外部库便由该用户专用。

当用户 RUser1 执行 R 脚本时，`libPath` 值可包含多个路径。 第一个路径始终为数据库所有者创建的共享库的路径。 `libPath` 的第二部分指定包含由 RUser1 单独上传的包的路径。

**file_spec**

指定特定平台的包的内容。 每个平台仅支持一个文件项目。

可以是以本地路径或网络路径的形式指定的文件。

还可以为文件指定一个 OS 平台。 针对特定语言或运行时，每个 OS 平台只允许一个文件项目或内容。

**library_bits**

将包的内容指定为十六进制文本，类似于程序集。 

如果需要创建库或更改现有库（并具有执行此操作的所需权限），但服务器上的文件系统受限，无法将库文件复制到服务器可以访问的位置，此选项会非常有用。

**PLATFORM = WINDOWS**

为库的内容指定平台。 该值默认为正在运行 SQL Server 的主机平台。 因此，用户不需要指定该值。 如果支持多个平台或用户需要指定不同的平台，则需要此值。 

在 SQL Server 2017 版本中，Windows 是唯一支持的平台。

## <a name="remarks"></a>Remarks

对于 R 语言，使用文件时，必须使用 Windows 的 .ZIP 扩展名以压缩存档文件的形式准备包。 目前仅支持 Windows 平台。 

`CREATE EXTERNAL LIBRARY` 语句将库位上载到数据库。 当用户使用 [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) 运行外部脚本并调用包或库时，会安装该库。

上传到实例的库可以是公共的也可以是私有的。 如果是由 `dbo` 成员创建的库，则该库是公共的且所有的用户都可以共享。 否则，该库就仅为用户私有。

## <a name="permissions"></a>Permissions

需要 `CREATE EXTERNAL LIBRARY` 权限。 默认情况下，dbo 用户或担任 db_owner 角色的任何成员都有权创建外部库。 对于其他所有用户，必须使用 [GRANT](https://docs.microsoft.com/sql/t-sql/statements/grant-database-permissions-transact-sql) 语句显式授予他们权限，同时将 CREATE EXTERNAL LIBRARY 指定为特权。

更改库需要单独的权限，`ALTER ANY EXTERNAL LIBRARY`。

## <a name="examples"></a>示例

### <a name="a-add-an-external-library-to-a-database"></a>A. 将外部库添加到数据库  

下面的示例将一个名为 `customPackage` 的外部库添加到数据库。

```sql
CREATE EXTERNAL LIBRARY customPackage
FROM (CONTENT = 'C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\customPackage.zip') WITH (LANGUAGE = 'R');
```

在库成功上传到实例之后，用户可执行 `sp_execute_external_script` 步骤来安装库。

```sql
EXEC sp_execute_external_script 
@language =N'R', 
@script=N'library(customPackage)'
```

### <a name="b-installing-packages-with-dependencies"></a>B. 安装具有依赖项的包

如果想要安装的包有任何依赖项，务必要分析第一级和第二级依赖项，并在尝试安装目标包之前，确保所需的所有包都可用。

例如，假设想要安装新包 `packageA`：

+ `packageA` 具有 `packageB` 上的依赖项
+ `packageB` 具有 `packageC` 上的依赖项

若要成功安装 `packageA`，则必须在将 `packageA` 添加到 SQL Server 的同时为 `packageB` 和 `packageC` 创建库。 同时请务必检查所需的包版本。

在实践中，常用包的依赖项通常比简单示例复杂得多。 例如，ggplot2 可能需要超过 30 个包，而这些包可能还需要服务器上没有的其他包。 任何缺少的包或错误的包版本都可能会导致安装失败。

由于仅通过查看程序包清单可能很难确定所有依赖项，因此建议使用 [miniCRAN](https://cran.r-project.org/web/packages/miniCRAN/index.html) 等包，以标识成功完成安装可能需要的所有包。

+ 上传目标包及其依赖项。 所有文件都必须位于服务器可访问的文件夹中。

    ```sql
    CREATE EXTERNAL LIBRARY packageA 
    FROM (CONTENT = 'C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\packageA.zip') 
    WITH (LANGUAGE = 'R'); 
    GO

    CREATE EXTERNAL LIBRARY packageB FROM (CONTENT = 'C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\packageB.zip') 
    WITH (LANGUAGE = 'R');
    GO

    CREATE EXTERNAL LIBRARY packageC FROM (CONTENT = 'C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\packageC.zip') 
    WITH (LANGUAGE = 'R');
    GO
    ```

+ 首先安装所需的包。

    如果所需的包已上传到实例，则不需要再次添加。 请务必检查现有包的版本是否正确。 
    
    第一次运行 `sp_execute_external_script` 以安装包 `packageA` 时，所需的包 `packageC` 和 `packageB` 也会按照正确的顺序安装。

    但是，如果所需的包均不可用，则安装目标包 `packageA` 时会失败。

    ```sql
    EXEC sp_execute_external_script 
    @language =N'R', 
    @script=N'
    # load the desired package packageA
    library(packageA)
    print(packageVersion("packageA"))
    '
    ```

### <a name="c-create-a-library-from-a-byte-stream"></a>C. 从字节流创建库

如果无法将包文件保存到服务器上的某个位置，可以在变量中传递包内容。 下面的示例通过将位传递为十六进制文本来创建库。

```SQL
CREATE EXTERNAL LIBRARY customLibrary FROM (CONTENT = 0xabc123) WITH (LANGUAGE = 'R');
```

> [!NOTE]
> 此代码示例只用于展示语法；为了提高可读性，`CONTENT =` 中的二进制值已遭截断，无法创建能够正常运行的库。 二进制变量的实际内容要长得多。

### <a name="d-change-an-existing-package-library"></a>D. 更改现有包库

`ALTER EXTERNAL LIBRARY` DDL 语句可用于向新库添加内容或更改现有库的内容。 修改现有库需要 `ALTER ANY EXTERNAL LIBRARY` 权限。

有关详细信息，请参阅 [ALTER EXTERNAL LIBRARY](alter-external-library-transact-sql.md)。

## <a name="see-also"></a>另请参阅

[ALTER EXTERNAL LIBRARY (Transact-SQL)](alter-external-library-transact-sql.md)  
[DROP EXTERNAL LIBRARY (Transact-SQL)](drop-external-library-transact-sql.md)  
[sys.external_library_files](../../relational-databases/system-catalog-views/sys-external-library-files-transact-sql.md)  
[sys.external_libraries](../../relational-databases/system-catalog-views/sys-external-libraries-transact-sql.md)  
