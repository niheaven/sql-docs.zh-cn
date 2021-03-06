---
title: 从存储过程返回数据 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.technology: stored-procedures
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- stored procedures [SQL Server], returning data
- returning data from stored procedure
ms.assetid: 7a428ffe-cd87-4f42-b3f1-d26aa8312bf7
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 6b11f924ce5692378896f1fd7d50186861abf223
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48220527"
---
# <a name="return-data-from-a-stored-procedure"></a>从存储过程中返回数据
  有两种方法可以将结果集或数据从过程返回给调用程序：输出参数和返回代码。 本主题提供了有关这两种方法的信息。  
  
## <a name="returning-data-using-an-output-parameter"></a>使用输出参数返回数据  
 如果在过程定义中为参数指定 OUTPUT 关键字，则过程在退出时可将该参数的当前值返回给调用程序。 若要将参数值保存在可在调用程序中使用的变量中，调用程序在执行过程时必须使用 OUTPUT 关键字。 有关可用作输出参数的数据类型的详细信息，请参阅 [CREATE PROCEDURE (Transact-SQL)](/sql/t-sql/statements/create-procedure-transact-sql)。  
  
### <a name="examples-of-output-parameter"></a>输出参数的示例  
 以下示例显示有一个输入参数和一个输出参数的过程。 `@SalesPerson` 参数将接收由调用程序指定的输入值。 SELECT 语句使用传递给输入参数的值来获取正确的 `SalesYTD` 值。 SELECT 语句还将该值赋给 `@SalesYTD` 输出参数，该参数在过程退出时将值返回给调用程序。  
  
```  
USE AdventureWorks2012;  
GO  
IF OBJECT_ID('Sales.uspGetEmployeeSalesYTD', 'P') IS NOT NULL  
    DROP PROCEDURE Sales.uspGetEmployeeSalesYTD;  
GO  
CREATE PROCEDURE Sales.uspGetEmployeeSalesYTD  
@SalesPerson nvarchar(50),  
@SalesYTD money OUTPUT  
AS    
  
    SET NOCOUNT ON;  
    SELECT @SalesYTD = SalesYTD  
    FROM Sales.SalesPerson AS sp  
    JOIN HumanResources.vEmployee AS e ON e.BusinessEntityID = sp.BusinessEntityID  
    WHERE LastName = @SalesPerson;  
RETURN  
GO  
  
```  
  
 以下示例调用在第一个示例中创建的过程并将从调用的过程返回的输出值保存在 `@SalesYTD` 变量中，该变量是调用程序的局部变量。  
  
```  
-- Declare the variable to receive the output value of the procedure.  
DECLARE @SalesYTDBySalesPerson money;  
-- Execute the procedure specifying a last name for the input parameter  
-- and saving the output value in the variable @SalesYTDBySalesPerson  
EXECUTE Sales.uspGetEmployeeSalesYTD  
    N'Blythe', @SalesYTD = @SalesYTDBySalesPerson OUTPUT;  
-- Display the value returned by the procedure.  
PRINT 'Year-to-date sales for this employee is ' +   
    convert(varchar(10),@SalesYTDBySalesPerson);  
GO  
  
```  
  
 也可以在执行过程时为 OUTPUT 参数指定输入值。 这将允许过程从调用程序接收值，使用该值更改或执行操作，然后将新值返回给调用程序。 在上一个示例中，可以在程序调用 `@SalesYTDBySalesPerson` 过程前为 `Sales.uspGetEmployeeSalesYTD` 变量赋值。 execute 语句将 `@SalesYTDBySalesPerson` 变量值传递给 `@SalesYTD` OUTPUT 参数。 然后，在过程主体中，可以将该值用于生成新值的计算。 新值可以通过 OUTPUT 参数重新从过程传回，在过程退出时更新 `@SalesYTDBySalesPerson` 变量的值。 这常常被称作“传址调用功能”。  
  
 如果在调用过程时为参数指定 OUTPUT，而在过程定义中该参数又不是用 OUTPUT 定义的，那么将收到一条错误消息。 但是，在执行过程时，可以执行带有输出参数的过程而不指定 OUTPUT。 这样不会返回错误，但将无法在调用程序中使用输出值。  
  
### <a name="using-the-cursor-data-type-in-output-parameters"></a>在 OUTPUT 参数中使用 cursor 数据类型  
 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 可以使用过程`cursor`数据类型用于 OUTPUT 参数。 如果`cursor`数据类型指定为参数，则必须为过程定义中该参数指定 VARYING 和 OUTPUT 关键字。 可以将参数指定为仅限 OUTPUT，但如果在参数声明中指定了 VARYING 关键字，则数据类型必须为`cursor`，并且还必须指定 OUTPUT 关键字。  
  
> [!NOTE]  
>  `cursor`数据类型不能绑定到通过数据库 Api，如 OLE DB、 ODBC、 ADO 和 Db-library 应用程序变量。 因为必须绑定 OUTPUT 参数，应用程序可以执行的过程，过程与之前`cursor`输出参数不能从数据库 Api 调用。 可以从调用这些过程[!INCLUDE[tsql](../../../includes/tsql-md.md)]批处理、 过程或触发器时，才`cursor`OUTPUT 变量分配给[!INCLUDE[tsql](../../../includes/tsql-md.md)]本地`cursor`变量。  
  
### <a name="rules-for-cursor-output-parameters"></a>cursor 输出参数的规则  
 以下规则适用于`cursor`时执行该过程输出参数：  
  
-   对于只进游标，游标的结果集中返回的行只是那些过程执行结束时处于或超出游标位置的行，例如：  
  
    -   在过程中的名为 RS 的 100 行结果集上打开一个非滚动游标。  
  
    -   过程提取结果集 RS 的头 5 行。  
  
    -   过程返回到其调用者。  
  
    -   返回到调用者的结果集 RS 由 RS 的第 6 到 100 行组成，调用者中的游标处于 RS 的第一行之前。  
  
-   对于只进游标，如果过程退出时游标位于第一行的前面，则整个结果集将返回给调用批处理、过程或触发器。 返回时，游标将位于第一行的前面。  
  
-   对于只进游标，如果过程退出时游标的位置超出最后一行的结尾，则为调用批处理、过程或触发器返回空结果集。  
  
    > [!NOTE]  
    >  空结果集与空值不同。  
  
-   对于可滚动游标，在过程退出时，结果集中的所有行均会返回给调用批处理、过程或触发器。 返回时，游标保留在过程中最后一次执行提取时的位置。  
  
-   对于任意类型的游标，如果游标关闭，则将 Null 值传递回调用批处理、过程或触发器。 如果将游标指派给一个参数，但该游标从未打开过，也会出现这种情况。  
  
    > [!NOTE]  
    >  关闭状态只有在返回时才有影响。 例如，可以在过程中关闭游标，稍后再打开游标，然后将该游标的结果集返回给调用批处理、过程或触发器。  
  
### <a name="examples-of-cursor-output-parameters"></a>cursor 输出参数的示例  
 在以下示例中，创建过程的指定输出参数， `@currency`_`cursor`使用`cursor`数据类型。 然后在批处理中调用该过程。  
  
 首先，创建以下过程，在 Currency 表上声明并打开一个游标。  
  
```  
USE AdventureWorks2012;  
GO  
IF OBJECT_ID ( 'dbo.uspCurrencyCursor', 'P' ) IS NOT NULL  
    DROP PROCEDURE dbo.uspCurrencyCursor;  
GO  
CREATE PROCEDURE dbo.uspCurrencyCursor   
    @CurrencyCursor CURSOR VARYING OUTPUT  
AS  
    SET NOCOUNT ON;  
    SET @CurrencyCursor = CURSOR  
    FORWARD_ONLY STATIC FOR  
      SELECT CurrencyCode, Name  
      FROM Sales.Currency;  
    OPEN @CurrencyCursor;  
GO  
  
```  
  
 接下来，执行一个批处理，声明一个局部游标变量，执行上述过程以将游标赋值给局部变量，然后从该游标提取行。  
  
```  
USE AdventureWorks2012;  
GO  
DECLARE @MyCursor CURSOR;  
EXEC dbo.uspCurrencyCursor @CurrencyCursor = @MyCursor OUTPUT;  
WHILE (@@FETCH_STATUS = 0)  
BEGIN;  
     FETCH NEXT FROM @MyCursor;  
END;  
CLOSE @MyCursor;  
DEALLOCATE @MyCursor;  
GO  
  
```  
  
## <a name="returning-data-using-a-return-code"></a>使用返回代码返回数据  
 过程可以返回一个整数值（称为“返回代码”），以指示过程的执行状态。 使用 RETURN 语句指定过程的返回代码。 与 OUTPUT 参数一样，执行过程时必须将返回代码保存到变量中，才能在调用程序中使用返回代码值。 例如，赋值变量`@result`的数据类型`int`用于存储过程的返回代码`my_proc`，如：  
  
```  
DECLARE @result int;  
EXECUTE @result = my_proc;  
```  
  
 返回代码通常用在过程内的控制流块中，以便为每种可能的错误情况设置返回代码值。 可以在 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 语句后使用 @@ERROR 函数，来检测该语句执行过程中是否有错误发生。  
  
### <a name="examples-of-return-codes"></a>返回代码的示例  
 下面的示例显示了带有错误处理设置（为各种错误设置特殊返回代码值）的 `usp_GetSalesYTD` 过程。 下表显示了由过程分配给每个可能错误的整数值，以及每个值的相应含义。  
  
|返回代码值|含义|  
|-----------------------|-------------|  
|0|成功执行。|  
|1|未指定所需参数值。|  
|2|指定参数值无效。|  
|3|获取销售额数值时出错。|  
|4|该销售人员的销售额数值为 NULL。|  
  
```  
USE AdventureWorks2012;  
GO  
IF OBJECT_ID('Sales.usp_GetSalesYTD', 'P') IS NOT NULL  
    DROP PROCEDURE Sales.usp_GetSalesYTD;  
GO  
CREATE PROCEDURE Sales.usp_GetSalesYTD  
@SalesPerson nvarchar(50) = NULL,  -- NULL default value  
@SalesYTD money = NULL OUTPUT  
AS    
  
-- Validate the @SalesPerson parameter.  
IF @SalesPerson IS NULL  
   BEGIN  
       PRINT 'ERROR: You must specify a last name for the sales person.'  
       RETURN(1)  
   END  
ELSE  
   BEGIN  
   -- Make sure the value is valid.  
   IF (SELECT COUNT(*) FROM HumanResources.vEmployee  
          WHERE LastName = @SalesPerson) = 0  
      RETURN(2)  
   END  
-- Get the sales for the specified name and   
-- assign it to the output parameter.  
SELECT @SalesYTD = SalesYTD   
FROM Sales.SalesPerson AS sp  
JOIN HumanResources.vEmployee AS e ON e.BusinessEntityID = sp.BusinessEntityID  
WHERE LastName = @SalesPerson;  
-- Check for SQL Server errors.  
IF @@ERROR <> 0   
   BEGIN  
      RETURN(3)  
   END  
ELSE  
   BEGIN  
   -- Check to see if the ytd_sales value is NULL.  
     IF @SalesYTD IS NULL  
       RETURN(4)   
     ELSE  
      -- SUCCESS!!  
        RETURN(0)  
   END  
-- Run the stored procedure without specifying an input value.  
EXEC Sales.usp_GetSalesYTD;  
GO  
-- Run the stored procedure with an input value.  
DECLARE @SalesYTDForSalesPerson money, @ret_code int;  
-- Execute the procedure specifying a last name for the input parameter  
-- and saving the output value in the variable @SalesYTD  
EXECUTE Sales.usp_GetSalesYTD  
    N'Blythe', @SalesYTD = @SalesYTDForSalesPerson OUTPUT;  
PRINT N'Year-to-date sales for this employee is ' +  
    CONVERT(varchar(10), @SalesYTDForSalesPerson);  
  
```  
  
 下面的示例创建了处理从 `usp_GetSalesYTD` 过程返回的返回代码的程序。  
  
```  
-- Declare the variables to receive the output value and return code   
-- of the procedure.  
DECLARE @SalesYTDForSalesPerson money, @ret_code int;  
  
-- Execute the procedure with a title_id value  
-- and save the output value and return code in variables.  
EXECUTE @ret_code = Sales.usp_GetSalesYTD  
    N'Blythe', @SalesYTD = @SalesYTDForSalesPerson OUTPUT;  
--  Check the return codes.  
IF @ret_code = 0  
BEGIN  
   PRINT 'Procedure executed successfully'  
   -- Display the value returned by the procedure.  
   PRINT 'Year-to-date sales for this employee is ' + CONVERT(varchar(10),@SalesYTDForSalesPerson)  
END  
ELSE IF @ret_code = 1  
   PRINT 'ERROR: You must specify a last name for the sales person.'  
ELSE IF @ret_code = 2   
   PRINT 'EERROR: You must enter a valid last name for the sales person.'  
ELSE IF @ret_code = 3  
   PRINT 'ERROR: An error occurred getting sales value.'  
ELSE IF @ret_code = 4  
   PRINT 'ERROR: No sales recorded for this employee.'     
GO  
  
```  
  
## <a name="see-also"></a>请参阅  
 [DECLARE @local_variable (Transact-SQL)](/sql/t-sql/language-elements/declare-local-variable-transact-sql)   
 [PRINT (Transact-SQL)](/sql/t-sql/language-elements/print-transact-sql)   
 [SET @local_variable (Transact-SQL)](/sql/t-sql/language-elements/set-local-variable-transact-sql)   
 [游标](../cursors.md)   
 [RETURN (Transact-SQL)](/sql/t-sql/language-elements/return-transact-sql)   
 [@@ERROR (Transact-SQL)](/sql/t-sql/functions/error-transact-sql)  
  
  
