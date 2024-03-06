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
