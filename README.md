# Description

This project is the Azure Database Migration for AiCore, aiming to migrate data to Azure SQL Database using Azure Micsosoft tools.

## Milestone 2


###  Task 1: Setting up virtual Machine

Steps:

    Choose a Cloud Provider: Select a cloud provider (such as Microsoft Azure) to create a Virtual Machine (VM).
    Create a Virtual Machine Instance:
    the VM size for this project was 16gb, 
    region chosen for this project was UKSouth, and operating system (Windows or Linux).
    Set up networking (assign a public IP, configure security groups, etc.).
    Install any necessary tools (such as SSH for Linux VMs).


### Task 2: Connecting Virtual Machine


Access the VM:

Use SSH (for Linux) or Remote Desktop (for Windows) to connect to the VM. I choose to connect my VM through Remote Desktop because i used windows VM operating system for this project.

Ensure proper firewall rules to allow SQL Server traffic.

Configure Network Settings:

    Assign a static IP address to the VM. This ensures consistency and easy access.
    Set up DNS settings to resolve domain names.

Enable Remote Desktop Protocol (RDP):

    Go to Control Panel > System > Remote settings.
    Enable “Allow remote connections to this computer.”
    Ensure that the user account you’ll use for RDP has proper permissions.





### Task 3: Installing SQL Server and SSMS


SQL Server Installation:

SQL Server is the relational database management system. You can download the latest version from the official Microsoft website. Follow these steps:

    Visit the SQL Server Downloads page.
    Choose the appropriate edition (e.g., Developer, Express, Standard, etc.) based on your requirements.
    I choose Develop edition for this for project.
    Download the installer and run it.
    Follow the installation wizard, specifying necessary configurations like instance name, authentication mode, and data directories.
    Once installed, start the SQL Server service.

SQL Server Management Studio

SQL Server Management Studio (SSMS) Installation:

 SSMS provides a comprehensive environment for managing SQL Server instances and databases. Here’s how to install it:

Visit the [SSMS download page](https://learn.microsoft.com/en-us/sql/ssms/download-sql-server-management-studio-ssms?view=sql-server-ver16).

    Click on the “Free Download” button for SQL Server Management Studio (SSMS) 19.3 (the latest GA version as of now).
    Install SSMS by following the setup instructions.
    During installation, you’ll be prompted to choose components. Ensure you select “Management Tools - Complete” to include SSMS.
    Agree to the license terms and privacy statement.
    Once installed, launch SSMS and connect to your SQL Server instance.


### Task 4: Creating Production Database.

    Download the AdventureWorks Backup File:
    First, ensure you have the AdventureWorks backup file. If you don’t, you can download it from the official Microsoft GitHub repository.
    Choose the appropriate version (e.g., AdventureWorks2019.bak) based on your SQL Server version.
    I used AdventureWorks2022.bak for this project.

Restore the Database:

    Open SQL Server Management Studio (SSMS).
    Connect to your SQL Server instance.
    Right-click on Databases in the Object Explorer and select Restore Database.
    In the General section, choose the Device option and click the … button.
    Navigate to the location where you saved the AdventureWorks backup file and select it.
    Click OK to close the dialog.
    In the Options section, ensure that the Overwrite the existing database option is selected.
    Click OK to start the restore process.
    
Verify the Restoration:

    Once the restoration completes, expand the Databases node in the Object Explorer. You should see the AdventureWorks database listed.
    Right-click on it and select New Query.
    Execute a simple query (e.g., SELECT TOP 1000 * FROM Person.Person) to verify that the data is accessible.
    
Explore the AdventureWorks Database:

    AdventureWorks contains various tables, views, stored procedures, and sample data.
    Explore different aspects of the database to understand its structure and relationships.
    You can start by querying tables like Sales.SalesOrderHeader, Production.Product, or HumanResources.Employee.

## Milestone 3

### Task 1: Setting up Azure SQL Database


Create an Azure SQL Database:

    Log in to your Azure Portal.
    Navigate to the SQL databases section.
    Click on + Add to create a new database.
    Choose the appropriate settings, such as database name, resource group, server, and pricing tier.
    Ensure that you select SQL authentication (username and password) during the setup process.
    
Configure Firewall Rules:

    Once your database is created, go to the Firewall settings section.
    Add your IP address to the allowed IP list. This step ensures that you can connect to the database securely.
    You can also configure a range of IP addresses if needed.
    
SQL Login Credentials:

    Make sure you have the SQL login credentials (username and password) handy. These will be used to authenticate your application or tools when connecting to the database.
    
Connection String:

    Retrieve the connection string for your Azure SQL Database. This string contains all the necessary information for connecting to the database, including the server name, database name, username, and password.
    Test the Connection:
    Use tools like Azure Data Studio, SQL Server Management Studio (SSMS), or your preferred programming language (e.g., Python, C#) to connect to the Azure SQL Database using the connection string.
    Verify that you can successfully connect and query the database.

### Task 2: Preparation for Migration.

Download Azure Data Studio:

Visit the [Azure Data Studio download page](https://learn.microsoft.com/en-us/azure-data-studio/download-azure-data-studio?tabs=win-install%2Cwin-user-install%2Credhat-install%2Cwindows-uninstall%2Credhat-uninstall).

    Click the “User installer (recommended)” hyperlink to initiate the download. This installer is tailored for individual users and simplifies installations and updates.
    
Installation:

    Once the download is complete, double-click the Azure Data Studio executable to launch the setup wizard.
    Follow the on-screen instructions to install Azure Data Studio.
    Note that this installation doesn’t require administrator privileges since it’s installed under your user’s Local AppData folder.
    
Launch Azure Data Studio:

    You can now launch Azure Data Studio from the Start Menu or by searching for “sqlops.”
    Alternatively, run the command sqlops in the command prompt.
    
Connect to Your On-Premises Database:

    Open Azure Data Studio.
    Click the “New Connection” button.
    Provide the necessary details for your existing on-premises database, such as server name, authentication method, and credentials.
    Test the connection to ensure it’s successful.



### Task 3: Connecting to Azure SQL Database


Connect to Your Azure SQL Database:

    Open Azure Data Studio.
    If the Welcome page doesn’t automatically appear, you can access it by selecting Help > Welcome.
    Click New Connection to open the Connection pane.
    Fill in the following details using your Azure SQL Database information:
    Server name: The fully qualified server name (e.g., servername.database.windows.net).
    Authentication: Choose SQL Login.
    User name: Use the server admin account user name.
    Password: Enter the server admin account password.
    Save Password: Select Yes if you want to avoid entering the password each time.
    Leave the Database name field blank since you’re only connecting to the server.
    Set the Server Group to <Default> or a specific group you’ve created.
    Click Connect.


### Task 4: Schema Migration


Install the SQL Server Schema Compare Extension:

    In Azure Data Studio, select the Extensions Icon (usually represented by a square grid) to view available extensions.
    Search for the Schema Compare extension and select it to view its details.
    Click Install to add the extension.
    Once installed, click Reload to enable the extension in Azure Data Studio (this step is only required when installing an extension for the first time).
    
Compare and Migrate Schema:

    To compare schemas, open the Schema Compare dialog box:
    Right-click a database in Object Explorer and select Schema Compare.
    The database you select becomes the Source database in the comparison.
    You can customize the comparison by clicking the Options button in the toolbar.
    Click Compare to view the results of the comparison.
    
To migrate schema changes:

    Install both the Schema Compare and Azure SQL Migration extensions.
    From a Database dashboard, select Update Project from Database in the toolbar.
    Choose the existing SQL project and the desired file structure for new objects.
    Review the changes in Schema Compare before applying them to the SQL project.


### Task 5: Data Migration 

Prerequisites:

    If you don’t have an Azure subscription, create a free Azure account before you begin.
    Ensure that you have Azure Data Studio installed. If not, you can download it from the Azure Data Studio download page.
    
Install the Azure SQL Migration Extension:

    Open Azure Data Studio.
    In the extensions manager, search for “Azure SQL Migration.”
    Select the Azure SQL Migration extension and view its details.
    Click Install to add the extension.
    Once installed, you’ll see the Azure SQL Migration extension in the extension list.
    
Connecting to Your On-Premises Database:

    Connect to your on-premises SQL Server instance within Azure Data Studio.
    Ensure that you have the necessary permissions to access the source database.
    
Assess and Migrate:

    The extension provides a responsive UI for an end-to-end migration experience.
    It starts with a migration readiness assessment and SKU recommendation (preview) based on performance data.
    You can evaluate SQL Server instances and identify databases ready for migration to Azure SQL targets.
    The SKU recommendation engine collects performance data from the on-premises source SQL Server instance and generates right-sized SKU recommendations for your Azure SQL target.
    The extension uses Azure Database Migration Service to orchestrate data movement activities, allowing you to run migrations online (minimal downtime) or offline (persistent downtime) based on your business needs.
    You can also configure a self-hosted integration runtime to access source SQL Server instance backup files in your on-premises environment.
    It provides a secure and improved user experience for migrating TDE databases and SQL/Windows logins to Azure SQL.
    
Migration Scenarios:
The extension supports various migration scenarios, including:

    SQL Server to Azure SQL Managed Instance (online/offline).
    SQL Server to SQL Server on an Azure virtual machine (online/offline).
    SQL Server to Azure SQL Database (offline).
    
Remember to deploy the database schema in Azure SQL Database before starting the migration.


### Task 6: Validating Migration Success

Schema Validation:

    Connect to the Azure SQL Database using Azure Data Studio or any SQL Server client.
    Compare the schema of the migrated database with the source database to ensure that all tables, views, stored procedures, and other objects were migrated successfully.
    Check for any schema-related errors or missing objects.
    
Data Validation:

    Execute sample queries to compare data between the source and target databases.
    Verify that the number of rows in critical tables matches between the on-premise and Azure SQL databases.
    Use checksums or hash functions to compare the integrity of data between the source and target.
    
Index and Constraints Validation:

    Check that indexes and constraints (primary keys, foreign keys) have been successfully migrated.
    Verify the index structures and configurations to ensure optimal performance.

Stored Procedures, Functions, and Triggers:

    Validate the migration of stored procedures, functions, and triggers.
    Test the execution of critical stored procedures to ensure they perform as expected in the Azure SQL Database.
    
Configuration and Settings:

    Verify that database settings, configurations, and options have been migrated correctly.
    Check compatibility levels, collation settings, and any database-specific configurations.

Permissions and Security:

    Confirm that user accounts, roles, and permissions have been migrated accurately.
    Validate that security settings, such as firewall rules, are configured correctly in Azure SQL Database.

Data Consistency and Integrity:

    Perform data consistency checks, especially if the migration involved downtime.
    Validate that any data modifications made during the migration process are accounted for and reflect accurately in the Azure SQL Database.
    
Application Integration Testing:

    If possible, conduct integration testing with the applications connected to the migrated database.
    Verify that the applications can read and write data as expected.

Error Handling and Logging:

    Review any migration logs or reports generated during the migration process.
    Address and investigate any reported errors or warnings.
    
Performance Testing:

    Conduct performance tests to ensure that the Azure SQL Database meets the performance expectations.
    Monitor and optimize queries if necessary.

Backup and Recovery Testing:

    Ensure that backup and recovery mechanisms are in place.
    Perform a test restore to validate the backup and recovery processes.

## Milestone 4


### Task 1: Backup the on-Premises Database

    Open SQL Server Management Studio (SSMS) on the Windows VM.
    Connect to the SQL Server instance where your production database resides.
    In the Object Explorer, right-click on your database and select Tasks > Back Up….
    In the Back Up Database dialog, choose the following options:
    Backup type: Select Full.
    Destination: Specify a location where you want to save the backup file (e.g., a local folder or network share).
    Backup set name: Provide a descriptive name for the backup set.
    Expiration: Set an appropriate retention period for the backup.
    Click OK to start the backup process. SSMS will create a full backup of your database.
    Once the backup completes, verify that the backup file is saved in the designated location on your computer.
    
Remember to schedule regular backups and test the restoration process periodically to ensure the safety of your data


### Task 2: Upload backup to blob storage
Create an Azure Blob Storage Account:

    Log in to the Azure Portal.
    Click on Create a resource and search for Storage account.
    Follow the prompts to create a new storage account.
    Choose a unique name, select the appropriate region, and configure other settings (such as performance and redundancy options).
    Once created, note down the connection string for later use.
    
Upload the Backup File to Blob Storage:

    Open your preferred method of interacting with Azure (Azure Portal, Azure CLI, or Azure Storage Explorer).
    Navigate to your newly created storage account.
    Create a new Blob container within the storage account.
    Upload your previously created database backup file (.bak extension) to this container.
    Ensure that the container’s access level is set to Private or Blob (anonymous read access for blobs only) for security.
    

### Task 3: Restore Database on Development environment
Provision a New Windows VM:

    In your Azure or virtualization platform, create a new Windows virtual machine (VM) that closely mirrors your development setup.
    Ensure that the VM specifications (CPU, memory, storage) align with your requirements for testing and development.
    
Install SQL Server:

    Once the VM is up and running, install SQL Server on it. You can use the same version as your production environment or a compatible one.
    Configure SQL Server with the necessary components (such as database engine, SSMS, and any additional features you need).
    
Restore the Database Backup:

    Transfer the database backup file (which you previously created from the production environment) to the new VM.
    Open SQL Server Management Studio (SSMS) on the VM.
    Connect to the SQL Server instance.
    Right-click on Databases in the Object Explorer and choose Restore Database.
    Select the backup file and follow the prompts to restore it onto the new VM.
    Ensure that the restored database has the same schema and data as your production database.
    
Configure Security and Permissions:

    Set up appropriate security measures for the sandbox environment. Limit access to authorized users.
    Create separate logins and users for developers working in the sandbox.
    Be cautious about granting excessive permissions to avoid accidental changes.
    
Test and Experiment Safely:

    Now you have a “sandbox” environment where you can safely explore new concepts, test code changes, and experiment without affecting the production data.
    Use this space to try out different scenarios, troubleshoot issues, and validate changes before deploying them to production.
    
Remember that the development environment should closely resemble the production environment to ensure accurate testing. Regularly refresh the sandbox with fresh data from production to maintain its relevance


### Task 4: Automate backups for Development environment

Open SSMS on your Windows VM.

Connect to the SQL Server instance where your development database resides.

In the Object Explorer, right-click on your database and select Tasks > Back Up….

In the Back Up Database dialog, configure the following options:

    Backup type: Choose Full.
    Destination: Specify a location where you want to save the backups (e.g., a local folder or network share).
    Backup set name: Provide a descriptive name for the backup set.
    Expiration: Set an appropriate retention period for the backups (e.g., keep backups for 1 week).
    Schedule: Click on the Script button to generate a T-SQL script for the backup task.
    Save the generated T-SQL script. You can create a SQL Server Agent Job to execute this script on a weekly basis.
    
Create a SQL Server Agent Job:

    In SSMS, navigate to SQL Server Agent > Jobs.
    Right-click and choose New Job.
    Name the job (e.g., “WeeklyBackup”).
    Under Steps, add a new step and paste the T-SQL script.
    Configure the schedule to run weekly (e.g., every Sunday at midnight).
    
Test the Backup Task:

    Execute the job manually to verify that backups are created successfully.
    Monitor the job history for any issues.
    
By following these steps, you’ll have an automated weekly backup process in place, ensuring consistent protection for your evolving work in the development environment

## Milestone 5

### Task 1: Mimic data loss in the production environment

Restore AdventureWorks Database:

    First, restore the AdventureWorks database from the provided backup file (adventureworks.bak) onto your SQL Server instance.
    You can use SQL Server Management Studio (SSMS) or Azure Data Studio to perform the restoration.
    
Identify Critical Data:

     Review the schema of the AdventureWorks database.
    Identify tables or records that contain critical data. For example, consider customer information, sales transactions, or inventory levels.
    
Simulate Data Loss:

    Choose a specific table or set of records to remove. Be deliberate in your selection.
    Execute SQL commands to delete or modify data. For instance:

    DELETE FROM Sales.SalesOrderDetail WHERE OrderQty > 200;
    Document the exact changes made, including the affected tables and the reason for removal.
    
Document the Simulation:

    Create a detailed record:
    Date and Time: When the simulation occurred.
    Affected Data: Specify which data was intentionally removed.
    Purpose: Explain why this data was chosen (e.g., testing recovery procedures).
    Steps Taken: Describe the SQL commands executed.
    Expected Impact: Document how this data loss affects your application.
    Recovery Plan: Outline the steps to restore the lost data.
    
Confirm Success:

    After simulating data loss, verify that your application behaves as expected. Test critical functionalities.
    Use the established connection in Azure Data Studio to examine the database and confirm the absence of the intentionally removed data.


### Task 2: Restore Database from Azure SQL Database backup

Restore the Database:

    Open the Azure portal and navigate to your Azure SQL Database.
    Go to the Overview page of your database.
    Click on Restore in the toolbar.
    Choose the backup source (which should be the backup taken just before the data loss).
    Select the point-in-time backup point from which you want to create a new database.
    
Validation:

    Once the restoration completes, connect to the restored database using Azure Data Studio.
    Examine the data to ensure that it matches the state just before the data loss.
    Test critical functionalities to verify that the restored database behaves as expected.
    
Production Database Update:

    Keep in mind that the restored database will now function as your production database.
    The previous production database, which lacks critical data, should be deleted in the Azure portal.
    
Remember to document this process meticulously for future reference. Regularly practice these recovery procedures to maintain confidence in your disaster recovery strategy.


## Milestone 6

### Task 1: Set up Geo-replication for Azure SQL Database

Log in to the Azure Portal:

    Navigate to the Azure Portal.
    Create a New Azure SQL Database (if you haven’t already):
    Click on Create a resource.
    Search for SQL Database and select it.
    Follow the prompts to create a new database.
    Choose the appropriate geographical region for this primary database.
    In this project, i chose uk-south as my primary database
    
Enable Geo-Replication:

    Once your primary database is set up, go to its overview page.
    Click on Geo-Replication in the left menu.
    Click Add secondary.
    Choose the target region where you want to create the replica (ensure it’s in a different geographical region).
    In this project, i chose East US.
    Configure the read-write or read-only access for the secondary database.
    Click Create.
    
Monitor and Test:

    Azure will automatically create a synchronized replica (secondary database) in the target region.
    Monitor the replication status in the portal.
    Test failover scenarios to ensure the secondary database is ready for use in case of a disaster.
    
Connection Strings:

    Obtain the connection strings for both the primary and secondary databases.
    Applications can use the secondary connection string for read operations, offloading traffic from the primary


### Task 2: Test failover and fallback

Planned Failover to Secondary Region:

    Geo-Replication Setup: Ensure that you’ve already set up geo-replication for your Azure SQL Database, with the primary database in UK South and the secondary (geo-replica) in East US.
    Initiate Failover: In the Azure portal or using Azure CLI, initiate a planned failover to the secondary region. This transition will make the secondary copy the new primary.
    DNS Update: DNS entries for your database endpoints will be updated, pointing to the secondary region as the new primary. Clients can now write to the new primary endpoints.

    

![](https://github.com/Maxwella10/azure-database-migration902/blob/main/images/migration_failover.png)



    
Evaluate Availability and Data Consistency:


    Application Testing: Test your application against the new primary endpoints in East US. Ensure it behaves as expected and handles read and write operations.

    

![](https://github.com/Maxwella10/azure-database-migration902/blob/main/images/migration_failover_2.png)



Data Consistency: Verify that the data in the secondary region is consistent with the state just before the failover. Check critical records and transactions.

Monitoring: Monitor performance and availability of the new primary. Look for any anomalies or issues.

Failback to Primary Region:

Stabilize the Secondary: If everything looks good, plan for the failback to the primary region (UK South).

Initiate Failback: In the Azure portal or using Azure CLI, initiate a failback to the primary region. The original primary becomes the new primary again.

DNS Update (Again): DNS entries will be updated once more, pointing back to the original primary endpoints.

Application Testing (Again): Test your application against the restored primary endpoints in UK South. Ensure it functions correctly.



![](https://github.com/Maxwella10/azure-database-migration902/blob/main/images/migration_failover_3.png)


Testing Outcomes

Latency and Replication Lag:

    Measure the replication lag between the primary and secondary databases.
    Understand the impact of network latency and database workload on replication.
    
Read-Only Workloads:

    Leverage the readable secondary for read-only workloads (e.g., reporting, analytics).
    Test the performance of read queries against the secondary.
    
Failover Scenarios:

    Simulate failover scenarios (e.g., planned maintenance, disaster recovery).
    Document the time taken for failover and application behavior during the process.
    
Insights Gained

Cost Considerations:
  
    Understand the cost implications of maintaining a secondary database.
    Evaluate whether active geo-replication or readable secondary is more suitable for your workload.
    
Application Resilience:

    Ensure that your application can handle failover seamlessly.
    Implement retry logic and connection pooling to handle transient errors during failover.
    
Business Continuity:

    Geo-replication provides peace of mind for disaster recovery.
    Regularly test failover to validate your setup.



## Milestone 7



### Task 1: Configure Microsoft Entra ID Azure SQL Database

