---
description: "sp_replmonitorhelppublisher (Transact-SQL)"
title: "sp_replmonitorhelppublisher (Transact-SQL) | Microsoft Docs"
ms.custom: ""
ms.date: "03/04/2017"
ms.service: sql
ms.reviewer: ""
ms.subservice: replication
ms.topic: "reference"
dev_langs: 
  - "TSQL"
f1_keywords: 
  - "sp_replmonitorhelppublisher_TSQL"
  - "sp_replmonitorhelppublisher"
helpviewer_keywords: 
  - "sp_replmonitorhelppublisher"
ms.assetid: 171501fe-4b74-4647-96c3-7691c777e01b
author: markingmyname
ms.author: maghan
---
# sp_replmonitorhelppublisher (Transact-SQL)
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

  Returns current status information for one or more Publishers associated with a Distributor. This stored procedure, which is used to monitor replication, is executed at the Distributor on the distribution database.  
  
 ![Topic link icon](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## Syntax  
  
```  
  
sp_replmonitorhelppublisher [ [ @publisher = ] 'publisher' ]  
    [ , [ @refreshpolicy = ] refreshpolicy ]  
```  
  
## Arguments  
`[ @publisher = ] 'publisher'`
 Is the name of the Publisher the status of which is being monitored. *publisher* is **sysname**, with a default value of NULL. If NULL, information will be returned for all Publishers that use the Distributor.  
  
`[ @refreshpolicy = ] refreshpolicy`
 Internal use only.  
  
## Result Sets  
  
|Column name|Data type|Description|  
|-----------------|---------------|-----------------|  
|**publisher**|**sysname**|Is the name of a Publisher.|  
|**distribution_db**|**sysname**|Is the name of the distribution database used by a given Publisher.|  
|**status**|**int**|Maximum status of all replication agents associated with publications at this Publisher, which can be one of these values.<br /><br /> **1** = Started<br /><br /> **2** = Succeeded<br /><br /> **3** = In progress<br /><br /> **4** = Idle<br /><br /> **5** = Retrying<br /><br /> **6** = Failed|  
|**warning**|**int**|Maximum threshold warning generated by a subscription belonging to a publication at this Publisher, which can be the logical OR result of one or more of these values.<br /><br /> **1** = expiration - a subscription to a transactional publication has not been synchronized within the retention period threshold.<br /><br /> **2** = latency - the time taken to replicate data from a transactional Publisher to the Subscriber exceeds the threshold, in seconds.<br /><br /> **4** = mergeexpiration - a subscription to a merge publication has not been synchronized within the retention period threshold.<br /><br /> **8** = mergefastrunduration - the time taken to complete synchronization of a merge subscription exceeds the threshold, in seconds, over a fast network connection.<br /><br /> **16** = mergeslowrunduration - the time taken to complete synchronization of a merge subscription exceeds the threshold, in seconds, over a slow or dial-up network connection.<br /><br /> **32** = mergefastrunspeed - the delivery rate for rows during synchronization of a merge subscription has failed to maintain the threshold rate, in rows per second, over a fast network connection.<br /><br /> **64** = mergeslowrunspeed - the delivery rate for rows during synchronization of a merge subscription has failed to maintain the threshold rate, in rows per second, over a slow or dial-up network connection.|  
|**publicationcount**|**int**|Is the number of publications belonging to the Publisher.|  
  
## Return Code Values  
 **0** (success) or **1** (failure)  
  
## Remarks  
 **sp_replmonitorhelppublisher** is used with all types of replication.  
  
## Permissions  
 Only members of the **sysadmin** fixed server role at the Distributor or members of the **db_owner** or **replmonitor** fixed database roles in the distribution database can execute **sp_replmonitorhelppublisher**.  
  
## See Also  
 [Programmatically Monitor Replication](../../relational-databases/replication/monitor/programmatically-monitor-replication.md)  
  
  
