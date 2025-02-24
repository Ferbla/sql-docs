---
description: "sp_addextendedproc (Transact-SQL)"
title: "sp_addextendedproc (Transact-SQL) | Microsoft Docs"
ms.custom: ""
ms.date: "03/16/2017"
ms.service: sql
ms.reviewer: ""
ms.subservice: system-objects
ms.topic: "reference"
f1_keywords: 
  - "sp_addextendedproc_TSQL"
  - "sp_addextendedproc"
dev_langs: 
  - "TSQL"
helpviewer_keywords: 
  - "sp_addextendedproc"
ms.assetid: c0d4b47b-a855-451e-90e5-5fb2d836ebfa
author: markingmyname
ms.author: maghan
---
# sp_addextendedproc (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Registers the name of a new extended stored procedure to [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
> [!NOTE]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] Use [CLR Integration](../../relational-databases/clr-integration/common-language-runtime-integration-overview.md) instead.  
  
 ![Topic link icon](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## Syntax  
  
```  
  
sp_addextendedproc [ @functname = ] 'procedure' ,   
     [ @dllname = ] 'dll'  
```  
  
## Arguments  
`[ @functname = ] 'procedure'`
 Is the name of the function to call within the dynamic-link library (DLL). *procedure* is **nvarchar(517)**, with no default. *procedure* optionally can include the owner name in the form *owner.function*.  
  
`[ @dllname = ] 'dll'`
 Is the name of the DLL that contains the function. *dll* is **varchar(255)**, with no default. It is recommended that you specify the complete path of the DLL.  
  
## Return Code Values  
 0 (success) or 1 (failure)  
  
## Result Sets  
 None  
  
## Remarks  
 After an extended stored procedure is created, it must be added to [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] by using **sp_addextendedproc**. For more information, see [Adding an Extended Stored Procedure to SQL Server](../../relational-databases/extended-stored-procedures-programming/adding-an-extended-stored-procedure-to-sql-server.md).  
  
 This procedure can be run only in the **master** database. To execute an extended stored procedure from a database other than **master**, qualify the name of the extended stored procedure with **master**.  
  
 **sp_addextendedproc** adds entries to the [sys.objects](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md) catalog view, registering the name of the new extended stored procedure with [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. It also adds an entry in the [sys.extended_procedures](../../relational-databases/system-catalog-views/sys-extended-procedures-transact-sql.md) catalog view.  
  
> [!IMPORTANT]  
>  Existing DLLs that were not registered with a complete path will not work after upgrading to [!INCLUDE [ssnoversion-md](../../includes/ssnoversion-md.md)]. To correct the problem, use **sp_dropextendedproc** to unregister the DLL, and then reregister it with **sp_addextendedproc**, specifying the complete path.  
  
## Permissions  
 Only members of the **sysadmin** fixed server role can execute **sp_addextendedproc**.  
  
## Examples  
 The following example adds the **xp_hello** extended stored procedure.  
  
```  
USE master;  
GO  
EXEC sp_addextendedproc xp_hello, 'c:\xp_hello.dll';  
```  
  
## See Also  
 [EXECUTE &#40;Transact-SQL&#41;](../../t-sql/language-elements/execute-transact-sql.md)   
 [GRANT &#40;Transact-SQL&#41;](../../t-sql/statements/grant-transact-sql.md)   
 [REVOKE &#40;Transact-SQL&#41;](../../t-sql/statements/revoke-transact-sql.md)   
 [sp_dropextendedproc &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropextendedproc-transact-sql.md)   
 [sp_helpextendedproc &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpextendedproc-transact-sql.md)   
 [System Stored Procedures &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
