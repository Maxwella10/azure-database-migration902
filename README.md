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

    Install both the Schema Compare and SQL Database Project extensions.
    From a Database dashboard, select Update Project from Database in the toolbar.
    Choose the existing SQL project and the desired file structure for new objects.
    Review the changes in Schema Compare before applying them to the SQL project.
