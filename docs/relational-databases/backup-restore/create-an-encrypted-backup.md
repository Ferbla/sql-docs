---
title: "Create an Encrypted Backup | Microsoft Docs"
description: This article shows you how to create an encrypted backup in SQL Server using Transact-SQL. You can back up to disk or to Azure Storage.
ms.custom: ""
ms.date: "08/04/2016"
ms.service: sql
ms.reviewer: ""
ms.subservice: backup-restore
ms.topic: conceptual
ms.assetid: e29061d3-c2ab-4d98-b9be-8e90a11d17fe
author: MashaMSFT
ms.author: mathoma
---
# Create an Encrypted Backup
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  This topic describes the steps necessary to create an encrypted backup using Transact-SQL.  For an example using [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], see [Create a Full Database Backup (SQL Server)](../../relational-databases/backup-restore/create-a-full-database-backup-sql-server.md). 
  
## Backup to Disk with Encryption  
 **Prerequisites:**  
  
-   Access to a local disk or to storage with adequate space to create a backup of the database.  
  
-   A Database Master Key for the master database, and a certificate or asymmetric key available on the instance of SQL Server. For encryption requirements and permissions, see [Backup Encryption](../../relational-databases/backup-restore/backup-encryption.md).  
  
 Use the following steps to create an encrypted backup of a database to a local disk. This example uses a user database called MyTestDB.  
  
1.  **Create a Database Master Key of the master database:** Choose a password for encrypting the copy of the master key that will be stored in the database. Connect to the database engine, start a new query windows and copy and paste the following example and click **Execute**.  
  
    ```  
    -- Creates a database master key.   
    -- The key is encrypted using the password "<master key password>"  
    USE master;  
    GO  
    CREATE MASTER KEY ENCRYPTION BY PASSWORD = '<master key password>';  
    GO  
  
    ```  
  
2.  **Create a Backup Certificate:** Create a backup certificate in the master database. Copy and paste the following example into the query window and click **Execute**  
  
    ```  
    Use Master  
    GO  
    CREATE CERTIFICATE MyTestDBBackupEncryptCert  
       WITH SUBJECT = 'MyTestDB Backup Encryption Certificate';  
    GO  
  
    ```  
  
3.  **Backup the database:** Specify the encryption algorithm and certificate to use. Copy and paste the following example into the query window and click **Execute**.  

    ```
    BACKUP DATABASE [MyTestDB]  
    TO DISK = N'C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Backup\MyTestDB.bak'  
    WITH  
      COMPRESSION,  
      ENCRYPTION   
       (  
       ALGORITHM = AES_256,  
       SERVER CERTIFICATE = MyTestDBBackupEncryptCert  
       ),  
      STATS = 10  
    GO
    ```  
  
 For an example of encrypting a backup protected by an EKM, see [Extensible Key Management Using Azure Key Vault &#40;SQL Server&#41;](../../relational-databases/security/encryption/extensible-key-management-using-azure-key-vault-sql-server.md).  
  
### Backup to Azure Storage with Encryption  
 If you are creating a backup to Azure storage using the **SQL Server Backup to URL** option, the encryption steps are the same, but you must use URL as the destination and a SQL Credential to authenticate to the Azure storage. If you want to configure [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] with encryption options, see [Enable SQL Server Managed Backup to Microsoft Azure](../../relational-databases/backup-restore/enable-sql-server-managed-backup-to-microsoft-azure.md).  
  
 **Prerequisites:**  
  
-   A Windows storage account and a container. For more information, see. [Lesson 1: Create Azure Storage Objects](/previous-versions/sql/sql-server-2016/jj720557(v=sql.130)).  
  
-   A Database Master Key for the master database, and a certificate or asymmetric key  on the instance of SQL Server. For encryption requirements and permissions, see [Backup Encryption](../../relational-databases/backup-restore/backup-encryption.md).  
  
1.  **Create SQL Server Credential:** To create a SQL Server credential, connect to the Database Engine, open a new query window, and copy and paste the following example and click **Execute**.  
  
    ```  
    CREATE CREDENTIAL mycredential   
    WITH IDENTITY= 'mystorageaccount' - this is the name of the storage account you specified when creating a storage account    
    , SECRET = '<storage account access key>' - this should be either the Primary or Secondary Access Key for the storage account  
    ```  
  
2.  **Create a Database Master Key:** Choose a password for encrypting the copy of the master key that will be stored in the database. Connect to the database engine, start a new query windows and copy and paste the following example and click **Execute**.  
  
    ```  
    -- Creates a database master key.  
    -- The key is encrypted using the password "<master key password>"  
    USE Master;  
    GO  
    CREATE MASTER KEY ENCRYPTION BY PASSWORD = '<master key password>';  
    GO  
  
    ```  
  
3.  **Create a Backup Certificate:** Create a Backup Certificate in the master database. Copy and paste the following example in the query window and click **Execute**  
  
    ```  
    USE Master;  
    GO  
    CREATE CERTIFICATE MyTestDBBackupEncryptCert  
       WITH SUBJECT = 'MyTestDBBackupEncryptCert ';  
    GO  
  
    ```  
  
4.  **Backup the database:** Specify the encryption algorithm and the certificate to use. Copy and paste the following example into the query window and click **Execute**.  
  
    ```  
    BACKUP DATABASE [MyTestDB]  
    TO URL = N'C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Backup\MyTestDB.bak'  
    WITH  
      CREDENTIAL 'mycredential' - this is the name of the credential created in the first step.  
      ,COMPRESSION  
      ,ENCRYPTION   
       (  
       ALGORITHM = AES_256,  
       SERVER CERTIFICATE = MyTestDBBackupEncryptCert  
       ),  
      STATS = 10  
    GO  
  
    ```  
  
