---
title: "了解同步和异步转换 |Microsoft 文档"
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- transformations [Integration Services], synchronous and asynchronous
- asynchronous transformations [Integration Services]
- data flow components [Integration Services], synchronous and asynchronous
- synchronous transformations [Integration Services]
ms.assetid: 0bc2bda5-3f8a-49c2-aaf1-01dbe4c3ebba
caps.latest.revision: 17
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 9cc38505042dadb1b057a737279be82bb7923432
ms.contentlocale: zh-cn
ms.lasthandoff: 09/26/2017

---
# <a name="understanding-synchronous-and-asynchronous-transformations"></a>了解同步和异步转换
  若要了解 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 中同步转换与异步转换之间的区别，最好先了解同步转换。 如果同步转换无法满足您的需要，您的设计可能需要异步转换。  
  
## <a name="synchronous-transformations"></a>同步转换  
 同步转换以一次一行的方式处理传入行并在数据流中传递它们。 输出与输入同步，这意味着输出与输入同时发生。 因此，若要处理一个给定行，转换不需要数据集中其他行的信息。 在实际实现中，行在从一个组件传递到下一个组件时分组到多个缓冲区中，但是这些缓冲区对于用户是透明的，您可以假定每一行都单独进行处理。  
  
 “数据转换”这种转换是同步转换的一个示例。 对于每个传入行，它都转换指定列中的值，然后将其向下游发送。 每个单独的转换操作都与数据集中的其他所有行无关。  
  
 在[!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]脚本和编程，你通过查阅组件的输入 ID，并将其分配给指定同步转换**SynchronousInputID**的组件的输出的属性。 这可以使数据流引擎处理输入中的每一行，然后自动将每行发送给指定输出。 如果希望每一行都产生一个输出，则不必再编写任何其他代码来输出数据。 如果你使用**ExclusionGroup**属性来指定行应仅转到一个或另一组的输出，如在有条件拆分转换中，必须调用**DirectRow**方法来选择每个行的适当的目标。 当你有一个错误输出时，必须调用**DirectErrorRow**将有问题的行发送到错误输出，而不是默认输出。  
  
## <a name="asynchronous-transformations"></a>异步转换  
 如果处理每一行时无法独立于其他所有行，则您的设计可能需要异步转换。 换言之，您不能在处理每一行时在数据流中传递该行，而必须使输出数据与输入异步，即两者不同时发生。 例如，以下情况需要异步转换：  
  
-   组件必须获得多个数据缓冲区后才能执行处理。 例如排序转换，在该转换中，组件必须在一个操作中处理整个行集。  
  
-   组件必须组合多个输入中的行。 例如合并转换，在该转换中，组件必须检查来自各个输入的多个行，然后按照排列好的顺序将这些行合并。  
  
-   在输入行和输出行之间不存在一对一的对应关系。 例如聚合转换，在该转换中，组件必须向输出添加一行来保存计算的聚合值。  
  
 在[!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]脚本和编程，你指定异步转换通过分配值为 0 到**SynchronousInputID**的组件的输出的属性。 实例时都提供 SQL Server 登录名。 这可以使数据流引擎不自动将每一行发送到输出中。 这样，您就必须编写代码将每一行显式发送到相应的输出中，方法是将该行添加到为异步转换的输出创建的新输出缓冲区中。  
  
> [!NOTE]  
>  由于源组件也必须显式将从数据源读取的每一行添加到该组件的输出缓冲区中，因此源与具有异步输出的转换很相似。  
  
 还可以创建一个模拟同步转换的异步转换，方法是显式将每个输入行复制到输出中。 使用此方法可以重命名列或者转换数据类型或格式。 但是，此方法会降低性能。 您可以使用内置 Integration Services 组件（如复制列或数据转换）达到同样的效果，但是性能更佳。  
  
## <a name="see-also"></a>另请参阅  
 [使用脚本组件创建同步转换](../integration-services/extending-packages-scripting-data-flow-script-component-types/creating-a-synchronous-transformation-with-the-script-component.md)   
 [使用脚本组件创建异步转换](../integration-services/extending-packages-scripting-data-flow-script-component-types/creating-an-asynchronous-transformation-with-the-script-component.md)   
 [开发具有同步输出的自定义转换组件](../integration-services/extending-packages-custom-objects-data-flow-types/developing-a-custom-transformation-component-with-synchronous-outputs.md)   
 [开发具有异步输出的自定义转换组件](../integration-services/extending-packages-custom-objects-data-flow-types/developing-a-custom-transformation-component-with-asynchronous-outputs.md)  
  
  