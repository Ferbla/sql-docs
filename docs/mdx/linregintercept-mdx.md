---
description: "LinRegIntercept (MDX)"
title: "LinRegIntercept (MDX) | Microsoft Docs"
ms.date: 02/17/2022
ms.service: sql
ms.subservice: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
---
# LinRegIntercept (MDX)


  Calculates the linear regression of a set and returns the value of the x-intercept in the regression line, y = ax + b.  
  
## Syntax  
  
```  
  
LinRegIntercept(Set_Expression, Numeric_Expression_y [ ,Numeric_Expression_x ] )  
```  
  
## Arguments  
 *Set_Expression*  
 A valid Multidimensional Expressions (MDX) expression that returns a set.  
  
 *Numeric_Expression_y*  
 A valid numeric expression that is typically a Multidimensional Expressions (MDX) expression of cell coordinates that return a number that represents values for the y-axis.  
  
 *Numeric_Expression_x*  
 A valid numeric expression that is typically a Multidimensional Expressions (MDX) expression of cell coordinates that return a number that represents values for the x-axis.  
  
## Remarks  
 Linear regression, that uses the least-squares method, calculates the equation of a regression line (that is, the best-fit line for a series of points). The regression line has the following equation, where a is the slope and b is the intercept:  
  
 y = ax+b  
  
 The **LinRegIntercept** function evaluates the specified set against the first numeric expression to obtain the values for the y-axis. The function then evaluates the specified set against the second numeric expression, if specified, to obtain the values for the x-axis. If the second numeric expression is not specified, the function uses the current context of the cells in the specified set as values for the x-axis. Not specifying the x-axis argument is frequently used with the Time dimension.  
  
 After obtaining the set of points, the **LinRegIntercept** function returns the intercept of the regression line (b in the previous equation).  
  
> [!NOTE]  
>  The **LinRegIntercept** function ignores empty cells or cells that contain text or logical values. However, the function includes cells with values of zero.  
  
## Example  
 The following example returns the intercept of a regression line for the unit sales and the store sales measures.  
  
```  
LinRegIntercept(LastPeriods(10),[Measures].[Unit Sales],[Measures].[Store Sales])  
```  
  
## See Also  
 [MDX Function Reference &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
