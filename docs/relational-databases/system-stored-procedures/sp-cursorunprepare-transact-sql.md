---
description: "sp_cursorunprepare (Transact-SQL)"
title: "sp_cursorunprepare (Transact-SQL) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.service: sql
ms.reviewer: ""
ms.subservice: system-objects
ms.topic: "reference"
f1_keywords: 
  - "sp_cursorunprepare_TSQL"
  - "sp_cursorunprepare"
dev_langs: 
  - "TSQL"
helpviewer_keywords: 
  - "sp_cursorunprepare"
ms.assetid: b46d4813-c4a9-4f9d-9979-2b5082ecf06a
author: markingmyname
ms.author: maghan
---
# sp_cursorunprepare (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Discards the execution plan developed in the sp_cursorprepare stored procedure. sp_cursorunprepare is invoked by specifying ID = 6 in a tabular data stream (TDS) packet.  
  
 ![Topic link icon](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## Syntax  
  
```  
  
sp_cursorunprepare handle  
```  
  
## Arguments  
 *handle*  
 Is the *handle* value that is returned by sp_cursorprepare when the statement is prepared.  
  
## See Also  
 [sp_cursorprepare &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-cursorprepare-transact-sql.md)   
 [System Stored Procedures &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
