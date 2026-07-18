![](Image00000.jpg)

[SQL Server on Linux](#text00002.html_aC2T)[Install SQL Server and create a database on Red Hat](#text00002.html_aC2U)[Unattended SQL Server installation script for Red Hat Enterprise Linux](#text00003.html_aC2V)[Migrate a SQL Server database from Windows to Linux using backup and restore](#text00003.html_aC2W)[Migrate databases and structured data to SQL Server on Linux](#text00004.html_aC2X)[Bulk copy data with bcp to SQL Server on Linux](#text00005.html_aC2Y)[Prepare data for bulk export or import](#text00005.html_aC2Z)[Extract, transform, and load data on Linux with SSIS](#text00006.html_aC30)[Run SQL Server container images with Docker](#text00007.html_aC31)[Tools and commands for running SQL Server 2019 on Linux](#text00008.html_aC32)[System Dynamic Management Views](#text00009.html_aC33)[Monitoring performance by using the Query Store](#text00010.html_aC34)[Best practices with Query Store](#text00010.html_aC35)[Configure SQL Server on Linux with the mssql-conf tool](#text00011.html_aC36)[Install sqlcmd and bcp the SQL Server command-line tools on Linux](#text00011.html_aC37)[Mssql-cli a interactive command line tool for SQL Server](#text00012.html_aC38)[SQL Server PowerShell](#text00012.html_aC39)[Manage SQL Server on Linux with PowerShell Core](#text00012.html_aC3A)[Get started with Log Shipping on Linux](#text00012.html_aC3B)[DB Mail and Email Alerts with SQL Agent on Linux](#text00012.html_aC3C)[Business continuity and database recovery - SQL Server on Linux](#text00012.html_aC3D)[SQL Server availability basics for Linux deployments](#text00012.html_aC3E)[Backup and restore SQL Server databases on Linux](#text00012.html_aC3F)[SQL Server on Linux VDI client SDK Specification](#text00012.html_aC3G)[Failover Cluster Instances - SQL Server on Linux](#text00012.html_aC3H)[Always On Availability Groups on Linux](#text00013.html_aC3J)[High availability and data protection for availability group configurations](#text00013.html_aC3K)[SQL Server Always On Availability Group for high availability on Linux](#text00014.html_aC3M)[Performance best practices and configuration guidelines for SQL Server on Linux](#text00015.html_aC3N)[Performance features of SQL Server on Linux](#text00016.html_aC3P)[SQL Server Replication on Linux](#text00017.html_aC3R)[Troubleshoot SQL Server on Linux](#text00018.html_aC3S)[High availability for SQL Server containers](#text00018.html_aC3T)[Deploy a SQL Server container in Kubernetes with Azure Kubernetes Services (AKS)](#text00018.html_aC3U)[Security features of SQL Server on Linux](#text00019.html_aC3V)[Active Directory authentication for SQL Server on Linux](#text00019.html_aC3W)[Encrypting Connections to SQL Server on Linux](#text00019.html_aC3X)SQL Server on LinuxSQL Server 2019 runs on Linux. It's the same SQL Server database engine, with many similar features and services regardless of your operating system.After installation, connect to the SQL Server instance on your Linux machine. You can connect locally or remotely and with a variety of tools and drivers. The quickstarts demonstrate how to use the sqlcmd command-line tool. Other tools include the following:SQL Server 2019 (15.x) has the same underlying database engine on all supported platforms, including Linux. Therefore, many existing features and capabilities operate the same way on Linux.Install SQL Server and create a database on Red HatIn this quickstart, you install SQL Server 2019 on Red Hat Enterprise Linux (RHEL) 8\. You then connect with sqlcmd to create your first database and run queries.You must have a RHEL 7.3 - 7.8, or 8.0 - 8.2 machine with at least 2 GB of memory.To install Red Hat Enterprise Linux on your own machine, go to https://access.redhat.com/products/red-hat-enterprise-linux/evaluation. You can also create RHEL virtual machines in Azure. See Create and Manage Linux VMs with the Azure CLI, and use --image RHEL in the call to az vm create.If you have previously installed a CTP or RC release of SQL Server, you must first remove the old repository before following these steps. For more information, see Configure Linux repositories for SQL Server 2017 and 2019.Install SQL ServerThe following commands for SQL Server 2019 points to the RHEL 8 repository. RHEL 8 does not come preinstalled with python2, which is required by SQL Server. Before you begin the SQL Server install steps, execute the command and verify that python2 is selected as the interpreter:sudo alternatives --config python# If not configured, install python2 and openssl10 using the following commands:sudo yum install python2sudo yum install compat-openssl10# Configure python2 as the default interpreter using this command:sudo alternatives --config pythonFor more information about these steps, see the following blog on installing python2 and configuring it as the default interpreter: https://www.redhat.com/en/blog/installing-microsoft-sql-server-red-hat-enterprise-linux-8-beta .If you are using RHEL 7, change the path below to /rhel/7 instead of /rhel/8.To configure SQL Server on RHEL, run the following commands in a terminal to install the mssql-server package:

1.  Download the Microsoft SQL Server 2019 Red Hat repository configuration file:

Bashsudo curl -o /etc/yum.repos.d/mssql-server.repo https://packages.microsoft.com/config/rhel/8/mssql-server-2019.repo

2.  Run the following commands to install SQL Server:

Bashsudo yum install -y mssql-server

3.  After the package installation finishes, run mssql-conf setup and follow the prompts to set the SA password and choose your edition.

Bashsudo /opt/mssql/bin/mssql-conf setup

4.  Once the configuration is done, verify that the service is running:

Bashsystemctl status mssql-server

5.  To allow remote connections, open the SQL Server port on the firewall on RHEL. The default SQL Server port is TCP 1433\. If you are using FirewallD for your firewall, you can use the following commands:

Bashsudo firewall-cmd --zone=public --add-port=1433/tcp --permanentsudo firewall-cmd --reloadAt this point, SQL Server 2019 is running on your RHEL machine and is ready to use!Install the SQL Server command-line toolsTo create a database, you need to connect with a tool that can run Transact-SQL statements on the SQL Server. The following steps install the SQL Server command-line tools: sqlcmd and bcp.

1.  Download the Microsoft Red Hat repository configuration file.

Bashsudo curl -o /etc/yum.repos.d/msprod.repo https://packages.microsoft.com/config/rhel/8/prod.repo

2.  If you had a previous version of mssql-tools installed, remove any older unixODBC packages.

Bashsudo yum remove unixODBC-utf16 unixODBC-utf16-devel

3.  Run the following commands to install mssql-tools with the unixODBC developer package.

Bashsudo yum install -y mssql-tools unixODBC-devel

4.  For convenience, add /opt/mssql-tools/bin/ to your PATH environment variable. This enables you to run the tools without specifying the full path. Run the following commands to modify the PATH for both login sessions and interactive/non-login sessions:

Bashecho 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bash_profileecho 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bashrcsource ~/.bashrcConnect locallyThe following steps use sqlcmd to locally connect to your new SQL Server instance.

1.  Run sqlcmd with parameters for your SQL Server name (-S), the user name (-U), and the password (-P). In this tutorial, you are connecting locally, so the server name is localhost. The user name is SA and the password is the one you provided for the SA account during setup.

Bashsqlcmd -S localhost -U SA -P '<YourPassword>'

2.  If successful, you should get to a sqlcmd command prompt: 1>.
3.  If you get a connection failure, first attempt to diagnose the problem from the error message.

Unattended SQL Server installation script for Red Hat Enterprise LinuxThis sample Bash script installs SQL Server 2017 on Red Hat Enterprise Linux (RHEL) without interactive input. It provides examples of installing the database engine, the SQL Server command-line tools, SQL Server Agent, and performs post-install steps. You can optionally install full-text search and create an administrative user.

*   You need at least 2 GB of memory to run SQL Server on Linux.
*   The file system must be  XFS  or  EXT4 . Other file systems, such as  BTRFS , are unsupported.

Sample scriptSave the sample script to a file and then to customize it, replace the variable values in the script. You can also set any of the scripting variables as environment variables, as long as you remove them from the script file.Bash#!/bin/bash -e# Use the following variables to control your install:# Password for the SA user (required)MSSQL_SA_PASSWORD='<YourStrong!Passw0rd>'# Product ID of the version of SQL server you're installing# Must be evaluation, developer, express, web, standard, enterprise, or your 25 digit product key# Defaults to developerMSSQL_PID='evaluation'# Install SQL Server Agent (recommended)SQL_ENABLE_AGENT='y'# Install SQL Server Full Text Search (optional)# SQL_INSTALL_FULLTEXT='y'# Create an additional user with sysadmin privileges (optional)# SQL_INSTALL_USER='<Username>'# SQL_INSTALL_USER_PASSWORD='<YourStrong!Passw0rd>'if [ -z $MSSQL_SA_PASSWORD ]thenecho Environment variable MSSQL_SA_PASSWORD must be set for unattended installexit 1fiecho Adding Microsoft repositories...sudo curl -o /etc/yum.repos.d/mssql-server.repo https://packages.microsoft.com/config/rhel/7/mssql-server-2017.reposudo curl -o /etc/yum.repos.d/msprod.repo https://packages.microsoft.com/config/rhel/7/prod.repoecho Installing SQL Server...sudo yum install -y mssql-serverecho Running mssql-conf setup...sudo MSSQL_SA_PASSWORD=$MSSQL_SA_PASSWORD \MSSQL_PID=$MSSQL_PID \/opt/mssql/bin/mssql-conf -n setup accept-eulaecho Installing mssql-tools and unixODBC developer...sudo ACCEPT_EULA=Y yum install -y mssql-tools unixODBC-devel# Add SQL Server tools to the path by default:echo Adding SQL Server tools to your path...echo PATH="$PATH:/opt/mssql-tools/bin" >> ~/.bash_profileecho 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bashrcsource ~/.bashrc# Optional Enable SQL Server Agent :if [ ! -z $SQL_ENABLE_AGENT ]thenecho Enable SQL Server Agent...sudo /opt/mssql/bin/mssql-conf set sqlagent.enabled truesudo systemctl restart mssql-serverfi# Optional SQL Server Full Text Search installation:if [ ! -z $SQL_INSTALL_FULLTEXT ]thenecho Installing SQL Server Full-Text Search...sudo yum install -y mssql-server-ftsfi# Configure firewall to allow TCP port 1433:echo Configuring firewall to allow traffic on port 1433...sudo firewall-cmd --zone=public --add-port=1433/tcp --permanentsudo firewall-cmd --reload# Example of setting post-installation configuration options# Set trace flags 1204 and 1222 for deadlock tracing:#echo Setting trace flags...#sudo /opt/mssql/bin/mssql-conf traceflag 1204 1222 on# Restart SQL Server after making configuration changes:echo Restarting SQL Server...sudo systemctl restart mssql-server# Connect to server and get the version:counter=1errstatus=1while [ $counter -le 5 ] && [ $errstatus = 1 ]doecho Waiting for SQL Server to start...sleep 5s/opt/mssql-tools/bin/sqlcmd \-S localhost \-U SA \-P $MSSQL_SA_PASSWORD \-Q "SELECT @@VERSION" 2>/dev/nullerrstatus=$?((counter++))done# Display error if connection failed:if [ $errstatus = 1 ]thenecho Cannot connect to SQL Server, installation abortedexit $errstatusfi# Optional new user creation:if [ ! -z $SQL_INSTALL_USER ] && [ ! -z $SQL_INSTALL_USER_PASSWORD ]thenecho Creating user $SQL_INSTALL_USER/opt/mssql-tools/bin/sqlcmd \-S localhost \-U SA \-P $MSSQL_SA_PASSWORD \-Q "CREATE LOGIN [$SQL_INSTALL_USER] WITH PASSWORD=N'$SQL_INSTALL_USER_PASSWORD', DEFAULT_DATABASE=[master], CHECK_EXPIRATION=ON, CHECK_POLICY=ON; ALTER SERVER ROLE [sysadmin] ADD MEMBER [$SQL_INSTALL_USER]"fiecho Done!Running the scriptTo run the script

1.  Paste the sample into your favorite text editor and save it with a memorable name, like install_sql.sh.
2.  Customize MSSQL_SA_PASSWORD, MSSQL_PID, and any of the other variables you'd like to change.
3.  Mark the script as executable

Bashchmod +x install_sql.sh

4.  Run the script

Bash./install_sql.shUnderstanding the scriptThe first thing the Bash script does is set a few variables. These can be either scripting variables, like the sample, or environment variables. The variable MSSQL_SA_PASSWORD is required  by SQL Server installation, the others are custom variables created for the script. The sample script performs the following steps:

1.  Import the public Microsoft GPG keys.
2.  Register the Microsoft repositories for SQL Server and the command-line tools.
3.  Update the local repositories
4.  Install SQL Server
5.  Configure SQL Server with the MSSQL_SA_PASSWORD and automatically accept the End-User License Agreement.
6.  Automatically accept the End-User License Agreement for the SQL Server command-line tools, install them, and install the unixodbc-dev package.
7.  Add the SQL Server command-line tools to the path for ease of use.
8.  Install the SQL Server Agent if the scripting variable SQL_INSTALL_AGENT is set, on by default.
9.  Optionally install SQL Server Full-Text search, if the variable SQL_INSTALL_FULLTEXT is set.
10.  Unblock port 1433 for TCP on the system firewall, necessary to connect to SQL Server from another system.
11.  Optionally set trace flags for deadlock tracing. (requires uncommenting the lines)
12.  SQL Server is now installed, to make it operational, restart the process.
13.  Verify that SQL Server is installed correctly, while hiding any error messages.
14.  Create a new server administrator user if SQL_INSTALL_USER and SQL_INSTALL_USER_PASSWORD are both set.

Next stepsSimplify multiple unattended installs and create a stand-alone Bash script that sets the proper environment variables. You can remove any of the variables the sample script uses and put them in their own Bash script.Bash#!/bin/bashexport MSSQL_SA_PASSWORD='<YourStrong!Passw0rd>'export MSSQL_PID='evaluation'export SQL_INSTALL_AGENT='y'export SQL_INSTALL_USER='<Username>'export SQL_INSTALL_USER_PASSWORD='<YourStrong!Passw0rd>'export SQL_INSTALL_AGENT='y'Then run the Bash script as follows:Bash. ./my_script_name.shCreate and query dataThe following sections walk you through using sqlcmd to create a new database, add data, and run a simple query.Create a new databaseThe following steps create a new database named TestDB.

1.  From the sqlcmd command prompt, paste the following Transact-SQL command to create a test database:

SQLCREATE DATABASE TestDB

2.  On the next line, write a query to return the name of all of the databases on your server:

SQLSELECT Name from sys.Databases

3.  The previous two commands were not executed immediately. You must type GO on a new line to execute the previous commands:

SQLGOInsert dataNext create a new table, Inventory, and insert two new rows.

1.  From the sqlcmd command prompt, switch context to the new TestDB database:

SQLUSE TestDB

2.  Create new table named Inventory:

SQLCREATE TABLE Inventory (id INT, name NVARCHAR (50), quantity INT)

3.  Insert data into the new table:

SQLINSERT INTO Inventory VALUES (1, 'banana', 150); INSERT INTO Inventory VALUES (2, 'orange', 154);

4.  Type GO to execute the previous commands:

SQLGOSelect dataNow, run a query to return data from the Inventory table.

1.  From the sqlcmd command prompt, enter a query that returns rows from the Inventory table where the quantity is greater than 152:

SQLSELECT * FROM Inventory WHERE quantity > 152;

2.  Execute the command:

SQLGOExit the sqlcmd command promptTo end your sqlcmd session, type QUIT:SQLQUITPerformance best practicesAfter installing SQL Server on Linux, review the best practices for configuring Linux and SQL Server to improve performance for production scenarios.Cross-platform data toolsIn addition to sqlcmd, you can use the following cross-platform tools to manage SQL Server:

| CROSS-PLATFORM DATA TOOLS |
| --- |
| Tool | Description |
| --- | --- |
| Azure Data Studio | A cross-platform GUI database management utility. |
| Visual Studio Code | A cross-platform GUI code editor that run Transact-SQL statements with the mssql extension. |
| PowerShell Core | A cross-platform automation and configuration tool based on cmdlets. |
| mssql-cli | A cross-platform command-line interface for running Transact-SQL commands. |
|  |  |

Connecting from WindowsSQL Server tools on Windows connect to SQL Server instances on Linux in the same way they would connect to any remote SQL Server instance.If you have a Windows machine that can connect to your Linux machine, try the same steps in this topic from a Windows command-prompt running sqlcmd. Just verify that you use the target Linux machine name or IP address rather than localhost, and make sure that TCP port 1433 is open.For other tools that run on Windows but connect to SQL Server on Linux, see:

*   SQL Server Management Studio (SSMS)
*   Windows PowerShell
*   SQL Server Data Tools (SSDT)

Migrate a SQL Server database from Windows to Linux using backup and restoreSQL Server's backup and restore feature is the recommended way to migrate a database from SQL Server on Windows to SQL Server on Linux. In this tutorial, you will walk through the steps required to move a database to Linux with backup and restore techniques.

*   Create a backup file on Windows with SSMS
*   Install a Bash shell on Windows
*   Move the backup file to Linux from the Bash shell
*   Restore the backup file on Linux with Transact-SQL
*   Run a query to verify the migration

You can also create a SQL Server Always On Availability Group to migrate a SQL Server database from Windows to Linux. The following prerequisites are required to complete this tutorial:

*   Windows machine with the following:
    *   SQL Server installed.
    *   SQL Server Management Studio installed.
    *   Target database to migrate.
*   Linux machine with the following installed:
    *   SQL Server (RHEL, SLES, or Ubuntu) with command-line tools.

Create a backup on WindowsThere are several ways to create a backup file of a database on Windows. The following steps use SQL Server Management Studio (SSMS).

1.  Start SQL Server Management Studio  on your Windows machine.
2.  In the connection dialog, enter localhost .
3.  In Object Explorer, expand Databases .
4.  Right-click your target database, select Tasks , and then click Back Up... .

![Use SSMS to create a backup file](Image00002.jpg)

5.  In the Backup Up Database  dialog, verify that Backup type  is Full  and Back up to  is Disk . Note name and location of the file. For example, a database named YourDB  on SQL Server 2016 has a default backup path of C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Backup\YourDB.bak.
6.  Click OK  to back up your database.

Another option is to run a Transact-SQL query to create the backup file. The following Transact-SQL command performs the same actions as the previous steps for a database called YourDB :SQLBACKUP DATABASE [YourDB] TO  DISK =N'C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Backup\YourDB.bak'WITH NOFORMAT, NOINIT, NAME = N'YourDB-Full Database Backup',SKIP, NOREWIND, NOUNLOAD, STATS = 10GOInstall a Bash shell on WindowsTo restore the database, you must first transfer the backup file from the Windows machine to the target Linux machine. In this tutorial, we move the file to Linux from a Bash shell (terminal window) running on Windows.

1.  Install a Bash shell on your Windows machine that supports the scp  (secure copy) and ssh  (remote login) commands. Two examples include:
    *   The Windows Subsystem for Linux (Windows 10)
    *   The Git Bash Shell (https://git-scm.com/downloads)
2.  Open a Bash session on Windows.

Copy the backup file to Linux

1.  In your Bash session, navigate to the directory containing your backup file. For example:

Bashcd 'C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Backup\'

2.  Use the scp  command to transfer the file to the target Linux machine. The following example transfers YourDB.bak  to the home directory of user1  on the Linux server with an IP address of 192.0.2.9 :

Bashscp YourDB.bak user1@192.0.2.9:./![scp command](Image00003.jpg)There are alternatives to using scp for file transfer. One is to use Samba  to configure an SMB network share between Windows and Linux. Once established, you can access it as a network file share from Windows, such as \\machinenameorip\share .Move the backup file before restoringAt this point, the backup file is on your Linux server in your user's home directory. Before restoring the database to SQL Server, you must place the backup in a subdirectory of /var/opt/mssql .

1.  In the same Windows Bash session, connect remotely to your target Linux machine with ssh . The following example connects to the Linux machine 192.0.2.9  as user user1 .

Bashssh user1@192.0.2.9You are now running commands on the remote Linux server.

2.  Enter super user mode.

Bashsudo su

3.  Create a new backup directory. The -p parameter does nothing if the directory already exists.

Bashmkdir -p /var/opt/mssql/backup

4.  Move the backup file to that directory. In the following example, the backup file resides in the home directory of user1 . Change the command to match the location and file name of your backup file.

Bashmv /home/user1/YourDB.bak /var/opt/mssql/backup/

5.  Exit super user mode.

BashexitRestore your database on LinuxTo restore the database backup, you can use the RESTORE DATABASE  Transact-SQL (TQL) command.

1.  In the same terminal, launch sqlcmd . The following example connects to the local SQL Server instance with the SA  user. Enter the password when prompted, or specify the password by adding the -P  parameter.

Bashsqlcmd -S localhost -U SA

2.  At the >1 prompt, enter the following RESTORE DATABASE  command, pressing ENTER after each line (you cannot copy and paste the entire multi-line command at once). Replace all occurrences of YourDB with the name of your database.

SQLRESTORE DATABASE YourDBFROM DISK = '/var/opt/mssql/backup/YourDB.bak'WITH MOVE 'YourDB' TO '/var/opt/mssql/data/YourDB.mdf',MOVE 'YourDB_Log' TO '/var/opt/mssql/data/YourDB_Log.ldf'GOYou should get a message the database is successfully restored.RESTORE DATABASE may return an error like the following example:BashFile 'YourDB_Product' cannot be restored to 'Z:\Microsoft SQL Server\MSSQL11.GLOBAL\MSSQL\Data\YourDB\YourDB_Product.ndf'. Use WITH MOVE to identify a valid location for the file.Msg 5133, Level 16, State 1, Server servername, Line 1Directory lookup for the file "Z:\Microsoft SQL Server\MSSQL11.GLOBAL\MSSQL\Data\YourDB\YourDB_Product.ndf" failed with the operating system error 2(The system cannot find the file specified.).In this case, the database contains secondary files. If these files are not specified in the MOVE clause of RESTORE DATABASE, the restore procedure will try to create them in the same path as the original server.You can list all files included in the backup:SQLRESTORE FILELISTONLY FROM DISK = '/var/opt/mssql/backup/YourDB.bak'GOYou should get a list like the one below (listing only the two first columns):SQLLogicalName         PhysicalName                                                                 ..............----------------------------------------------------------------------------------------------------------------------YourDB              Z:\Microsoft SQL Server\MSSQL11.GLOBAL\MSSQL\Data\YourDB\YourDB.mdf          ..............YourDB_Product      Z:\Microsoft SQL Server\MSSQL11.GLOBAL\MSSQL\Data\YourDB\YourDB_Product.ndf  ..............YourDB_Customer     Z:\Microsoft SQL Server\MSSQL11.GLOBAL\MSSQL\Data\YourDB\YourDB_Customer.ndf ..............YourDB_log          Z:\Microsoft SQL Server\MSSQL11.GLOBAL\MSSQL\Data\YourDB\YourDB_Log.ldf      ..............You can use this list to create MOVE clauses for the additional files. In this example, the RESTORE DATABASE is:SQLRESTORE DATABASE YourDBFROM DISK = '/var/opt/mssql/backup/YourDB.bak'WITH MOVE 'YourDB' TO '/var/opt/mssql/data/YourDB.mdf',MOVE 'YourDB_Product' TO '/var/opt/mssql/data/YourDB_Product.ndf',MOVE 'YourDB_Customer' TO '/var/opt/mssql/data/YourDB_Customer.ndf',MOVE 'YourDB_Log' TO '/var/opt/mssql/data/YourDB_Log.ldf'GO

3.  Verify the restoration by listing all of the databases on the server. The restored database should be listed.

SQLSELECT Name FROM sys.DatabasesGO

4.  Run other queries on your migrated database. The following command switches context to the YourDB  database and selects rows from one of its tables.

SQLUSE YourDBSELECT * FROM YourTableGO

5.  When you are done using sqlcmd , type exit.
6.  When you are done working in the remote ssh session, type exit again.

Migrate databases and structured data to SQL Server on LinuxYou can migrate your databases and data to SQL Server running on Linux. The method you choose to use depends on the source data and your specific scenario. The following sections provide best practices for various migration scenarios.Migrate from SQL Server on WindowsIf you want to migrate SQL Server databases on Windows to SQL Server on Linux, the recommended technique is to use SQL Server backup and restore.

1.  Create a backup of the database on the Windows machine.
2.  Transfer the backup file to the target SQL Server Linux machine.
3.  Restore the backup on the Linux machine.

Migrate from other database serversYou can migrate databases on other database systems to SQL Server on Linux. This includes Microsoft Access, DB2, MySQL, Oracle, and Sybase databases. In this scenario, use the SQL Server Management Assistant (SSMA) to automate the migration to SQL Server on Linux.Migrate structured dataThere are also techniques for importing raw data. You might have structured data files that were exported from other databases or data sources. In this case, you can use the bcp tool to bulk insert the data. Or you can run SQL Server Integration Services on Windows to import the data into a SQL Server database on Linux. SQL Server Integration Services enables you to run more complex transformations on the data during the import.Bulk copy data with bcp to SQL Server on LinuxLet us see how to use the bcp command-line utility to bulk copy data between an instance of SQL Server on Linux and a data file in a user-specified format.You can use bcp to import large numbers of rows into SQL Server tables or to export data from SQL Server tables into data files. Except when used with the queryout option, bcp requires no knowledge of Transact-SQL. The bcp command-line utility works with Microsoft SQL Server running on-premises or in the cloud, on Linux, Windows or Docker and Azure SQL Database and Azure Synapse Analytics.This article shows you how to:

*   Import data into a table using the bcp in command
*   Export data from a table using the bcp out command

Install the SQL Server command-line toolsbcp is part of the SQL Server command-line tools, which are not installed automatically with SQL Server on Linux. If you have not already installed the SQL Server command-line tools on your Linux machine, you must install them. For more information on how to install the tools, for Red Hat Enterprise Linux (RHEL)Install tools on RHEL 8Use the following steps to install the mssql-tools on Red Hat Enterprise Linux.

1.  Enter superuser mode.

Bashsudo su

2.  Download the Microsoft Red Hat repository configuration file.

Bashcurl https://packages.microsoft.com/config/rhel/8/prod.repo > /etc/yum.repos.d/msprod.repo

3.  Exit superuser mode.

Bashexit

4.  If you had a previous version of mssql-tools installed, remove any older unixODBC packages.

Bashsudo yum remove mssql-tools unixODBC-utf16-devel

5.  Run the following commands to install mssql-tools with the unixODBC developer package.

Bashsudo yum install mssql-tools unixODBC-devel NoteTo update to the latest version of mssql-tools run the following commands:Bashsudo yum check-updatesudo yum update mssql-tools

6.  Optional: Add /opt/mssql-tools/bin/ to your PATH environment variable in a bash shell.

To make sqlcmd/bcp accessible from the bash shell for login sessions, modify your PATH in the ~/.bash_profile file with the following command:Bashecho 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bash_profileTo make sqlcmd/bcp accessible from the bash shell for interactive/non-login sessions, modify the PATH in the ~/.bashrc file with the following command:Bashecho 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bashrcsource ~/.bashrcImport data with bcpIn this tutorial, you create a sample database and table on the local SQL Server instance (localhost) and then use bcp to load into the sample table from a text file on disk.Create a sample database and tableLet's start by creating a sample database with a simple table that is used in the rest of this tutorial.

1.  On your Linux box, open a command terminal.
2.  Copy and paste the following commands into the terminal window. These commands use the sqlcmd command-line utility to create a sample database (BcpSampleDB) and a table (TestEmployees) on the local SQL Server instance (localhost). Remember to replace the username and <your_password> as necessary before running the commands.

Create the database BcpSampleDB:Bashsqlcmd -S localhost -U sa -P <your_password> -Q "CREATE DATABASE BcpSampleDB;"Create the table TestEmployees in the database BcpSampleDB:Bashsqlcmd -S localhost -U sa -P <your_password> -d BcpSampleDB -Q "CREATE TABLE TestEmployees (Id INT IDENTITY(1,1) NOT NULL PRIMARY KEY, Name NVARCHAR(50), Location NVARCHAR(50));"Create the source data fileCopy and paste the following command into your terminal window. We use the built-in cat command to create a sample text data file with three records save the file in your home directory as ~/test_data.txt. The fields in the records are delimited by a comma.Bashcat > ~/test_data.txt << EOF1,Jared,Australia2,Nikita,India3,Tom,GermanyEOFYou can verify that the data file was created correctly by running the following command in your terminal window:Bashcat ~/test_data.txtThis should display the following in your terminal window:Bash1,Jared,Australia2,Nikita,India3,Tom,GermanyImport data from the source data fileCopy and paste the following commands into the terminal window. This command uses bcp to connect to the local SQL Server instance (localhost) and import the data from the data file (~/test_data.txt) into the table (TestEmployees) in the database (BcpSampleDB). Remember to replace the username and <your_password> as necessary before running the commands.Bashbcp TestEmployees in ~/test_data.txt -S localhost -U sa -P <your_password> -d BcpSampleDB -c -t  ','Here's a brief overview of the command-line parameters we used with bcp in this example:

*   -S: specifies the instance of SQL Server to which to connect
*   -U: specifies the login ID used to connect to SQL Server
*   -P: specifies the password for the login ID
*   -d: specifies the database to connect to
*   -c: performs operations using a character data type
*   -t: specifies the field terminator. We are using comma as the field terminator for the records in our data file

You can verify that the data was successfully imported by running the following command in your terminal window. Remember to replace the username and <your_password> as necessary before running the command.Bashsqlcmd -S localhost -d BcpSampleDB -U sa -P <your_password> -I -Q "SELECT * FROM TestEmployees;"This should display the following results:BashId          Name                Location----------- ------------------- -------------------1 Jared               Australia2 Nikita              India3 Tom                 Germany(3 rows affected)Export data with bcpIn this tutorial, you use bcp to export data from the sample table we created earlier to a new data file.Copy and paste the following commands into the terminal window. These commands use the bcp command-line utility to export data from the table TestEmployees in the database BcpSampleDB to a new data file called ~/test_export.txt. Remember to replace the username and <your_password> as necessary before running the command.Bashbcp TestEmployees out ~/test_export.txt -S localhost -U sa -P <your_password> -d BcpSampleDB -c -t ','You can verify that the data was exported correctly by running the following command in your terminal window:Bashcat ~/test_export.txtThis should display the following in your terminal window:1,Jared,Australia2,Nikita,India3,Tom,Germanybcp UtilityThe bulk copy program utility (bcp) bulk copies data between an instance of Microsoft SQL Server and a data file in a user-specified format. The bcp utility can be used to import large numbers of new rows into SQL Server tables or to export data out of tables into data files. Except when used with the queryout option, the utility requires no knowledge of Transact-SQL. To import data into a table, you must either use a format file created for that table or understand the structure of the table and the types of data that are valid for its columns.If you use bcp to back up your data, create a format file to record the data format. bcp data files do not include any schema or format information, so if a table or view is dropped and you do not have a format file, you may be unable to import the data.Download the latest version of bcp UtilityThe command-line tools are General Availability (GA), however they're being released with the installer package for SQL Server 2019 (15.x).Version InformationRelease number: 15.0.2
Build number: 15.0.2000.5
Release date: September 11, 2020The new version of SQLCMD supports Azure AD authentication, including Multi-Factor Authentication (MFA) support for SQL Database, Azure Synapse Analytics, and Always Encrypted features. The new BCP supports Azure AD authentication, including Multi-Factor Authentication (MFA) support for SQL Database and Azure Synapse Analytics.System RequirementsWindows 10, Windows 7, Windows 8, Windows 8.1, Windows Server 2008, Windows Server 2008 R2, Windows Server 2008 R2 SP1, Windows Server 2012, Windows Server 2012 R2, Windows Server 2016, Windows Server 2019This component requires both Windows Installer 4.5 and Microsoft ODBC Driver 17 for SQL Server.To check the BCP version execute bcp /v command and confirm that 15.0.2000.5 or higher is in use.

| SYSTEM REQUIREMENTS |
| Syntax |
| bcp [database_name.] schema.{table_name &#124; view_name &#124; "query"}{in data_file &#124; out data_file &#124; queryout data_file &#124; format nul}[-a packet_size][-b batch_size][-c][-C { ACP &#124; OEM &#124; RAW &#124; code_page } ][-d database_name][-D][-e err_file][-E][-f format_file][-F first_row][-G Azure Active Directory Authentication][-h"hint [,...n]"][-i input_file][-k][-K application_intent][-l login_timeout][-L last_row][-m max_errors][-n][-N][-o output_file][-P password][-q][-r row_term][-R][-S [server_name[\instance_name]][-t field_term][-T][-U login_id][-v][-V (80 &#124; 90 &#124; 100 &#124; 110 &#124; 120 &#124; 130 ) ][-w][-x] |

Argumentsdata_file
Is the full path of the data file. When data is bulk imported into SQL Server, the data file contains the data to be copied into the specified table or view. When data is bulk exported from SQL Server, the data file contains the data copied from the table or view. The path can have from 1 through 255 characters. The data file can contain a maximum of 2^63 - 1 rows.database_name
Is the name of the database in which the specified table or view resides. If not specified, this is the default database for the user.You can also explicitly specify the database name with -d.in data_file | out data_file | queryout data_file | format nul
Specifies the direction of the bulk copy, as follows:

*   in copies from a file into the database table or view.
*   out copies from the database table or view to a file. If you specify an existing file, the file is overwritten. When extracting data, the bcp utility represents an empty string as a null and a null string as an empty string.
*   queryout copies from a query and must be specified only when bulk copying data from a query.
*   format creates a format file based on the option specified (-n, -c, -w, or -N) and the table or view delimiters. When bulk copying data, the bcp command can refer to a format file, which saves you from reentering format information interactively. The format option requires the -f option; creating an XML format file, also requires the -x option. For more information, see Create a Format File (SQL Server). You must specify nul as the value (format nul).

owner
Is the name of the owner of the table or view. owner is optional if the user performing the operation owns the specified table or view. If owner is not specified and the user performing the operation does not own the specified table or view, SQL Server returns an error message, and the operation is canceled." query  " Is a Transact-SQL query that returns a result set. If the query returns multiple result sets, only the first result set is copied to the data file; subsequent result sets are ignored. Use double quotation marks around the query and single quotation marks around anything embedded in the query. queryout must also be specified when bulk copying data from a query.The query can reference a stored procedure as long as all tables referenced inside the stored procedure exist prior to executing the bcp statement. For example, if the stored procedure generates a temp table, the bcp statement fails because the temp table is available only at run time and not at statement execution time. In this case, consider inserting the results of the stored procedure into a table and then use bcp to copy the data from the table into a data file.table_name
Is the name of the destination table when importing data into SQL Server (in), and the source table when exporting data from SQL Server (out).view_name
Is the name of the destination view when copying data into SQL Server (in), and the source view when copying data from SQL Server (out). Only views in which all columns refer to the same table can be used as destination views.-a packet_size
Specifies the number of bytes, per network packet, sent to and from the server. A server configuration option can be set by using SQL Server Management Studio (or the sp_configure system stored procedure). However, the server configuration option can be overridden on an individual basis by using this option. packet_size can be from 4096 bytes to 65535 bytes; the default is 4096.Increased packet size can enhance performance of bulk-copy operations. If a larger packet is requested but cannot be granted, the default is used. The performance statistics generated by the bcp utility show the packet size used.-b batch_size
Specifies the number of rows per batch of imported data. Each batch is imported and logged as a separate transaction that imports the whole batch before being committed. By default, all the rows in the data file are imported as one batch. To distribute the rows among multiple batches, specify a batch_size that is smaller than the number of rows in the data file. If the transaction for any batch fails, only insertions from the current batch are rolled back. Batches already imported by committed transactions are unaffected by a later failure.Do not use this option in conjunction with the -h "ROWS_PER_BATCH =bb " option.-c
Performs the operation using a character data type. This option does not prompt for each field; it uses char as the storage type, without prefixes and with \t (tab character) as the field separator and \r\n (newline character) as the row terminator. -c is not compatible with -w.-C { ACP | OEM | RAW | code_page }
Specifies the code page of the data in the data file. code_page is relevant only if the data contains char, varchar, or text columns with character values greater than 127 or less than 32.

| Code page value | Description |
| --- | --- |
| ACP | ANSI/Microsoft Windows (ISO 1252). |
| OEM | Default code page used by the client. This is the default code page used if -C  is not specified. |
| RAW | No conversion from one code page to another occurs. This is the fastest option because no conversion occurs. |
| code_page | Specific code page number; for example, 850. Versions prior to version 13 (SQL Server 2016 (13.x)) do not support code page 65001 (UTF-8 encoding). Versions beginning with 13 can import UTF-8 encoding to earlier versions of SQL Server. |

-d database_name
Specifies the database to connect to. By default, bcp.exe connects to the user's default database. If -d database_name and a three part name (database_name.schema.table, passed as the first parameter to bcp.exe) are specified, an error will occur because you cannot specify the database name twice. If database_name begins with a hyphen (-) or a forward slash (/), do not add a space between -d and the database name.-D
Causes the value passed to the bcp -S option to be interpreted as a data source name (DSN). A DSN may be used to embed driver options to simplify command lines, enforce driver options that are not otherwise accessible from the command line such as MultiSubnetFailover, or to help protect sensitive credentials from being discoverable as command line arguments.-e err_file
Specifies the full path of an error file used to store any rows that the bcp utility cannot transfer from the file to the database. Error messages from the bcp command go to the workstation of the user. If this option is not used, an error file is not created.If err_file begins with a hyphen (-) or a forward slash (/), do not include a space between -e and the err_file value.-ESpecifies that identity value or values in the imported data file are to be used for the identity column. If -E is not given, the identity values for this column in the data file being imported are ignored, and SQL Server automatically assigns unique values based on the seed and increment values specified during table creation.If the data file does not contain values for the identity column in the table or view, use a format file to specify that the identity column in the table or view should be skipped when importing data; SQL Server automatically assigns unique values for the column.The -E option has a special permissions requirement.-f format_file
Specifies the full path of a format file. The meaning of this option depends on the environment in which it is used, as follows:

*   If -f is used with the format option, the specified format_file is created for the specified table or view. To create an XML format file, also specify the -x option.
*   If used with the in or out option, -f requires an existing format file.

If format_file begins with a hyphen (-) or a forward slash (/), do not include a space between -f and the format_file value.-F first_row
Specifies the number of the first row to export from a table or import from a data file. This parameter requires a value greater than (>) 0 but less than (<) or equal to (=) the total number rows. In the absence of this parameter, the default is the first row of the file.first_row can be a positive integer with a value up to 2^63-1. -F first_row is 1-based.-GThis switch is used by the client when connecting to Azure SQL Database or Azure Synapse Analytics to specify that the user be authenticated using Azure Active Directory authentication. The -G switch requires version 14.0.3008.27 or later. To determine your version, execute bcp -v.ImportantThe -G option only applies to Azure SQL Database and Azure Data Warehouse. AAD Integrated and Interactive Authentication is not currently supported on Linux or macOS.TipTo check if your version of bcp includes support for Azure Active Directory Authentication (AAD) type bcp -- (bcp<space><dash><dash>) and verify that you see -G in the list of available arguments.

*   Azure Active Directory Username and Password:

When you want to use an Azure Active Directory user name and password, you can provide the -G option and also use the user name and password by providing the -U and -P options.The following example exports data using Azure AD Username and Password where user and password is an AAD credential. The example exports table bcptest from database testdb from Azure server aadserver.database.windows.net and stores the data in file c:\last\data1.dat:cmdbcp bcptest out "c:\last\data1.dat" -c -t -S aadserver.database.windows.net -d testdb -G -U alice@aadtest.onmicrosoft.com -P xxxxxThe following example imports data using Azure AD Username and Password where user and password is an AAD credential. The example imports data from file c:\last\data1.dat into table bcptest for database testdb on Azure server aadserver.database.windows.net using Azure AD User/Password:cmdbcp bcptest in "c:\last\data1.dat" -c -t -S aadserver.database.windows.net -d testdb -G -U alice@aadtest.onmicrosoft.com -P xxxxx

*   Azure Active Directory Integrated

For Azure Active Directory Integrated authentication, provide the -G option without a user name or password. This configuration assumes that the current Windows user account (the account the bcp command is running under) is federated with Azure AD:The following example exports data using Azure AD-Integrated account. The example exports table bcptest from database testdb using Azure AD Integrated from Azure server aadserver.database.windows.net and stores the data in file c:\last\data2.dat:cmdbcp bcptest out "c:\last\data2.dat" -S aadserver.database.windows.net -d testdb -G -c -tThe following example imports data using Azure AD-Integrated auth. The example imports data from file c:\last\data2.txt into table bcptest for database testdb on Azure server aadserver.database.windows.net using Azure AD Integrated auth:cmdbcp bcptest in "c:\last\data2.dat" -S aadserver.database.windows.net -d testdb -G -c -t

*   Azure Active Directory Interactive

The Azure AD Interactive authentication for Azure SQL Database and Azure Synapse Analytics, allows you to use an interactive method supporting multi-factor authentication.To enable interactive authentication, provide -G option with user name (-U) only, without a password.The following example exports data using Azure AD interactive mode indicating username where user represents an AAD account. This is the same example used in the previous section: Azure Active Directory Username and Password.Interactive mode requires a password to be manually entered, or for accounts with multi-factor authentication enabled, complete your configured MFA authentication method.cmdbcp bcptest out "c:\last\data1.dat" -c -t -S aadserver.database.windows.net -d testdb -G -U alice@aadtest.onmicrosoft.comIn case an Azure AD user is a domain federated one using Windows account, the user name required in the command line, contains its domain account (for example, joe@contoso.com see below):cmdbcp bcptest out "c:\last\data1.dat" -c -t -S aadserver.database.windows.net -d testdb -G -U joe@contoso.comIf guest users exist in a specific Azure AD and are part of a group that exists in SQL Database that has database permissions to execute the bcp command, their guest user alias is used (for example, *keith0@adventureworks.com*).-h "load hints [ ,... n]" Specifies the hint or hints to be used during a bulk import of data into a table or view.

*   ORDER( column [ASC | DESC] [,... n ])
    The sort order of the data in the data file. Bulk import performance is improved if the data being imported is sorted according to the clustered index on the table, if any. If the data file is sorted in a different order, that is other than the order of a clustered index key, or if there is no clustered index on the table, the ORDER clause is ignored. The column names supplied must be valid column names in the destination table. By default, bcp assumes the data file is unordered. For optimized bulk import, SQL Server also validates that the imported data is sorted.
*   ROWS_PER_BATCH =  bb
    Number of rows of data per batch (as bb). Used when -b is not specified, resulting in the entire data file being sent to the server as a single transaction. The server optimizes the bulkload according to the value bb. By default, ROWS_PER_BATCH is unknown.
*   KILOBYTES_PER_BATCH =  cc
    Approximate number of kilobytes of data per batch (as cc). By default, KILOBYTES_PER_BATCH is unknown.
*   TABLOCK
    Specifies that a bulk update table-level lock is acquired for the duration of the bulkload operation; otherwise, a row-level lock is acquired. This hint significantly improves performance because holding a lock for the duration of the bulk-copy operation reduces lock contention on the table. A table can be loaded concurrently by multiple clients if the table has no indexes and TABLOCK is specified. By default, locking behavior is determined by the table option table lock on bulkload.

  CHECK_CONSTRAINTS
Specifies that all constraints on the target table or view must be checked during the bulk-import operation. Without the CHECK_CONSTRAINTS hint, any CHECK, and FOREIGN KEY constraints are ignored, and after the operation the constraint on the table is marked as not-trusted.At some point, you will need to check the constraints on the entire table. If the table was nonempty before the bulk import operation, the cost of revalidating the constraint may exceed the cost of applying CHECK constraints to the incremental data. Therefore, we recommend that normally you enable constraint checking during an incremental bulk import.A situation in which you might want constraints disabled (the default behavior) is if the input data contains rows that violate constraints. With CHECK constraints disabled, you can import the data and then use Transact-SQL statements to remove data that is not valid.

*   FIRE_TRIGGERS
    Specified with the in argument, any insert triggers defined on the destination table will run during the bulk-copy operation. If FIRE_TRIGGERS is not specified, no insert triggers will run. FIRE_TRIGGERS is ignored for the out, queryout, and format arguments.

-i input_file
Specifies the name of a response file, containing the responses to the command prompt questions for each data field when a bulk copy is being performed using interactive mode (-n, -c, -w, or -N not specified).If input_file begins with a hyphen (-) or a forward slash (/), do not include a space between -i and the input_file value.-k
Specifies that empty columns should retain a null value during the operation, rather than have any default values for the columns inserted.-K application_intent
Declares the application workload type when connecting to a server. The only value that is possible is ReadOnly. If -K is not specified, the bcp utility will not support connectivity to a secondary replica in an Always On availability group.-l login_timeout
Specifies a login timeout. The -l option specifies the number of seconds before a login to SQL Server times out when you try to connect to a server. The default login timeout is 15 seconds. The login timeout must be a number between 0 and 65534\. If the value supplied is not numeric or does not fall into that range, bcp generates an error message. A value of 0 specifies an infinite timeout.-L last_row
Specifies the number of the last row to export from a table or import from a data file. This parameter requires a value greater than (>) 0 but less than (<) or equal to (=) the number of the last row. In the absence of this parameter, the default is the last row of the file.last_row can be a positive integer with a value up to 2^63-1.-m max_errors
Specifies the maximum number of syntax errors that can occur before the bcp operation is canceled. A syntax error implies a data conversion error to the target data type. The max_errors total excludes any errors that can be detected only at the server, such as constraint violations.A row that cannot be copied by the bcp utility is ignored and is counted as one error. If this option is not included, the default is 10.-n
Performs the bulk-copy operation using the native (database) data types of the data. This option does not prompt for each field; it uses the native values.-N
Performs the bulk-copy operation using the native (database) data types of the data for noncharacter data, and Unicode characters for character data. This option offers a higher performance alternative to the -w option, and is intended for transferring data from one instance of SQL Server to another using a data file. It does not prompt for each field. Use this option when you are transferring data that contains ANSI extended characters and you want to take advantage of the performance of native mode.If you export and then import data to the same table schema by using bcp.exe with -N, you might see a truncation warning if there is a fixed length, non-Unicode character column (for example, char(10)).The warning can be ignored. One way to resolve this warning is to use -n instead of -N.-o output_file
Specifies the name of a file that receives output redirected from the command prompt.If output_file begins with a hyphen (-) or a forward slash (/), do not include a space between -o and the output_file value.-P password
Specifies the password for the login ID. If this option is not used, the bcp command prompts for a password. If this option is used at the end of the command prompt without a password, bcp uses the default password (NULL).ImportantDo not use a blank password. Use a strong password.To mask your password, do not specify the -P option along with the -U option. Instead, after specifying bcp along with the -U option and other switches (do not specify -P), press ENTER, and the command will prompt you for a password. This method ensures that your password will be masked when it is entered.If password begins with a hyphen (-) or a forward slash (/), do not add a space between -P and the password value.-q
Executes the SET QUOTED_IDENTIFIERS ON statement in the connection between the bcp utility and an instance of SQL Server. Use this option to specify a database, owner, table, or view name that contains a space or a single quotation mark. Enclose the entire three-part table or view name in quotation marks ("").To specify a database name that contains a space or single quotation mark, you must use the -q option.-q does not apply to values passed to -d.-r row_term
Specifies the row terminator. The default is \n (newline character). Use this parameter to override the default row terminator.If you specify the row terminator in hexadecimal notation in a bcp.exe command, the value will be truncated at 0x00\. For example, if you specify 0x410041, 0x41 will be used.If row_term begins with a hyphen (-) or a forward slash (/), do not include a space between -r and the row_term value.-R
Specifies that currency, date, and time data is bulk copied into SQL Server using the regional format defined for the locale setting of the client computer. By default, regional settings are ignored.-S server_name  [\instance_name ] Specifies the instance of SQL Server to which to connect. If no server is specified, the bcp utility connects to the default instance of SQL Server on the local computer. This option is required when a bcp command is run from a remote computer on the network or a local named instance. To connect to the default instance of SQL Server on a server, specify only server_name. To connect to a named instance of SQL Server, specify server_name\instance_name.-t field_term
Specifies the field terminator. The default is \t (tab character). Use this parameter to override the default field terminator.If you specify the field terminator in hexadecimal notation in a bcp.exe command, the value will be truncated at 0x00\. For example, if you specify 0x410041, 0x41 will be used.If field_term begins with a hyphen (-) or a forward slash (/), do not include a space between -t and the field_term value.-T
Specifies that the bcp utility connects to SQL Server with a trusted connection using integrated security. The security credentials of the network user, login_id, and password are not required. If -T is not specified, you need to specify -U and -P to successfully log in.ImportantWhen the bcp utility is connecting to SQL Server with a trusted connection using integrated security, use the -T option (trusted connection) instead of the user name and password combination. When the bcp utility is connecting to SQL Database or Azure Synapse Analytics, using Windows authentication or Azure Active Directory authentication is not supported. Use the -U and -P options.-U login_id
Specifies the login ID used to connect to SQL Server.ImportantWhen the bcp utility is connecting to SQL Server with a trusted connection using integrated security, use the -T option (trusted connection) instead of the user name and password combination. When the bcp utility is connecting to SQL Database or Azure Synapse Analytics, using Windows authentication or Azure Active Directory authentication is not supported. Use the -U and -P options.-v
Reports the bcp utility version number and copyright.-V (80 | 90 | 100 | 110 | 120 | 130)
Performs the bulk-copy operation using data types from an earlier version of SQL Server. This option does not prompt for each field; it uses the default values.80 = SQL Server 2000 (8.x)90 = SQL Server 2005 (9.x)100 = SQL Server 2008 and SQL Server 2008 R2110 = SQL Server 2012 (11.x)120 = SQL Server 2014 (12.x)130 = SQL Server 2016 (13.x)For example, to generate data for types not supported by SQL Server 2000 (8.x), but were introduced in later versions of SQL Server, use the -V80 option.-w
Performs the bulk copy operation using Unicode characters. This option does not prompt for each field; it uses nchar as the storage type, no prefixes, \t (tab character) as the field separator, and \n (newline character) as the row terminator. -w is not compatible with -c.-x
Used with the format and -f format_file options, generates an XML-based format file instead of the default non-XML format file. The -x does not work when importing or exporting data. It generates an error if used without both format and -f format_file.

*   The bcp 13.0 client is installed when you install MicrosoftSQL Server 2019 (15.x) tools. If tools are installed for both SQL Server 2019 (15.x) and an earlier version of SQL Server, depending on the order of values of the PATH environment variable, you might be using the earlier bcp client instead of the bcp 13.0 client. This environment variable defines the set of directories used by Windows to search for executable files. To discover which version you are using, run the bcp /v or bcp -v command at the Windows Command Prompt.

To make sure the newest version of the bcp utility is running you need to remove any older versions of the bcp utility.To determine where all versions of the bcp utility are installed, type in the command prompt:cmdwhere bcp.exeThe characters <, >, |, &, ^ are special command shell characters, and they must be preceded by the escape character (^) or enclosed in quotation marks when used in String (for example, "StringContaining&Symbol"). If you use quotation marks to enclose a string that contains one of the special characters, the quotation marks are set as part of the environment variable value.Native Data File SupportIn SQL Server 2019 (15.x), the bcp utility supports native data files compatible with SQL Server 2000 (8.x), SQL Server 2005 (9.x), SQL Server 2008, SQL Server 2008 R2, and SQL Server 2012 (11.x).Computed Columns and timestamp ColumnsValues in the data file being imported for computed or timestamp columns are ignored, and SQL Server automatically assigns values. If the data file does not contain values for the computed or timestamp columns in the table, use a format file to specify that the computed or timestamp columns in the table should be skipped when importing data; SQL Server automatically assigns values for the column.Computed and timestamp columns are bulk copied from SQL Server to a data file as usual.Specifying Identifiers That Contain Spaces or Quotation MarksSQL Server identifiers can include characters such as embedded spaces and quotation marks. Such identifiers must be treated as follows:

*   When you specify an identifier or file name that includes a space or quotation mark at the command prompt, enclose the identifier in quotation marks ("").

For example, the following bcp out command creates a data file named Currency Types.dat:cmdbcp AdventureWorks2012.Sales.Currency out "Currency Types.dat" -T -c 

*   To specify a database name that contains a space or quotation mark, you must use the -q option.
*   For owner, table, or view names that contain embedded spaces or quotation marks, you can either:
    *   Specify the -q option, or
    *   Enclose the owner, table, or view name in brackets ([]) inside the quotation marks.

Data Validationbcp now enforces data validation and data checks that might cause scripts to fail if they're executed on invalid data in a data file. For example, bcp now verifies that:

*   The native representations of float or real data types are valid.
*   Unicode data has an even-byte length.

Forms of invalid data that could be bulk imported in earlier versions of SQL Server might fail to load now; whereas, in earlier versions, the failure did not occur until a client tried to access the invalid data. The added validation minimizes surprises when querying the data after bulkload.Bulk Exporting or Importing SQLXML DocumentsTo bulk export or import SQLXML data, use one of the following data types in your format file.

| BULK EXPORTING OR IMPORTING SQLXML DOCUMENTS |
| --- |
| Data type | Effect |
| --- | --- |
| SQLCHAR or SQLVARYCHAR | The data is sent in the client code page or in the code page implied by the collation). The effect is the same as specifying the -c  switch without specifying a format file. |
| SQLNCHAR or SQLNVARCHAR | The data is sent as Unicode. The effect is the same as specifying the -w  switch without specifying a format file. |
| SQLBINARY or SQLVARYBIN | The data is sent without any conversion. |
|  |  |

PermissionsA bcp out operation requires SELECT permission on the source table.A bcp in operation minimally requires SELECT/INSERT permissions on the target table. In addition, ALTER TABLE permission is required if any of the following is true:

*   Constraints exist and the CHECK_CONSTRAINTS hint is not specified.
*   Triggers exist and the FIRE_TRIGGER hint is not specified.
*   You use the -E option to import identity values from a data file.

Character Mode (-c) and Native Mode (-n) Best PracticesThis section has recommendations for to character mode (-c) and native mode (-n).

*   (Administrator/User) When possible, use native format (-n) to avoid the separator issue. Use the native format to export and import using SQL Server. Export data from SQL Server using the -c or -w option if the data will be imported to a non-SQL Server database.
*   (Administrator) Verify data when using BCP OUT. For example, when you use BCP OUT, BCP IN, and then BCP OUT verify that the data is properly exported and the terminator values are not used as part of some data value. Consider overriding the default terminators (using -t and -r options) with random hexadecimal values to avoid conflicts between terminator values and data values.
*   (User) Use a long and unique terminator (any sequence of bytes or characters) to minimize the possibility of a conflict with the actual string value. This can be done by using the -t and -r options.

This section contains the following examples:A. Identify bcp utility versionB. Copying table rows into a data file (with a trusted connection)C. Copying table rows into a data file (with Mixed-mode Authentication)D. Copying data from a file to a tableE. Copying a specific column into a data fileF. Copying a specific row into a data fileG. Copying data from a query to a data fileH. Creating format filesI. Using a format file to bulk import with bcpJ. Specifying a code pageExample Test ConditionsThe examples below make use of the WideWorldImporters sample database for SQL Server (starting 2016) and Azure SQL Database. WideWorldImporters can be downloaded from https://github.com/Microsoft/sql-server-samples/releases/tag/wide-world-importers-v1.0. The examples assume that you are using Windows Authentication and have a trusted connection to the server instance on which you are running the bcp command. A directory named D:\BCP will be used in many of the examples.The script below creates an empty copy of the WideWorldImporters.Warehouse.StockItemTransactions table and then adds a primary key constraint. Run the following T-SQL script in SQL Server Management Studio (SSMS)SQLUSE WideWorldImporters;GOSET NOCOUNT ON ;IF NOT EXISTS (SELECT * FROM sys.tables WHERE name = 'Warehouse.StockItemTransactions_bcp')BEGINSELECT * INTO WideWorldImporters.Warehouse.StockItemTransactions_bcpFROM WideWorldImporters.Warehouse.StockItemTransactionsWHERE 1 = 2;ALTER TABLE Warehouse.StockItemTransactions_bcpADD CONSTRAINT PK_Warehouse_StockItemTransactions_bcp PRIMARY KEY NONCLUSTERED(StockItemTransactionID ASC );ENDTRUNCATE TABLE WideWorldImporters.Warehouse.StockItemTransactions_bcp;A. Identify bcp utility versionAt a command prompt, enter the following command:cmdbcp –vB. Copying table rows into a data file (with a trusted connection)The following examples illustrate the out option on the WideWorldImporters.Warehouse.StockItemTransactions table.

*   Basic This example creates a data file named StockItemTransactions_character.bcp and copies the table data into it using character format.

At a command prompt, enter the following command:cmdbcp WideWorldImporters.Warehouse.StockItemTransactions out D:\BCP\StockItemTransactions_character.bcp -c -T

*   Expanded This example creates a data file named StockItemTransactions_native.bcp and copies the table data into it using the native format. The example also: specifies the maximum number of syntax errors, an error file, and an output file.

At a command prompt, enter the following command:cmdbcp WideWorldImporters.Warehouse.StockItemTransactions OUT D:\BCP\StockItemTransactions_native.bcp -m 1 -n -e D:\BCP\Error_out.log -o D:\BCP\Output_out.log -S -TReview Error_out.log and Output_out.log. Error_out.log should be blank. Compare the file sizes between StockItemTransactions_character.bcp and StockItemTransactions_native.bcp.C. Copying table rows into a data file (with mixed-mode authentication)The following example illustrates the out option on the WideWorldImporters.Warehouse.StockItemTransactions table. This example creates a data file named StockItemTransactions_character.bcp and copies the table data into it using character format.The example assumes that you are using mixed-mode authentication, you must use the -U switch to specify your login ID. Also, unless you are connecting to the default instance of SQL Server on the local computer, use the -S switch to specify the system name and, optionally, an instance name.At a command prompt, enter the following command: (The system will prompt you for your password.)cmdbcp WideWorldImporters.Warehouse.StockItemTransactions out D:\BCP\StockItemTransactions_character.bcp -c -U<login_id> -S<server_name\instance_name>D. Copying data from a file to a tableThe following examples illustrate the in option on the WideWorldImporters.Warehouse.StockItemTransactions_bcp table using files created above.

*   Basic This example uses the StockItemTransactions_character.bcp data file previously created.

At a command prompt, enter the following command:cmd Copybcp WideWorldImporters.Warehouse.StockItemTransactions_bcp IN D:\BCP\StockItemTransactions_character.bcp -c -T

*   Expanded This example uses the StockItemTransactions_native.bcp data file previously created. The example also: use the hint TABLOCK, specifies the batch size, the maximum number of syntax errors, an error file, and an output file.

At a command prompt, enter the following command:cmdbcp WideWorldImporters.Warehouse.StockItemTransactions_bcp IN D:\BCP\StockItemTransactions_native.bcp -b 5000 -h "TABLOCK" -m 1 -n -e D:\BCP\Error_in.log -o D:\BCP\Output_in.log -S -TReview Error_in.log and Output_in.log.E. Copying a specific column into a data fileTo copy a specific column, you can use the queryout option. The following example copies only the StockItemTransactionID column of the Warehouse.StockItemTransactions table into a data file.At a command prompt, enter the following command:cmdbcp "SELECT StockItemTransactionID FROM WideWorldImporters.Warehouse.StockItemTransactions WITH (NOLOCK)" queryout D:\BCP\StockItemTransactionID_c.bcp -c –TF. Copying a specific row into a data fileTo copy a specific row, you can use the queryout option. The following example copies only the row for the person named Amy Trefl from the WideWorldImporters.Application.People table into a data file Amy_Trefl_c.bcp. Note: the -d switch is used identify the database.At a command prompt, enter the following command:cmdbcp "SELECT * from Application.People WHERE FullName = 'Amy Trefl'" queryout D:\BCP\Amy_Trefl_c.bcp -d WideWorldImporters -c –TG. Copying data from a query to a data fileTo copy the result set from a Transact-SQL statement to a data file, use the queryout option. The following example copies the names from the WideWorldImporters.Application.People table, ordered by full name, into the People.txt data file. Note: the -t switch is used to create a comma-delimited file.At a command prompt, enter the following command:cmdbcp "SELECT FullName, PreferredName FROM WideWorldImporters.Application.People ORDER BY FullName" queryout D:\BCP\People.txt -t, -c –TH. Creating format filesThe following example creates three different format files for the Warehouse.StockItemTransactions table in the WideWorldImporters database. Review the contents of each created file.At a command prompt, enter the following commands:cmdREM non-XML character formatbcp WideWorldImporters.Warehouse.StockItemTransactions format nul -f D:\BCP\StockItemTransactions_c.fmt -c -TREM non-XML native formatbcp WideWorldImporters.Warehouse.StockItemTransactions format nul -f D:\BCP\StockItemTransactions_n.fmt -n -TREM XML character formatbcp WideWorldImporters.Warehouse.StockItemTransactions format nul -f D:\BCP\StockItemTransactions_c.xml -x -c –TI. Using a format file to bulk import with bcpTo use a previously created format file when importing data into an instance of SQL Server, use the -f switch with the in option. For example, the following command bulk copies the contents of a data file, StockItemTransactions_character.bcp, into a copy of the Warehouse.StockItemTransactions_bcp table by using the previously created format file, StockItemTransactions_c.xml. Note: the -L switch is used to import only the first 100 records.At a command prompt, enter the following command:cmdbcp WideWorldImporters.Warehouse.StockItemTransactions_bcp in D:\BCP\StockItemTransactions_character.bcp -L 100 -f D:\BCP\StockItemTransactions_c.xml -TJ. Specifying a code pageThe following partial code example shows bcp import while specifying a code page 65001:cmdbcp.exe MyTable in "D:\data.csv" -T -c -C 65001 -t , ... Prepare data for bulk export or importThis section discusses the considerations involved in planning for bulk-export operations and the requirements for bulk-import operations.Data-File Format Considerations for Bulk ExportBefore you perform a bulk-export operation by using the bcp  command, consider the following:

*   When data is exported to a file, the  bcp  command creates the data file automatically by using the specified file name. If that file name is already in use, the data that is being bulk copied to the data file overwrites the existing contents of the file.
*   Bulk export from a table or view to a data file requires SELECT permission on the table or view that is being bulk copied.
*   Microsoft SQL Server can use parallel scans to retrieve data. Therefore, the table rows that are bulk exported in from an instance of SQL Server are not ordinarily guaranteed to be in any specific order in the data file. To make bulk-exported table rows appear in a specific order in the data file, use the  queryout  option to bulk export from a query, and specify an ORDER BY clause.

Data-File Format Requirements for Bulk ImportTo import data from a data file, the file must meet the following basic requirements:

*   The data must be in row and column format.
*   The data in the data file must be in a supported format such as character or native format.
*   The data can be in character or native binary format including Unicode.

*   To import data by using a  bcp  command, BULK INSERT statement, or INSERT ... SELECT * FROM OPENROWSET(BULK...) statement, the destination table must already exist.
*   Each field in the data file must be compatible with the corresponding column in the target table. For example, an  int  field cannot be loaded into a  datetime  column.
*   To import data from data files with fixed-length or fixed-width fields, use a format file.
*   Comma-separated value (CSV) files are not supported by SQL Server bulk-import operations. However, in some cases, a CSV file can be used as the data file for a bulk import of data into SQL Server. Note that the field terminator of a CSV file does not have to be a comma. To be usable as a data file for bulk import, a CSV file must comply with the following restrictions:
    *   Data fields never contain the field terminator.
    *   Either none or all of the values in a data field are enclosed in quotation marks ("").

To bulk import data from a Microsoft FoxPro or Visual FoxPro table (.dbf) file or a Microsoft Excel worksheet (.xls) file, you would need to convert the data into a CSV file that complies to the preceding restrictions. The file extension will typically be .csv. You can then use the .csv file as a data file in a SQL Server bulk-import operation.On 32-bit systems (SQL Server 2014 and below), it is possible to import CSV data into a SQL Server table without bulk-import optimizations by using OPENROWSET with the OLE DB Provider for Jet. Jet treats text files as tables, with the schema defined by a schema.ini file that is located in the same directory as the data source. For CSV data, one of the parameters in the schema.ini file would be "FORMAT=CSVDelimited". To use this solution, you would need to understand how the Jet Text IISAM operates (its connection string syntax, schema.ini usage, registry setting options, and so on.) The best sources of this information are Microsoft Access Help and Knowledge Base (KB) articles.In addition, the bulk import of data from a data file into a table requires the following:

*   Users must have INSERT and SELECT permissions on the table. Users also need ALTER TABLE permission when they use options that require data definition language (DDL) operations, such as disabling constraints.
*   When you bulk import data by using BULK INSERT or INSERT ... SELECT * FROM OPENROWSET(BULK...), the data file must be accessible for read operations by either the security profile of the SQL Server process (if the user logs in using SQL Server provided login) or by the Microsoft Windows login that is used under delegated security. Additionally, the user must have ADMINISTER BULK OPERATIONS permission to read the file.

BULK INSERT (Transact-SQL)Imports a data file into a database table or view in a user-specified format in SQL ServerSyntaxsyntaxsqlBULK INSERT{ database_name.schema_name.table_or_view_name | schema_name.table_or_view_name | table_or_view_name }FROM 'data_file'[ WITH([ [ , ] BATCHSIZE = batch_size ][ [ , ] CHECK _CONSTRAINTS ][ [ , ] CODEPAGE = { 'ACP' | 'OEM' | 'RAW' | 'code_page' } ][ [ , ] DATAFILETYPE ={ 'char' | 'native'| 'widechar' | 'widenative' } ][ [ , ] DATA _SOURCE = 'data_source_name' ][ [ , ] ERRORFILE = 'file_name' ][ [ , ] ERRORFILE _DATA _SOURCE = 'data_source_name' ][ [ , ] FIRSTROW = first_row ][ [ , ] FIRE _TRIGGERS ][ [ , ] FORMATFILE _DATA _SOURCE = 'data_source_name' ][ [ , ] KEEPIDENTITY ][ [ , ] KEEPNULLS ][ [ , ] KILOBYTES _PER _BATCH = kilobytes_per_batch ][ [ , ] LASTROW = last_row ][ [ , ] MAXERRORS = max_errors ][ [ , ] ORDER ( { column [ ASC | DESC ] } [ ,...n ] ) ][ [ , ] ROWS _PER _BATCH = rows_per_batch ][ [ , ] ROWTERMINATOR = 'row_terminator' ][ [ , ] TABLOCK ]-- input file format options[ [ , ] FORMAT = 'CSV' ][ [ , ] FIELDQUOTE = 'quote_characters'][ [ , ] FORMATFILE = 'format_file_path' ][ [ , ] FIELDTERMINATOR = 'field_terminator' ][ [ , ] ROWTERMINATOR = 'row_terminator' ])]Argumentsdatabase_name Is the database name in which the specified table or view resides. If not specified, this is the current database.schema_name Is the name of the table or view schema. schema_name is optional if the default schema for the user performing the bulk-import operation is schema of the specified table or view. If schema is not specified and the default schema of the user performing the bulk-import operation is different from the specified table or view, SQL Server returns an error message, and the bulk-import operation is canceled.table_name Is the name of the table or view to bulk import data into. Only views in which all columns refer to the same base table can be used.' data_file ' Is the full path of the data file that contains data to import into the specified table or view. BULK INSERT can import data from a disk or Azure Blob storage (including network, floppy disk, hard disk, and so on).data_file must specify a valid path from the server on which SQL Server is running. If data_file is a remote file, specify the Universal Naming Convention (UNC) name. A UNC name has the form \\Systemname\ShareName\Path\FileName. For example:SQLBULK INSERT Sales.OrdersFROM '\\SystemX\DiskZ\Sales\data\orders.dat';Applies to: SQL Server 2017 (14.x) CTP 1.1 and Azure SQL Database. Beginning with SQL Server 2017 (14.x) CTP1.1, the data_file can be in Azure blob storage. In that case, you need to specify data_source_name option. For an example, see Importing data from a file in Azure blob storage.ImportantAzure SQL Database only supports reading from Azure Blob Storage.' data_source_name ' Applies to: SQL Server 2017 (14.x) CTP 1.1 and Azure SQL Database. Is a named external data source pointing to the Azure Blob storage location of the file that will be imported. The external data source must be created using the TYPE = BLOB_STORAGE option added in SQL Server 2017 (14.x) CTP 1.1.BATCHSIZE =batch_size Specifies the number of rows in a batch. Each batch is copied to the server as one transaction. If this fails, SQL Server commits or rolls back the transaction for every batch. By default, all data in the specified data file is one batch. For information about performance considerations, see "Remarks," later in this topic.CHECK_CONSTRAINTS Specifies that all constraints on the target table or view must be checked during the bulk-import operation. Without the CHECK_CONSTRAINTS option, any CHECK and FOREIGN KEY constraints are ignored, and after the operation, the constraint on the table is marked as not-trusted.At some point, you must examine the constraints on the whole table. If the table was non-empty before the bulk-import operation, the cost of revalidating the constraint may exceed the cost of applying CHECK constraints to the incremental data.A situation in which you might want constraints disabled (the default behavior) is if the input data contains rows that violate constraints. With CHECK constraints disabled, you can import the data and then use Transact-SQL statements to remove the invalid data.The MAXERRORS option does not apply to constraint checking.CODEPAGE = { 'ACP' | 'OEM' | 'RAW' | 'code_page' } Specifies the code page of the data in the data file. CODEPAGE is relevant only if the data contains char, varchar, or text columns with character values greater than 127 or less than 32.ImportantCODEPAGE is not a supported option on Linux for SQL Server 2017 (14.x). For SQL Server 2019 (15.x), only the 'RAW' option is allowed for CODEPAGE.

| CODEPAGE value | Description |
| --- | --- |
| ACP | Columns of char , varchar , or text  data type are converted from the ANSI/Microsoft Windows code page (ISO 1252) to the SQL Server code page. |
| OEM (default) | Columns of char , varchar , or text  data type are converted from the system OEM code page to the SQL Server code page. |
| RAW | No conversion from one code page to another occurs; this is the fastest option. |
| code_page | Specific code page number, for example, 850. ** Important **  Versions prior to SQL Server 2016 (13.x) do not support code page 65001 (UTF-8 encoding). |

DATAFILETYPE = { 'char' | 'native' | 'widechar' | 'widenative' } Specifies that BULK INSERT performs the import operation using the specified data-file type value.

| DATAFILETYPE value | All data represented in: |
| --- | --- |
| char (default) | Character format. |
| native | Native (database) data types. Create the native data file by bulk importing data from SQL Server using the bcp  utility. The native value offers a higher performance alternative to the char value. Native format is recommended when you bulk transfer data between multiple instances of SQL Server using a data file that does not contain any extended/double-byte character set (DBCS) characters. |
| widechar | Unicode characters. |
| widenative | Native (database) data types, except in char , varchar , and text  columns, in which data is stored as Unicode. Create the widenative  data file by bulk importing data from SQL Server using the bcp  utility. The widenative  value offers a higher performance alternative to widechar . If the data file contains ANSI extended characters, specify widenative . |

ERRORFILE ='file_name' Specifies the file used to collect rows that have formatting errors and cannot be converted to an OLE DB rowset. These rows are copied into this error file from the data file "as is."The error file is created when the command is executed. An error occurs if the file already exists. Additionally, a control file that has the extension .ERROR.txt is created. This references each row in the error file and provides error diagnostics. As soon as the errors have been corrected, the data can be loaded. Applies to: SQL Server 2017 (14.x) CTP 1.1\. Beginning with SQL Server 2017 (14.x), the error_file_path can be in Azure blob storage.'errorfile_data_source_name' Applies to: SQL Server 2017 (14.x) CTP 1.1. Is a named external data source pointing to the Azure Blob storage location of the error file that will contain errors found during the import. The external data source must be created using the TYPE = BLOB_STORAGE option added in SQL Server 2017 (14.x) CTP 1.1.FIRSTROW = first_row Specifies the number of the first row to load. The default is the first row in the specified data file. FIRSTROW is 1-based.FIRE_TRIGGERS Specifies that any insert triggers defined on the destination table execute during the bulk-import operation. If triggers are defined for INSERT operations on the target table, they are fired for every completed batch.If FIRE_TRIGGERS is not specified, no insert triggers execute.FORMATFILE_DATA_SOURCE = 'data_source_name' Applies to: SQL Server 2017 (14.x) 1.1\. Is a named external data source pointing to the Azure Blob storage location of the format file that will define the schema of imported data. The external data source must be created using the TYPE = BLOB_STORAGE option added in SQL Server 2017 (14.x) CTP 1.1.KEEPIDENTITY Specifies that identity value or values in the imported data file are to be used for the identity column. If KEEPIDENTITY is not specified, the identity values for this column are verified but not imported and SQL Server automatically assigns unique values based on the seed and increment values specified during table creation. If the data file does not contain values for the identity column in the table or view, use a format file to specify that the identity column in the table or view is to be skipped when importing data; SQL Server automatically assigns unique values for the column.KEEPNULLS Specifies that empty columns should retain a null value during the bulk-import operation, instead of having any default values for the columns inserted.KILOBYTES_PER_BATCH = kilobytes_per_batch Specifies the approximate number of kilobytes (KB) of data per batch as kilobytes_per_batch. By default, KILOBYTES_PER_BATCH is unknown. For information about performance considerations, see "Remarks," later in this topic.LASTROW = last_row Specifies the number of the last row to load. The default is 0, which indicates the last row in the specified data file.MAXERRORS = max_errors Specifies the maximum number of syntax errors allowed in the data before the bulk-import operation is canceled. Each row that cannot be imported by the bulk-import operation is ignored and counted as one error. If max_errors is not specified, the default is 10.ORDER ( { column [ ASC | DESC ] } [ ,... n ] ) Specifies how the data in the data file is sorted. Bulk import performance is improved if the data being imported is sorted according to the clustered index on the table, if any. If the data file is sorted in a different order, that is other than the order of a clustered index key or if there is no clustered index on the table, the ORDER clause is ignored. The column names supplied must be valid column names in the destination table. By default, the bulk insert operation assumes the data file is unordered. For optimized bulk import, SQL Server also validates that the imported data is sorted.n Is a placeholder that indicates that multiple columns can be specified.ROWS_PER_BATCH = rows_per_batch Indicates the approximate number of rows of data in the data file.By default, all the data in the data file is sent to the server as a single transaction, and the number of rows in the batch is unknown to the query optimizer. If you specify ROWS_PER_BATCH (with a value > 0) the server uses this value to optimize the bulk-import operation. The value specified for ROWS_PER_BATCH should approximately the same as the actual number of rows. For information about performance considerations, see "Remarks," later in this topic.TABLOCK Specifies that a table-level lock is acquired for the duration of the bulk-import operation. A table can be loaded concurrently by multiple clients if the table has no indexes and TABLOCK is specified. By default, locking behavior is determined by the table option table lock on bulk load. Holding a lock for the duration of the bulk-import operation reduces lock contention on the table, in some cases can significantly improve performance. For information about performance considerations, see "Remarks," later in this topic.For columnstore index. the locking behavior is different because it is internally divided into multiple rowsets.Each thread loads data exclusively into each rowset by taking a X lock on the rowset allowing parallel data load with concurrent data load sessions. The use of TABLOCK option will cause thread to take an X lock on the table (unlike BU lock for traditional rowsets) which will prevent other concurrent threads to load data concurrently.Input file format optionsFORMAT = 'CSV' Applies to: SQL Server 2017 (14.x) CTP 1.1\. Specifies a comma separated values file compliant to the RFC 4180 standard.SQLBULK INSERT Sales.OrdersFROM '\\SystemX\DiskZ\Sales\data\orders.csv'WITH ( FORMAT ='CSV');FIELDQUOTE = 'field_quote' Applies to: SQL Server 2017 (14.x) CTP 1.1. Specifies a character that will be used as the quote character in the CSV file. If not specified, the quote character (") will be used as the quote character as defined in the RFC 4180 standard.FORMATFILE = 'format_file_path' Specifies the full path of a format file. A format file describes the data file that contains stored responses created by using the bcp utility on the same table or view. The format file should be used if:

*   The data file contains greater or fewer columns than the table or view.
*   The columns are in a different order.
*   The column delimiters vary.
*   There are other changes in the data format. Format files are typically created by using the  bcp utility and modified with a text editor as needed. For more information, see bcp Utility and Create a format file.

Applies to: SQL Server 2017 (14.x) CTP 1.1 and Azure SQL Database. Beginning with SQL Server 2017 (14.x) CTP 1.1, the format_file_path can be in Azure blob storage.FIELDTERMINATOR ='field_terminator' Specifies the field terminator to be used for char and widechar data files. The default field terminator is \t (tab character).ROWTERMINATOR ='row_terminator' Specifies the row terminator to be used for char and widechar data files. The default row terminator is \r\n (newline character).CompatibilityBULK INSERT enforces strict data validation and data checks of data read from a file that could cause existing scripts to fail when they are executed on invalid data. For example, BULK INSERT verifies that:

*   The native representations of float or real data types are valid.
*   Unicode data has an even-byte length.

Data TypesString-to-Decimal Data Type ConversionsThe string-to-decimal data type conversions used in BULK INSERT follow the same rules as the Transact-SQL CONVERT function, which rejects strings representing numeric values that use scientific notation. Therefore, BULK INSERT treats such strings as invalid values and reports conversion errors.To work around this behavior, use a format file to bulk import scientific notation float data into a decimal column. In the format file, explicitly describe the column as real or float data. Example of Importing a Numeric Value that Uses Scientific NotationThis example uses the following table:SQLCREATE TABLE t_float(c1 FLOAT, c2 DECIMAL (5,4));The user wants to bulk import data into the t_float table. The data file, C:\t_float-c.dat, contains scientific notation float data; for example:input8.0000000000000002E-28.0000000000000002E-2However, BULK INSERT cannot import this data directly into t_float, because its second column, c2, uses the decimal data type. Therefore, a format file is necessary. The format file must map the scientific notation float data to the decimal format of column c2.The following format file uses the SQLFLT8 data type to map the second data field to the second column:XML<?xml version="1.0"?><BCPFORMAT xmlns="https://schemas.microsoft.com/sqlserver/2004/bulkload/format" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"><RECORD><FIELD ID="1" xsi:type="CharTerm" TERMINATOR="\t" MAX_LENGTH="30"/><FIELD ID="2" xsi:type="CharTerm" TERMINATOR="\r\n" MAX_LENGTH="30"/> </RECORD> <ROW><COLUMN SOURCE="1" NAME="c1" xsi:type="SQLFLT8"/><COLUMN SOURCE="2" NAME="c2" xsi:type="SQLFLT8"/> </ROW> </BCPFORMAT>To use this format file (using the file name C:\t_floatformat-c-xml.xml) to import the test data into the test table, issue the following Transact-SQL statement:SQLBULK INSERT bulktest..t_floatFROM 'C:\t_float-c.dat' WITH (FORMATFILE='C:\t_floatformat-c-xml.xml');ImportantAzure SQL Database only supports reading from Azure Blob Storage.Data Types for Bulk Exporting or Importing SQLXML DocumentsTo bulk export or import SQLXML data, use one of the following data types in your format file:

| DATA TYPES FOR BULK EXPORTING OR IMPORTING SQLXML DOCUMENTS |
| --- |
| Data type | Effect |
| --- | --- |
| SQLCHAR or SQLVARCHAR | The data is sent in the client code page or in the code page implied by the collation). The effect is the same as specifying the DATAFILETYPE ='char'  without specifying a format file. |
| SQLNCHAR or SQLNVARCHAR | The data is sent as Unicode. The effect is the same as specifying the DATAFILETYPE = 'widechar'  without specifying a format file. |
| SQLBINARY or SQLVARBIN | The data is sent without any conversion. |
|  |  |

The BULK INSERT statement can be executed within a user-defined transaction to import data into a table or view. Optionally, to use multiple matches for bulk importing data, a transaction can specify the BATCHSIZE clause in the BULK INSERT statement. If a multiple-batch transaction is rolled back, every batch that the transaction has sent to SQL Server is rolled back.RestrictionsWhen using a format file with BULK INSERT, you can specify up to 1024 fields only. This is same as the maximum number of columns allowed in a table. If you use a format file with BULK INSERT with a data file that contains more than 1024 fields, BULK INSERT generates the 4822 error. The bcp utility does not have this limitation, so for data files that contain more than 1024 fields, use BULK INSERT without a format file or use the bcp command.Performance ConsiderationsIf the number of pages to be flushed in a single batch exceeds an internal threshold, a full scan of the buffer pool might occur to identify which pages to flush when the batch commits. This full scan can hurt bulk-import performance. A likely case of exceeding the internal threshold occurs when a large buffer pool is combined with a slow I/O subsystem. To avoid buffer overflows on large machines, either do not use the TABLOCK hint (which will remove the bulk optimizations) or use a smaller batch size (which preserves the bulk optimizations).Because computers vary, we recommend that you test various batch sizes with your data load to find out what works best for you.With Azure SQL Database, consider temporarily increasing the performance level of the database or instance prior to the import if you are importing a large volume of data.SecuritySecurity Account Delegation (Impersonation)If a user uses a SQL Server login, the security profile of the SQL Server process account is used. A login using SQL Server authentication cannot be authenticated outside of the Database Engine. Therefore, when a BULK INSERT command is initiated by a login using SQL Server authentication, the connection to the data is made using the security context of the SQL Server process account (the account used by the SQL Server Database Engine service). To successfully read the source data you must grant the account used by the SQL Server Database Engine, access to the source data.In contrast, if a SQL Server user logs on by using Windows Authentication, the user can read only those files that can be accessed by the user account, regardless of the security profile of the SQL Server process.When executing the BULK INSERT statement by using sqlcmd or osql, from one computer, inserting data into SQL Server on a second computer, and specifying a data_file on third computer by using a UNC path, you may receive a 4861 error.To resolve this error, use SQL Server Authentication and specify a SQL Server login that uses the security profile of the SQL Server process account, or configure Windows to enable security account delegation. For information about how to enable a user account to be trusted for delegation, see Windows Help.When importing from Azure Blob storage and the data is not public (anonymous access), create a DATABASE SCOPED CREDENTIAL based on a SAS key which is encrypted with a MASTER KEY, and then create an then create an external database source for use in your BULK INSERT command.PermissionsRequires INSERT and ADMINISTER BULK OPERATIONS permissions. In Azure SQL Database, INSERT and ADMINISTER DATABASE BULK OPERATIONS permissions are required. ADMINISTER BULK OPERATIONS permissions or the bulkadmin role is not supported for SQL Server on Linux. Only the sysadmin can perform bulk inserts for SQL Server on Linux.Additionally, ALTER TABLE permission is required if one or more of the following is true:

*   Constraints exist and the CHECK_CONSTRAINTS option is not specified.

*   Triggers exist and the FIRE_TRIGGER option is not specified.
*   You use the KEEPIDENTITY option to import identity value from data file.

ExamplesA. Using pipes to import data from a fileThe following example imports order detail information into the AdventureWorks2012.Sales.SalesOrderDetail table from the specified data file by using a pipe (|) as the field terminator and |\n as the row terminator.SQLBULK INSERT AdventureWorks2012.Sales.SalesOrderDetailFROM 'f:\orders\lineitem.tbl'WITH(FIELDTERMINATOR =' |', ROWTERMINATOR =' |\n');ImportantAzure SQL Database only supports reading from Azure Blob Storage.B. Using the FIRE_TRIGGERS argumentThe following example specifies the FIRE_TRIGGERS argument.SQLBULK INSERT AdventureWorks2012.Sales.SalesOrderDetailFROM 'f:\orders\lineitem.tbl'WITH(FIELDTERMINATOR =' |', ROWTERMINATOR = ':\n', FIRE_TRIGGERS);ImportantAzure SQL Database only supports reading from Azure Blob Storage.C. Using line feed as a row terminatorThe following example imports a file that uses the line feed as a row terminator such as a UNIX output:SQLDECLARE @bulk_cmd VARCHAR(1000);SET @bulk_cmd = 'BULK INSERT AdventureWorks2012.Sales.SalesOrderDetailFROM ''<drive>:\<path>\<filename>''WITH (ROWTERMINATOR = '''+CHAR(10)+''')';EXEC(@bulk_cmd);Azure SQL Database only supports reading from Azure Blob Storage.D. Specifying a code pageThe following example show how to specify a code page.SQLBULK INSERT MyTableFROM 'D:\data.csv'WITH( CODEPAGE = '65001', DATAFILETYPE = 'char', FIELDTERMINATOR = ',');Azure SQL Database only supports reading from Azure Blob Storage.E. Importing data from a CSV fileThe following example show how to specify a CSV file, skipping the header (first row), using ; as field terminator and 0x0a as line terminator:SQLBULK INSERT Sales.InvoicesFROM '\\share\invoices\inv-2016-07-25.csv'WITH (FORMAT = 'CSV', FIRSTROW=2, FIELDQUOTE = '\', FIELDTERMINATOR = ';', ROWTERMINATOR = '0x0a');Azure SQL Database only supports reading from Azure Blob Storage.F. Importing data from a file in Azure blob storageThe following example shows how to load data from a csv file in an Azure Blob storage location on which you have created a SAS key. The Azure Blob storage location is configured as an external data source. This requires a database scoped credential using a shared access signature that is encrypted using a master key in the user database.SQL--> Optional - a MASTER KEY is not required if a DATABASE SCOPED CREDENTIAL is not required because the blob is configured for public (anonymous) access!CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'YourStrongPassword1';GO--> Optional - a DATABASE SCOPED CREDENTIAL is not required because the blob is configured for public (anonymous) access!CREATE DATABASE SCOPED CREDENTIAL MyAzureBlobStorageCredentialWITH IDENTITY = 'SHARED ACCESS SIGNATURE',SECRET = '******srt=sco&sp=rwac&se=2017-02-01T00:55:34Z&st=2016-12-29T16:55:34Z***************';-- NOTE: Make sure that you don't have a leading ? in SAS token, and-- that you have at least read permission on the object that should be loaded srt=o&sp=r, and-- that expiration period is valid (all dates are in UTC time)CREATE EXTERNAL DATA SOURCE MyAzureBlobStorageWITH ( TYPE = BLOB_STORAGE,LOCATION = 'https://****************.blob.core.windows.net/invoices', CREDENTIAL= MyAzureBlobStorageCredential --> CREDENTIAL is not required if a blob is configured for public (anonymous) access!);BULK INSERT Sales.InvoicesFROM 'inv-2017-12-08.csv'WITH (DATA_SOURCE = 'MyAzureBlobStorage');Azure SQL only supports reading from Azure Blob Storage.G. Importing data from a file in Azure blob storage and specifying an error fileThe following example shows how to load data from a csv file in an Azure blob storage location, which has been configured as an external data source and also specifying an error file. This requires a database scoped credential using a shared access signature. Note that if running on Azure SQL Database, ERRORFILE option should be accompanied by ERRORFILE_DATA_SOURCE otherwise the import might fail with permissions error. The file specified in ERRORFILE should not exist in the container.SQLBULK INSERT Sales.InvoicesFROM 'inv-2017-12-08.csv'WITH (DATA_SOURCE = 'MyAzureInvoices', FORMAT = 'CSV', ERRORFILE = 'MyErrorFile', ERRORFILE_DATA_SOURCE = 'MyAzureInvoices');Extract, transform, and load data on Linux with SSISThis article describes how to run SQL Server Integration Services (SSIS) packages on Linux. SSIS solves complex data integration problems by extracting data from multiple sources and formats, transforming and cleansing the data, and loading the data into multiple destinations.SSIS packages running on Linux can connect to Microsoft SQL Server running on Windows on-premises or in the cloud, on Linux, or in Docker. They can also connect to Azure SQL Database, Azure Synapse Analytics, ODBC data sources, flat files, and other data sources including ADO.NET sources, XML files, and OData services.To run SSIS packages on a Linux computer, first you have to install SQL Server Integration Services. SSIS is not included in the installation of SQL Server for Linux computers.You also have to have a Windows computer to create and maintain packages. The SSIS design and management tools are Windows applications that are not currently available for Linux computers.Run an SSIS packageTo run an SSIS package on a Linux computer, do the following things:

1.  Copy the SSIS package to the Linux computer.
2.  Run the following command:

$ dtexec /F \<package name \> /DE <protection password>Run an encrypted (password-protected) packageThere are three ways to run an SSIS package that's encrypted with a password:

1.  Set the value of the environment variable SSIS_PACKAGE_DECRYPT, as shown in the following example:

SSIS_PACKAGE_DECRYPT=test /opt/ssis/bin/dtexec /f package.dtsx

2.  Specify the /de[crypt] option to enter the password interactively, as shown in the following example:

/opt/ssis/bin/dtexec /f package.dtsx /deEnter decryption password:

3.  Specify the /de option to provide the password on the command line, as shown in the following example. This method is not recommended because it stores the decryption password with the command in the command history.

opt/ssis/bin/dtexec /f package.dtsx /de testWarning: Using /De[crypt] <password> may store decryption password in command history.You can use /De[crypt] instead to enter interactive mode,or use environment variable SSIS_PACKAGE_DECRYPT to set decryption password.Design packagesConnect to ODBC data sources . With SSIS on Linux CTP 2.1 Refresh and later, SSIS packages can use ODBC connections on Linux. This functionality has been tested with the SQL Server and the MySQL ODBC drivers, but is also expected to work with any Unicode ODBC driver that observes the ODBC specification. At design time, you can provide either a DSN or a connection string to connect to the ODBC data; you can also use Windows authentication.Paths . Provide Windows-style paths in your SSIS packages. SSIS on Linux does not support Linux-style paths, but maps Windows-style paths to Linux-style paths at run time. Then, for example, SSIS on Linux maps the Windows-style path C:\test to the Linux-style path /test.Deploy packagesYou can only store packages in the file system on Linux in this release. The SSIS Catalog database and the legacy SSIS service are not available on Linux for package deployment and storage.Schedule packagesYou can use Linux system scheduling tools such as cron to schedule packages. You can't use SQL Agent on Linux to schedule package execution in this release.More info about SSISMicrosoft SQL Server Integration Services (SSIS) is a platform for building high-performance data integration solutions, including extraction, transformation, and loading (ETL) packages for data warehousing.SSIS includes the following features:

*   Graphical tools and wizards for building and debugging packages on Windows
*   A variety of tasks for performing workflow functions such as FTP operations, executing SQL statements, and sending e-mail messages
*   A variety of data sources and destinations for extracting and loading data
*   A variety of transformations for cleaning, aggregating, merging, and copying data
*   Application programming interfaces (APIs) for extending SSIS with your own custom scripts and components

Run SQL Server container images with DockerYou can use Docker to pull and run the SQL Server 2019 container image, mssql-server. Then connect with sqlcmd to create your first database and run queries.The image consists of SQL Server running on Linux based on Ubuntu 18.04. It can be used with the Docker Engine 1.8+ on Linux or on Docker for Mac/Windows. This quickstart specifically focuses on using the SQL Server on Linux image. The Windows image is not covered, but you can learn more about it on the mssql-server-windows-developer Docker Hub page.Prerequisites

*   Docker Engine 1.8+ on any supported Linux distribution or Docker for Mac/Windows. For more information, see Install Docker.
*   Docker  overlay2 storage driver. This is the default for most users. If you find that you are not using this storage provider and need to change, see the instructions and warnings in the docker documentation for configuring overlay2.
*   Minimum of 2 GB of disk space.
*   Minimum of 2 GB of RAM.
*   System requirements for SQL Server on Linux.

Pull and run the 2019 container imageBefore starting the following steps, make sure that you have selected your preferred shell (bash, PowerShell, or cmd) at the top of this article.

1.  Pull the SQL Server 2019 Linux container image from Microsoft Container Registry.

Bashsudo docker pull mcr.microsoft.com/mssql/server:2019-latest

2.  To run the container image with Docker, you can use the following command from a bash shell (Linux/macOS) or elevated PowerShell command prompt.

Bashsudo docker run -e "ACCEPT_EULA=Y" -e "SA_PASSWORD=<YourStrong@Passw0rd>" \-p 1433:1433 --name sql1 -h sql1 \-d mcr.microsoft.com/mssql/server:2019-latestBy default, this creates a container with the Developer edition of SQL Server 2019.The following table provides a description of the parameters in the previous docker run example:

| Parameter | Description |
| --- | --- |
| -e "ACCEPT_EULA=Y" | Set the ACCEPT_EULA  variable to any value to confirm your acceptance of the End-User Licensing Agreement. Required setting for the SQL Server image. |
| -e "SA_PASSWORD=<YourStrong@Passw0rd\>" | Specify your own strong password that is at least 8 characters and meets the SQL Server password requirements. Required setting for the SQL Server image. |
| -p 1433:1433 | Map a TCP port on the host environment (first value) with a TCP port in the container (second value). In this example, SQL Server is listening on TCP 1433 in the container and this is exposed to the port, 1433, on the host. |
| --name sql1 | Specify a custom name for the container rather than a randomly generated one. If you run more than one container, you cannot reuse this same name. |
| -h sql1 | Used to explicitly set the container hostname, if you don't specify it, it defaults to the container ID which is a randomly generated system GUID. |
| mcr.microsoft.com/mssql/server:2019-latest | The SQL Server 2019 Ubuntu Linux container image. |

3.  To view your Docker containers, use the docker ps command.

Bashsudo docker ps -aYou should see output similar to the following screenshot:![Docker ps command output](Image00004.jpg)

4.  If the STATUS column shows a status of Up, then SQL Server is running in the container and listening on the port specified in the PORTS column. If the STATUS column for your SQL Server container shows Exited.

The -h (host name) parameter as discussed above, changes the internal name of the container to a custom value. This changes the internal name of the container to a custom value. This is the name you'll see returned in the following Transact-SQL query:SQLSELECT @@SERVERNAME,SERVERPROPERTY('ComputerNamePhysicalNetBIOS'),SERVERPROPERTY('MachineName'),SERVERPROPERTY('ServerName')Setting -h and --name to the same value is a good way to easily identify the target container.

5.  As a final step, change your SA password because the SA_PASSWORD is visible in ps -eax output and stored in the environment variable of the same name. See steps below.

Change the SA passwordThe SA account is a system administrator on the SQL Server instance that gets created during setup. After creating your SQL Server container, the SA_PASSWORD environment variable you specified is discoverable by running echo $SA_PASSWORD in the container. For security purposes, change your SA password.

1.  Choose a strong password to use for the SA user.
2.  Use docker exec to run sqlcmd to change the password using Transact-SQL. In the following example, replace the old password, <YourStrong!Passw0rd>, and the new password, <YourNewStrong!Passw0rd>, with your own password values.

Bashsudo docker exec -it sql1 /opt/mssql-tools/bin/sqlcmd \-S localhost -U SA -P "<YourStrong@Passw0rd>" \-Q 'ALTER LOGIN SA WITH PASSWORD="<YourNewStrong@Passw0rd>"'Connect to SQL ServerThe following steps use the SQL Server command-line tool, sqlcmd, inside the container to connect to SQL Server.

1.  Use the docker exec -it command to start an interactive bash shell inside your running container. In the following example sql1 is name specified by the --name parameter when you created the container.

Bashsudo docker exec -it sql1 "bash"

2.  Once inside the container, connect locally with sqlcmd. Sqlcmd is not in the path by default, so you have to specify the full path.

Bash/opt/mssql-tools/bin/sqlcmd -S localhost -U SA -P "<YourNewStrong@Passw0rd>"TipYou can omit the password on the command-line to be prompted to enter it.

3.  If successful, you should get to a sqlcmd command prompt: 1>.

Create and query dataThe following sections walk you through using sqlcmd and Transact-SQL to create a new database, add data, and run a query.Create a new databaseThe following steps create a new database named TestDB.

1.  From the sqlcmd command prompt, paste the following Transact-SQL command to create a test database:

SQLCREATE DATABASE TestDB

2.  On the next line, write a query to return the name of all of the databases on your server:

SQLSELECT Name from sys.Databases

3.  The previous two commands were not executed immediately. Type GO on a new line to execute the previous commands:

SQLGOInsert dataNext create a new table, Inventory, and insert two new rows.

1.  From the sqlcmd command prompt, switch context to the new TestDB database:

SQLUSE TestDB

2.  Create new table named Inventory:

SQLCREATE TABLE Inventory (id INT, name NVARCHAR (50), quantity INT)

3.  Insert data into the new table:

SQLINSERT INTO Inventory VALUES (1, 'banana', 150); INSERT INTO Inventory VALUES (2, 'orange', 154);

4.  Type GO to execute the previous commands:

SQLGOSelect dataNow, run a query to return data from the Inventory table.

1.  From the sqlcmd command prompt, enter a query that returns rows from the Inventory table where the quantity is greater than 152:

SQLSELECT * FROM Inventory WHERE quantity > 152;

2.  Execute the command:

SQLGOExit the sqlcmd command prompt

1.  To end your sqlcmd session, type QUIT:

SQLQUIT

2.  To exit the interactive command-prompt in your container, type exit. Your container continues to run after you exit the interactive bash shell.

Connect from outside the containerYou can also connect to the SQL Server instance on your Docker machine from any external Linux, Windows, or macOS tool that supports SQL connections.The following steps use sqlcmd outside of your container to connect to SQL Server running in the container. These steps assume that you already have the SQL Server command-line tools installed outside of your container. The same principles apply when using other tools, but the process of connecting is unique to each tool.

1.  Find the IP address for the machine that hosts your container. On Linux, use ifconfig or ip addr. On Windows, use ipconfig.
2.  For this example, install the sqlcmd tool on your client machine.
3.  Run sqlcmd specifying the IP address and the port mapped to port 1433 in your container. In this example, that is the same port, 1433, on the host machine. If you specified a different mapped port on the host machine, you would use it here. You will also need to open the appropriate inbound port on your firewall to allow the connection.

Bashsqlcmd -S <ip_address>,1433 -U SA -P "<YourNewStrong@Passw0rd>"

4.  Run Transact-SQL commands. When finished, type QUIT.

Remove your containerIf you want to remove the SQL Server container used in this tutorial, run the following commands:Bashsudo docker stop sql1sudo docker rm sql1Docker demoTools and commands for running SQL Server 2019 on LinuxSupported Linux platformsMicrosoft SQL Server 2019 is tested and supported to run on several Linux distribution platforms:

*   Red Hat Enterprise Linux (RHEL)
*   SUSE Linux Enterprise Server (SLES)
*   Ubuntu

Along with the above versions of Linux distributions, SQL Server 2019 is supported in a container scenario using a Docker image.  Running a SQL Server database inside a Docker engine with Linux offers more flexibility, faster recovery, and quicker deployments, including deployments into the Azure cloud. For those becoming familiar with Linux, Docker for Windows or Mac gives you the option to run a Docker engine on your workstation with SQL Server 2019 on Linux.Along with Docker technology, orchestration can be achieved, both managing and deploying SQL Server containers on Linux using Red Hat Open shift or Kubernetes. This includes SQL Server 2019 Big Data Clusters (BDC), fully scalable clusters with SQL Server, Spark, and Hadoop File System (HDFS). BDCs provide the ability to read, write, and analyze big data with T-SQL or Spark, and you can combine big data and relational data, too.While this post has focused on RHEL, SLES, Ubuntu, and container options for Linux, you may have questions regarding other Linux distributions that may be able to run SQL Server 2019, but they’re not supported by Microsoft. Always consider the database server’s use before deciding to run SQL Server 2019 on an unsupported operating system.Tools for Microsoft SQL Server 2019 running on LinuxWith the release of SQL Server 2019, there are more tools that database professionals can use with SQL Server 2019 running on Linux:

*   Windows-based tools—You can use any existing tools that run on Windows to access SQL Server on Linux. This includes SQL Server Management Studio (SSMS), SQL Server Data Tools (SSDT), operational support systems, and third-party tools.
*   Activity Monitor—Use SSMS on Windows to connect remotely and use tools/features such as Activity Monitor commands on a Linux host.
*   Azure Data Studio—Use this cross-platform database tool to manage the Microsoft family of on-premises and cloud data platforms on Windows, MacOS, and Linux. That includes SQL Server 2019 running on Linux. You can also create SQL Server Notebooks in Azure Data Studio, multiple team members to collaborate on projects.
*   Dynamic Management Views (DMVs) —System DMVs collect different types of information about SQL Server, including Linux process information. Use server state information in conjunction with dynamic management functions (DMFs) to monitor the health of a server instance, diagnose problems, and tune performance.
*   Query Store —Use Query Store for insights on query plan choice and performance. It simplifies performance troubleshooting by helping database professionals quickly find performance differences caused by query plan changes.
*   Performance Dashboard —The Performance Dashboard helps you determine if there’s a performance bottleneck on the connected SQL Server instance and provides diagnostic data to help you resolve the problem.
*   mssql-conf  is a configuration script that installs with SQL Server 2019 for Linux.

Command Line Tools for Microsoft SQL Server 2019 on Linux

*   sqlcmd  and Bulk Copy Protocol (BCP)—These command-line tools are natively available on Linux. sqlcmd is a command-line query utility, and BCP is a bulk import-export utility.
*   mssql-scripter —This command-line tool on Linux generates T-SQL scripts for a SQL database running anywhere.
*   mssql-cli —This new, interactive command-line tool written in Python offers several enhancements over sqlcmd in the Terminal environment.

With these tools and command line tools, you’re now ready to run Microsoft SQL Server 2019 on Linux.System Dynamic Management ViewsDynamic management views and functions return server state information that can be used to monitor the health of a server instance, diagnose problems, and tune performance.Dynamic management views and functions return internal, implementation-specific state data. Their schemas and the data they return may change in future releases of SQL Server. Therefore, dynamic management views and functions in future releases may not be compatible with the dynamic management views and functions in this release. For example, in future releases of SQL Server, Microsoft may augment the definition of any dynamic management view by adding columns to the end of the column list. We recommend against using the syntax SELECT * FROM dynamic_management_view_name in production code because the number of columns returned might change and break your application.There are two types of dynamic management views and functions:

*   Server-scoped dynamic management views and functions. These require VIEW SERVER STATE permission on the server.
*   Database-scoped dynamic management views and functions. These require VIEW DATABASE STATE permission on the database.

Querying Dynamic Management ViewsDynamic management views can be referenced in Transact-SQL statements by using two-part, three-part, or four-part names. Dynamic management functions on the other hand can be referenced in Transact-SQL statements by using either two-part or three-part names. Dynamic management views and functions cannot be referenced in Transact-SQL statements by using one-part names.All dynamic management views and functions exist in the sys schema and follow this naming convention dm_*. When you use a dynamic management view or function, you must prefix the name of the view or function by using the sys schema. For example, to query the dm_os_wait_stats dynamic management view, run the following query:SQLSELECT wait_type, wait_time_msFROM sys.dm_os_wait_stats;Required PermissionsTo query a dynamic management view or function requires SELECT permission on object and VIEW SERVER STATE or VIEW DATABASE STATE permission. This lets you selectively restrict access of a user or login to dynamic management views and functions. To do this, first create the user in master and then deny the user SELECT permission on the dynamic management views or functions that you do not want them to access. After this, the user cannot select from these dynamic management views or functions, regardless of database context of the user.Dynamic management views and functions have been organized into the following categories.

*   Always On Availability Groups Dynamic Management Views and Functions (Transact-SQL)

Always On Availability Groups Dynamic Management Views - Functionssys.dm_hadr_auto_page_repairsys.dm_hadr_availability_group_statessys.dm_hadr_availability_replica_cluster_nodessys.dm_hadr_availability_replica_cluster_statessys.dm_hadr_availability_replica_statessys.dm_hadr_clustersys.dm_hadr_cluster_memberssys.dm_hadr_cluster_networkssys.dm_hadr_database_replica_cluster_statessys.dm_hadr_database_replica_statessys.dm_hadr_instance_node_mapsys.dm_hadr_name_id_mapsys.dm_tcp_listener_states

*   Change Data Capture Related Dynamic Management Views (Transact-SQL)

Change Data Capture - sys.dm_cdc_errors

*   Change Tracking Related Dynamic Management Views

Change Tracking - sys.dm_tran_commit_table

*   Common Language Runtime Related Dynamic Management Views (Transact-SQL)

Common Language Runtime Related Dynamic Management Views (Transact-SQL)sys.dm_clr_appdomainssys.dm_clr_propertiessys.dm_clr_loaded_assembliessys.dm_clr_tasks

*   Database Mirroring Related Dynamic Management Views (Transact-SQL)

Database Mirroring - sys.dm_db_mirroring_auto_page_repair

*   Database Related Dynamic Management Views (Transact-SQL)

Database Related Dynamic Management Views (Transact-SQL)sys.dm_db_file_space_usagesys.dm_db_log_infosys.dm_db_log_statssys.dm_db_partition_statssys.dm_db_session_space_usagesys.dm_db_uncontained_entitiessys.dm_db_fts_index_physical_statssys.dm_db_log_space_usagesys.dm_db_page_infosys.dm_db_persisted_sku_featuressys.dm_db_task_space_usage

*   DMV's unique to SQL Database or Azure Synapse Analytics.

sys.dm_db_wait_stats (Azure SQL Database)sys.dm_db_resource_stats (Azure SQL Database)sys.dm_operation_status (Azure SQL Database)sys.dm_database_copies (Azure SQL Database)sys.dm_db_objects_impacted_on_version_change (Azure SQL Database)

*   Execution Related Dynamic Management Views and Functions (Transact-SQL)

Execution Related Dynamic Management Views and Functions (Transact-SQL)sys.dm_exec_background_job_queuesys.dm_exec_cached_plan_dependent_objectssys.dm_exec_compute_node_errorssys.dm_exec_compute_nodessys.dm_exec_cursorssys.dm_exec_describe_first_result_set_for_objectsys.dm_exec_distributed_requestssys.dm_exec_dms_servicessys.dm_exec_external_operationssys.dm_exec_function_statssys.dm_exec_plan_attributessys.dm_exec_query_memory_grantssys.dm_exec_query_optimizer_memory_gatewayssys.dm_exec_query_parallel_workerssys.dm_exec_query_resource_semaphoressys.dm_exec_query_statssys.dm_exec_requestssys.dm_exec_sessionssys.dm_exec_text_query_plansys.dm_exec_valid_use_hintssys.dm_external_script_execution_statssys.dm_exec_background_job_queue_statssys.dm_exec_cached_planssys.dm_exec_compute_node_statussys.dm_exec_connectionssys.dm_exec_describe_first_result_setsys.dm_exec_distributed_request_stepssys.dm_exec_distributed_sql_requestssys.dm_exec_dms_workerssys.dm_exec_external_worksys.dm_exec_input_buffersys.dm_exec_procedure_statssys.dm_exec_query_optimizer_infosys.dm_exec_query_plansys.dm_exec_query_profilessys.dm_exec_query_statistics_xmlsys.dm_exec_query_plan_statssys.dm_exec_session_wait_statssys.dm_exec_sql_textsys.dm_exec_trigger_statssys.dm_exec_xml_handlessys.dm_external_script_requests

*   Extended Events Dynamic Management Views

Extended Events Dynamic Management Viewssys.dm_xe_map_values (Transact-SQL)sys.dm_xe_object_columns (Transact-SQL)sys.dm_xe_objects (Transact-SQL)sys.dm_xe_packages (Transact-SQL)sys.dm_xe_session_event_actions (Transact-SQL)sys.dm_xe_session_events (Transact-SQL)sys.dm_xe_session_object_columns (Transact-SQL)sys.dm_xe_session_targets (Transact-SQL)sys.dm_xe_sessions (Transact-SQL)

*   Filestream and FileTable Dynamic Management Views (Transact-SQL)

Filestream and FileTable Dynamic Management Views (Transact-SQL)Filestream Dynamic Management Views and Functionssys.dm_filestream_file_io_handles (Transact-SQL)
Displays the currently open transactional file handles.sys.dm_filestream_file_io_requests (Transact-SQL)
Displays current file input and file output requests.FileTable Dynamic Management Views and Functionssys.dm_filestream_non_transacted_handles (Transact-SQL)
Displays the currently open non-transactional file handles to FileTable data.Full-Text Search and Semantic Search Dynamic Management Views and Functions (Transact-SQL)Full-Text and Semantic Search Dynamic Management Views - FunctionsThis section contains the following dynamic management views and functions that are related to full-text search and semantic search.Full-Text Search Dynamic Management Views and Functionssys.dm_fts_active_catalogs (Transact-SQL)
Returns information on the full-text catalogs that have some population activity in progress on the server.sys.dm_fts_fdhosts
Returns information on the current activity of the filter daemon host or hosts on the server instance.sys.dm_fts_index_keywords
Returns information about the content of a full-text index for the specified table.sys.dm_fts_index_keywords_by_document
Returns information about the document-level content of a full-text index for the specified table. A given keyword can appear in several documents.sys.dm_fts_index_keywords_by_property
Returns all property-related content in the full-text index of a given table. This includes all data that belongs to any property registered by the search property list associated with that full-text index.sys.dm_fts_index_keywords_position_by_document
Returns the position of keywords in a document.sys.dm_fts_index_population
Returns information about the full-text index populations currently in progress.sys.dm_fts_memory_buffers
Returns information about memory buffers belonging to a specific memory pool that are used as part of a full-text crawl or a full-text crawl range.sys.dm_fts_memory_pools
Returns information about the shared memory pools available to the Full-Text Gatherer component for a full-text crawl or a full-text crawl range.sys.dm_fts_outstanding_batches
Returns information about each full-text indexing batch.sys.dm_fts_parser
Returns the final tokenization result after applying a given word breaker, thesaurus, and stoplist combination to a query string input. The output is equivalent to the output if the specified given query string were issued to the Full-Text Engine.sys.dm_fts_population_ranges
Returns information about the specific ranges related to a full-text index population currently in progress.Semantic Search Dynamic Management Views and Functionssys.dm_fts_semantic_similarity_population (Transact-SQL)
Returns one row of status information about the population of the document similarity index for each similarity index in each table that has an associated semantic index.

*   Geo-Replication Dynamic Management Views and Functions (Azure SQL Database)

Geo-Replication Dynamic Management Views and Functions (Azure SQL Database)sys.geo_replication_links (Azure SQL Database)sys.dm_operation_status (Azure SQL Database)sys.dm_geo_replication_link_status (Azure SQL Database)sys.dm_continuous_copy_status (Azure SQL Database)

*   Index Related Dynamic Management Views and Functions (Transact-SQL)

Index Related Dynamic Management Views and Functions (Transact-SQL)sys.dm_db_column_store_row_group_physical_stats (Transact-SQL)sys.dm_db_index_operational_stats (Transact-SQL)sys.dm_db_index_usage_stats (Transact-SQL)sys.dm_db_missing_index_details (Transact-SQL)sys.dm_db_missing_index_groups (Transact-SQL)sys.dm_db_index_physical_stats (Transact-SQL)sys.dm_db_missing_index_columns (Transact-SQL)sys.dm_db_missing_index_group_stats (Transact-SQL)

*   I O Related Dynamic Management Views and Functions (Transact-SQL)

I/O Related Dynamic Management Views and Functions (Transact-SQL)sys.dm_io_backup_tapes (Transact-SQL)sys.dm_io_pending_io_requests (Transact-SQL)sys.dm_io_cluster_valid_path_names (Transact-SQL)sys.dm_io_cluster_shared_drives (Transact-SQL)sys.dm_io_virtual_file_stats (Transact-SQL)

*   Memory-Optimized Table Dynamic Management Views (Transact-SQL)

Memory-Optimized Table Dynamic Management Views (Transact-SQL)sys.dm_db_xtp_checkpoint_stats (Transact-SQL)sys.dm_db_xtp_gc_cycle_stats (Transact-SQL)sys.dm_db_xtp_index_stats (Transact-SQL)sys.dm_db_xtp_merge_requests (Transact-SQL)sys.dm_db_xtp_nonclustered_index_stats (Transact-SQL)sys.dm_db_xtp_transactions (Transact-SQL)sys.dm_xtp_gc_stats (Transact-SQL)sys.dm_xtp_transaction_stats (Transact-SQL)sys.dm_db_xtp_checkpoint_files (Transact-SQL)sys.dm_db_xtp_hash_index_stats (Transact-SQL)sys.dm_db_xtp_memory_consumers (Transact-SQL)sys.dm_db_xtp_object_stats (Transact-SQL)sys.dm_db_xtp_table_memory_stats (Transact-SQL)sys.dm_xtp_gc_queue_stats (Transact-SQL)sys.dm_xtp_system_memory_consumers (Transact-SQL)Object Catalog ViewsThe following object catalog views are used specifically with In-Memory OLTP.sys.hash_indexes (Transact-SQL)sys.memory_optimized_tables_internal_attributes (Transact-SQL)Internal DMVsThere are additional DMVs that are intended for internal use only, and for which we provide no direct documentation. In the area of memory-optimized tables, undocumented DMVs include the following:

*   sys.dm_xtp_threads
*   sys.dm_xtp_transaction_recent_rows

*   Object Related Dynamic Management Views and Functions (Transact-SQL)

Object Related Dynamic Management Views and Functions (Transact-SQL)sys.dm_db_incremental_stats_propertiessys.dm_db_stats_propertiessys.dm_sql_referencing_entitiessys.dm_db_stats_histogramsys.dm_sql_referenced_entities

*   Query Notifications Related Dynamic Management Views (Transact-SQL)

Query Notifications - sys.dm_qn_subscriptions

*   Replication Related Dynamic Management Views (Transact-SQL)

Replication Related Dynamic Management Views (Transact-SQL)sys.dm_repl_articlessys.dm_repl_tranhashsys.dm_repl_schemassys.dm_repl_traninfo

*   Resource Governor Related Dynamic Management Views (Transact-SQL)

Resource Governor Related Dynamic Management Views (Transact-SQL)sys.dm_resource_governor_configuration (Transact-SQL)sys.dm_resource_governor_external_resource_pool_affinity (Transact-SQL)sys.dm_resource_governor_resource_pool_affinity (Transact-SQL)sys.dm_resource_governor_external_resource_pools (Transact-SQL)sys.dm_resource_governor_resource_pools (Transact-SQL)sys.dm_resource_governor_resource_pool_volumes (Transact-SQL)sys.dm_resource_governor_workload_groups (Transact-SQL)

*   Security-Related Dynamic Management Views and Functions (Transact-SQL)

Security-Related Dynamic Management Views and Functions (Transact-SQL)sys.dm_audit_actions (Transact-SQL)sys.dm_audit_class_type_map (Transact-SQL)sys.dm_cryptographic_provider_algorithms (Transact-SQL)sys.dm_cryptographic_provider_keys (Transact-SQL)sys.dm_cryptographic_provider_properties (Transact-SQL)sys.dm_cryptographic_provider_sessions (Transact-SQL)sys.dm_database_encryption_keys (Transact-SQL)sys.dm_server_audit_status (Transact-SQL)

*   Server-Related Dynamic Management Views and Functions (Transact-SQL)

Server-Related Dynamic Management Views and Functions (Transact-SQL)sys.dm_server_memory_dumpssys.dm_server_registrysys.dm_server_services

*   Service Broker Related Dynamic Management Views (Transact-SQL)

Service Broker Related Dynamic Management Views (Transact-SQL)sys.dm_broker_activated_taskssys.dm_broker_forwarded_messagessys.dm_broker_connectionssys.dm_broker_queue_monitors

*   Spatial Data Related Dynamic Management Views and Functions (Transact-SQL)

Spatial Data - sys.dm_db_objects_disabled_on_compatibility_level_changeExampleThe following example shows a query on sys.dm_db_objects_disabled_on_compatibility_level_change  to find the objects impacted by changing the compatibility level to 120.SQLSELECT * FROM sys.dm_db_objects_disabled_on_compatibility_level_change(120); GO

*   Azure Synapse Analytics and Parallel Data Warehouse Dynamic Management Views (Transact-SQL)

Azure Synapse Analytics (SQL Data Warehouse) and Parallel Data Warehouse Dynamic Management ViewsThe following dynamic management views apply to both Azure Synapse Analytics (SQL Data Warehouse) and Parallel Data Warehouse:sys.dm_pdw_dms_cores (Transact-SQL)sys.dm_pdw_dms_external_work (Transact-SQL)sys.dm_pdw_dms_workers (Transact-SQL)sys.dm_pdw_errors (Transact-SQL)sys.dm_pdw_exec_connections (Transact-SQL)sys.dm_pdw_exec_requests (Transact-SQL)sys.dm_pdw_exec_sessions (Transact-SQL)sys.dm_pdw_hadoop_operations (Transact-SQL)sys.dm_pdw_lock_waits (Transact-SQL)sys.dm_pdw_nodes (Transact-SQL)sys.dm_pdw_nodes_database_encryption_keys (Transact-SQL)sys.dm_pdw_os_threads (Transact-SQL)sys.dm_pdw_request_steps (Transact-SQL)sys.dm_pdw_resource_waits (Transact-SQL)sys.dm_pdw_sql_requests (Transact-SQL)sys.dm_pdw_sys_info (Transact-SQL)sys.dm_pdw_wait_stats (Transact-SQL)sys.dm_pdw_waits (Transact-SQL)Azure Synapse Analytics (SQL Data Warehouse) Dynamic Management ViewsThe following dynamic management views apply to Azure Synapse Analytics (SQL Data Warehouse) only:sys.dm_pdw_nodes_exec_query_plan (Transact-SQL)sys.dm_pdw_nodes_exec_query_profiles (Transact-SQL)sys.dm_pdw_nodes_exec_query_statistics_xml (Transact-SQL)sys.dm_pdw_nodes_exec_sql-text (Transact-SQL)sys.dm_pdw_nodes_exec_text_query_plan (Transact-SQL)sys.dm_workload_management_workload_groups_stats (Transact-SQL) (Preview)Parallel Data Warehouse Dynamic Management ViewsThe following dynamic management views apply to Parallel Data Warehouse only:sys.dm_pdw_component_health_active_alerts (Transact-SQL)sys.dm_pdw_component_health_alerts (Transact-SQL)sys.dm_pdw_component_health_status (Transact-SQL)sys.dm_pdw_diag_processing_stats (Transact-SQL)sys.dm_pdw_network_credentials (Transact-SQL)sys.dm_pdw_node_status (Transact-SQL)sys.dm_pdw_os_event_logs (Transact-SQL)sys.dm_pdw_os_performance_counters (Transact-SQL)sys.dm_pdw_query_stats_xe (Transact-SQL)sys.dm_pdw_query_stats_xe_file (Transact-SQL)

*   SQL Server Operating System Related Dynamic Management Views (Transact-SQL)

SQL Server Operating System Related Dynamic Management Views (Transact-SQL)This section documents dynamic management views (DMV) that are associated with SQL Server Operating System (SQLOS). SQLOS is responsible for managing operating system resources that are specific to SQL Server.

| SQL SERVER OPERATING SYSTEM RELATED DYNAMIC MANAGEMENT VIEWS (TRANSACT-SQL) |
| --- |
| sys.dm_os_buffer_descriptors | sys.dm_os_buffer_pool_extension_configuration |
| sys.dm_os_child_instances | sys.dm_os_cluster_nodes |
| sys.dm_os_cluster_properties | sys.dm_os_dispatcher_pools |
| sys.dm_os_enumerate_fixed_drives | sys.dm_os_host_info |
| sys.dm_os_hosts | sys.dm_os_latch_stats |
| sys.dm_os_loaded_modules | sys.dm_os_memory_brokers |
| sys.dm_os_memory_cache_clock_hands | sys.dm_os_memory_cache_counters |
| sys.dm_os_memory_cache_entries | sys.dm_os_memory_cache_hash_tables |
| sys.dm_os_memory_clerks | sys.dm_os_memory_nodes |
| sys.dm_os_nodes | sys.dm_os_performance_counters |
| sys.dm_os_process_memory | sys.dm_os_schedulers |
| sys.dm_os_server_diagnostics_log_configurations | sys.dm_os_spinlock_stats |
| sys.dm_os_stacks | sys.dm_os_sys_info |
| sys.dm_os_sys_memory | sys.dm_os_tasks |
| sys.dm_os_threads | sys.dm_os_virtual_address_dump |
| sys.dm_os_volume_stats | sys.dm_os_waiting_tasks |
| sys.dm_os_wait_stats | sys.dm_os_windows_info |
| sys.dm_os_workers |  |
|  |  |

The following SQL Server Operating System-related dynamic management views are Identified for informational purposes only. Not supported. Future compatibility is not guaranteed..

| sys.dm_os_function_symbolic_name | sys.dm_os_ring_buffers |
| sys.dm_os_memory_allocations | sys.dm_os_sublatches |
| sys.dm_os_worker_local_storage |  |

*   Stretch Database Dynamic Management Views (Transact-SQL)

There are two types of dynamic management views and functions:

*   Server-scoped dynamic management views and functions. These require VIEW SERVER STATE permission on the server.
*   Database-scoped dynamic management views and functions. These require VIEW DATABASE STATE permission on the database.

Querying Dynamic Management ViewsDynamic management views can be referenced in Transact-SQL statements by using two-part, three-part, or four-part names. Dynamic management functions on the other hand can be referenced in Transact-SQL statements by using either two-part or three-part names. Dynamic management views and functions cannot be referenced in Transact-SQL statements by using one-part names.All dynamic management views and functions exist in the sys schema and follow this naming convention dm_*. When you use a dynamic management view or function, you must prefix the name of the view or function by using the sys schema. For example, to query the dm_os_wait_stats dynamic management view, run the following query:SQLSELECT wait_type, wait_time_msFROM sys.dm_os_wait_stats;

*   Transaction Related Dynamic Management Views and Functions (Transact-SQL)

Transaction Related Dynamic Management Views and Functions (Transact-SQL)sys.dm_tran_active_snapshot_database_transactions (Transact-SQL)sys.dm_tran_current_snapshot (Transact-SQL)sys.dm_tran_database_transactions (Transact-SQL)sys.dm_tran_session_transactions (Transact-SQL)sys.dm_tran_transactions_snapshot (Transact-SQL)sys.dm_tran_version_store_space_usagesys.dm_tran_active_transactions (Transact-SQL)sys.dm_tran_current_transaction (Transact-SQL)sys.dm_tran_locks (Transact-SQL)sys.dm_tran_top_version_generators (Transact-SQL)sys.dm_tran_version_store (Transact-SQL)Monitoring performance by using the Query StoreThe SQL Server Query Store feature provides you with insight on query plan choice and performance. It simplifies performance troubleshooting by helping you quickly find performance differences caused by query plan changes. Query Store automatically captures a history of queries, plans, and runtime statistics, and retains these for your review. It separates data by time windows so you can see database usage patterns and understand when query plan changes happened on the server. You can configure query store using the ALTER DATABASE SET option.If you are using Query Store for just in time workload insights in SQL Server 2016 (13.x), plan to install the performance scalability fixes in KB 4340759  as soon as possible.Enabling the Query StoreQuery Store is not enabled by default for new SQL Server and Azure Synapse Analytics (SQL DW) databases, and is enabled by default for new Azure SQL Database databases.Use the Query Store Page in SQL Server Management Studio

1.  In Object Explorer, right-click a database, and then click Properties.
2.  In the Database Properties dialog box, select the Query Store page.
3.  In the Operation Mode (Requested) box, select Read Write.

Use Transact-SQL StatementsUse the ALTER DATABASE statement to enable the query store for a given database. For example:SQLSET QUERY_STORE = ON (OPERATION_MODE = READ_WRITE);For more syntax options related to the Query Store, see ALTER DATABASE SET Options (Transact-SQL).Information in the Query StoreExecution plans for any specific query in SQL Server typically evolve over time due to a number of different reasons such as statistics changes, schema changes, creation/deletion of indexes, etc. The procedure cache (where cached query plans are stored) only stores the latest execution plan. Plans also get evicted from the plan cache due to memory pressure. As a result, query performance regressions caused by execution plan changes can be non-trivial and time consuming to resolve.Since the Query Store retains multiple execution plans per query, it can enforce policies to direct the Query Processor to use a specific execution plan for a query. This is referred to as plan forcing. Plan forcing in Query Store is provided by using a mechanism similar to the USE PLAN query hint, but it does not require any change in user applications. Plan forcing can resolve a query performance regression caused by a plan change in a very short period of time.Query Store does not collect data for natively compiled stored procedures by default. Use sys.sp_xtp_control_query_exec_stats  to enable data collection for natively compiled stored procedures.Wait stats are another source of information that helps to troubleshoot performance in the Database Engine. For a long time, wait statistics were available only on instance level, which made it hard to backtrack waits to a specific query. Starting with SQL Server 2017 (14.x) and Azure SQL Database, Query Store includes a dimension that tracks wait stats. The following example enables the Query Store to collect wait stats.SQLSET QUERY_STORE = ON ( WAIT_STATS_CAPTURE_MODE = ON );Common scenarios for using the Query Store feature are:

*   Quickly find and fix a plan performance regression by forcing the previous query plan. Fix queries that have recently regressed in performance due to execution plan changes.
*   Determine the number of times a query was executed in a given time window, assisting a DBA in troubleshooting performance resource problems.
*   Identify top n queries (by execution time, memory consumption, etc.) in the past x hours.
*   Audit the history of query plans for a given query.
*   Analyze the resource (CPU, I/O, and Memory) usage patterns for a particular database.
*   Identify top n queries that are waiting on resources.
*   Understand wait nature for a particular query or plan.

The Query Store contains three stores:

*   a  plan store for persisting the execution plan information.
*   a  runtime stats store for persisting the execution statistics information.
*   a  wait stats store for persisting wait statistics information.

The number of unique plans that can be stored for a query in the plan store is limited by the max_plans_per_query configuration option. To enhance performance, the information is written to the stores asynchronously. To minimize space usage, the runtime execution statistics in the runtime stats store are aggregated over a fixed time window. The information in these stores is visible by querying the Query Store catalog views.The following query returns information about queries and plans in the Query Store.SQLSELECT Txt.query_text_id, Txt.query_sql_text, Pl.plan_id, Qry.*FROM sys.query_store_plan AS PlINNER JOIN sys.query_store_query AS QryON Pl.query_id = Qry.query_idINNER JOIN sys.query_store_query_text AS TxtON Qry.query_text_id = Txt.query_text_id ;Use the Regressed Queries featureAfter enabling the Query Store, refresh the database portion of the Object Explorer pane to add the Query Store section.![SQL Server 2016 Query Store tree in SSMS Object Explorer](Image00005.jpg) ![SQL Server 2017 Query Store tree in SSMS Object Explorer](Image00006.jpg)Select Regressed Queries to open the Regressed Queries pane in SQL Server Management Studio. The Regressed Queries pane shows you the queries and plans in the query store. Use the drop-down boxes at the top to filter queries based on various criteria: Duration (ms) (Default), CPU Time (ms), Logical Reads (KB), Logical Writes (KB), Physical Reads (KB), CLR Time (ms), DOP, Memory Consumption (KB), Row Count, Log Memory Used (KB), Temp DB Memory Used (KB), and Wait Time (ms).Select a plan to see the graphical query plan. Buttons are available to view the source query, force and unforce a query plan, toggle between grid and chart formats, compare selected plans (if more than one is selected), and refresh the display.![SQL Server 2016 Regressed Queries in SSMS Object Explorer](Image00007.jpg)To force a plan, select a query and plan, and then click Force Plan. You can only force plans that were saved by the query plan feature and are still retained in the query plan cache.Finding waiting queriesStarting with SQL Server 2017 (14.x) and Azure SQL Database, wait statistics per query over time are available in Query Store.In Query Store, wait types are combined into wait categories. The mapping of wait categories to wait types is available in sys.query_store_wait_stats (Transact-SQL).Select Query Wait Statistics to open the Query Wait Statistics pane in SQL Server Management Studio v18 or higher. The Query Wait Statistics pane shows you a bar chart containing the top wait categories in the Query Store. Use the drop-down at the top to select an aggregate criteria for the wait time: avg, max, min, std dev, and total (default).![SQL Server 2017 Query Wait Statistics in SSMS Object Explorer](Image00008.jpg)Select a wait category by clicking on the bar and a detail view on the selected wait category displays. This new bar chart contains the queries that contributed to that wait category.![SQL Server 2017 Query Wait Statistics detail view in SSMS Object Explorer](Image00009.jpg)Use the drop-down box at the top to filter queries based on various wait time criteria for the selected wait category: avg, max, min, std dev, and total (default). Select a plan to see the graphical query plan. Buttons are available to view the source query, force, and unforce a query plan, and refresh the display.Wait categories are combining different wait types into buckets similar by nature. Different wait categories require a different follow up analysis to resolve the issue, but wait types from the same category lead to very similar troubleshooting experiences, and providing the affected query on top of waits would be the missing piece to complete the majority of such investigations successfully.Here are some examples how you can get more insights into your workload before and after introducing wait categories in Query Store:

| Previous experience | New experience | Action |
| --- | --- | --- |
| High RESOURCE_SEMAPHORE waits per database | High Memory waits in Query Store for specific queries | Find the top memory consuming queries in Query Store. These queries are probably delaying further progress of the affected queries. Consider using MAX_GRANT_PERCENT query hint for these queries, or for the affected queries. |
| High LCK_M_X waits per database | High Lock waits in Query Store for specific queries | Check the query texts for the affected queries and identify the target entities. Look in Query Store for other queries modifying the same entity, which are executed frequently and/or have high duration. After identifying these queries, consider changing the application logic to improve concurrency, or use a less restrictive isolation level. |
| High PAGEIOLATCH_SH waits per database | High Buffer IO waits in Query Store for specific queries | Find the queries with a high number of physical reads in Query Store. If they match the queries with high IO waits, consider introducing an index on the underlying entity, in order to do seeks instead of scans, and thus minimize the IO overhead of the queries. |
| High SOS_SCHEDULER_YIELD waits per database | High CPU waits in Query Store for specific queries | Find the top CPU consuming queries in Query Store. Among them, identify the queries for which high CPU trend correlates with high CPU waits for the affected queries. Focus on optimizing those queries - there could be a plan regression, or perhaps a missing index. |

Configuration OptionsQuery the sys.database_query_store_options view to determine the current options of the Query Store.Related Views, Functions, and ProceduresView and manage Query Store through Management Studio or by using the following views and procedures.Query Store FunctionsFunctions help operations with the Query Store.sys.fn_stmt_sql_handle_from_sql_stmt (Transact-SQL)Query Store Catalog ViewsCatalog views present information about the Query Store.sys.database_query_store_options (Transact-SQL)sys.query_context_settings (Transact-SQL)sys.query_store_plan (Transact-SQL)sys.query_store_query (Transact-SQL)sys.query_store_query_text (Transact-SQL)sys.query_store_runtime_stats (Transact-SQL)sys.query_store_wait_stats (Transact-SQL)sys.query_store_runtime_stats_interval (Transact-SQL)Query Store Stored ProceduresStored procedures configure the Query Store.sp_query_store_flush_db (Transact-SQL)sp_query_store_reset_exec_stats (Transact-SQL)sp_query_store_force_plan (Transact-SQL)sp_query_store_unforce_plan (Transact-SQL)sp_query_store_remove_plan (Transact-SQL)sp_query_store_remove_query (Transact-SQL)sp_query_store_consistency_check (Transact-SQL)1In extreme scenarios Query Store can enter an ERROR state because of internal errors. Starting with SQL Server 2017 (14.x), if this happens, Query Store can be recovered by executing the sp_query_store_consistency_check stored procedure in the affected database. See sys.database_query_store_options for more details described in the actual_state_desc column description.This section provides some guidelines on managing Query Store feature itself.Is Query Store currently active?Query Store stores its data inside the user database and that is why it has size limit (configured with MAX_STORAGE_SIZE_MB). If data in Query Store hits that limit Query Store will automatically change state from read-write to read-only and stop collecting new data.Query sys.database_query_store_options to determine if Query Store is currently active, and whether it is currently collects runtime stats or not.SQLSELECT actual_state, actual_state_desc, readonly_reason,current_storage_size_mb, max_storage_size_mbFROM sys.database_query_store_options;Query Store status is determined by actual_state column. If it's different than the desired status, the readonly_reason column can give you more information. When Query Store size exceeds the quota, the feature will switch to read_only mode.Get Query Store optionsTo find out detailed information about Query Store status, execute following in a user database.SQLSELECT * FROM sys.database_query_store_options;Setting Query Store intervalYou can override interval for aggregating query runtime statistics (default is 60 minutes).SQLALTER DATABASE <database_name>SET QUERY_STORE (INTERVAL_LENGTH_MINUTES = 15);New value for interval is exposed through sys.database_query_store_options view.Query Store space usageTo check current the Query Store size and limit execute the following statement in the user database.SQLSELECT current_storage_size_mb, max_storage_size_mbFROM sys.database_query_store_options;If the Query Store storage is full use the following statement to extend the storage.SQLALTER DATABASE <database_name>SET QUERY_STORE (MAX_STORAGE_SIZE_MB = <new_size>);Set Query Store optionsYou can set multiple Query Store options at once with a single ALTER DATABASE statement.SQLALTER DATABASE <database name >SET QUERY_STORE (OPERATION_MODE = READ_WRITE,CLEANUP_POLICY = (STALE_QUERY_THRESHOLD_DAYS = 30),DATA_FLUSH_INTERVAL_SECONDS = 3000,MAX_STORAGE_SIZE_MB = 500,INTERVAL_LENGTH_MINUTES = 15,SIZE_BASED_CLEANUP_MODE = AUTO ,QUERY_CAPTURE_MODE = AUTO ,MAX_PLANS_PER_QUERY = 1000,WAIT_STATS_CAPTURE_MODE = ON);Cleaning up the spaceQuery Store internal tables are created in the PRIMARY filegroup during database creation and that configuration cannot be changed later. If you are running out of space you might want to clear older Query Store data by using the following statement.SQLALTER DATABASE <db_name> SET QUERY_STORE CLEAR ;Alternatively, you might want to clear up only ad-hoc query data, since it is less relevant for query optimizations and plan analysis but takes up just as much space.Delete ad-hoc queriesThis purges adhoc and internal queries from the query store every 3 minutes so that the query store does not run out of space and remove queries we really need to trackSQLSET NOCOUNT ON-- This purges adhoc and internal queries from the query store every 3 minutes so that the-- query store does not run out of space and remove queries we really need to trackDECLARE @command varchar(1000)SELECT @command = 'IF ''?'' NOT IN(''master'', ''model'', ''msdb'', ''tempdb'') BEGIN USE ?EXEC(''DECLARE @id intDECLARE adhoc_queries_cursor CURSORFORSELECT q.query_idFROM sys.query_store_query_text AS qtJOIN sys.query_store_query AS qON q.query_text_id = qt.query_text_idJOIN sys.query_store_plan AS pON p.query_id = q.query_idJOIN sys.query_store_runtime_stats AS rsON rs.plan_id = p.plan_idWHERE q.is_internal_query = 1 ' -- is it an internal query then we dont care to keep track of it' OR q.object_id = 0' -- if it does not have a valid object_id then it is an adhoc query and we dont care about keeping track of it' GROUP BY q.query_idHAVING MAX(rs.last_execution_time) < DATEADD (minute, -5, GETUTCDATE()) ' -- if it has been more than 5 minutes since the adhoc query ran' ORDER BY q.query_id ;OPEN adhoc_queries_cursor ;FETCH NEXT FROM adhoc_queries_cursor INTO @id;WHILE @@fetch_status = 0BEGINEXEC sp_query_store_remove_query @idFETCH NEXT FROM adhoc_queries_cursor INTO @idENDCLOSE adhoc_queries_cursor ;DEALLOCATE adhoc_queries_cursor;'') END' ;EXEC sp_MSforeachdb @commandYou can define your own procedure with different logic for clearing up data you no longer want.The example above uses the sp_query_store_remove_query extended stored procedure for removing unnecessary data. You can also use:

*   sp_query_store_reset_exec_stats to clear runtime statistics for a given plan.
*   sp_query_store_remove_plan to remove a single plan.

Performance Auditing and TroubleshootingQuery Store keeps a history of compilation and runtime metrics throughout query executions, allowing you to ask questions about your workload.Last n  queries executed on the database?SQLSELECT TOP 10 qt.query_sql_text, q.query_id,qt.query_text_id, p.plan_id, rs.last_execution_timeFROM sys.query_store_query_text AS qtJOIN sys.query_store_query AS qON qt.query_text_id = q.query_text_idJOIN sys.query_store_plan AS pON q.query_id = p.query_idJOIN sys.query_store_runtime_stats AS rsON p.plan_id = rs.plan_idORDER BY rs.last_execution_time DESC ;Number of executions for each query?SQLSELECT q.query_id, qt.query_text_id, qt.query_sql_text,SUM (rs.count_executions) AS total_execution_countFROM sys.query_store_query_text AS qtJOIN sys.query_store_query AS qON qt.query_text_id = q.query_text_idJOIN sys.query_store_plan AS pON q.query_id = p.query_idJOIN sys.query_store_runtime_stats AS rsON p.plan_id = rs.plan_idGROUP BY q.query_id, qt.query_text_id, qt.query_sql_textORDER BY total_execution_count DESC ;The number of queries with the longest average execution time within last hour?SQLSELECT TOP 10 rs.avg_duration, qt.query_sql_text, q.query_id,qt.query_text_id, p.plan_id, GETUTCDATE () AS CurrentUTCTime,rs.last_execution_timeFROM sys.query_store_query_text AS qtJOIN sys.query_store_query AS qON qt.query_text_id = q.query_text_idJOIN sys.query_store_plan AS pON q.query_id = p.query_idJOIN sys.query_store_runtime_stats AS rsON p.plan_id = rs.plan_idWHERE rs.last_execution_time > DATEADD (hour , -1, GETUTCDATE ())ORDER BY rs.avg_duration DESC ;The number of queries that had the biggest average physical I/O reads in last 24 hours, with corresponding average row count and execution count?SQLSELECT TOP 10 rs.avg_physical_io_reads, qt.query_sql_text,q.query_id, qt.query_text_id, p.plan_id, rs.runtime_stats_id,rsi.start_time, rsi.end_time, rs.avg_rowcount, rs.count_executionsFROM sys.query_store_query_text AS qtJOIN sys.query_store_query AS qON qt.query_text_id = q.query_text_idJOIN sys.query_store_plan AS pON q.query_id = p.query_idJOIN sys.query_store_runtime_stats AS rsON p.plan_id = rs.plan_idJOIN sys.query_store_runtime_stats_interval AS rsiON rsi.runtime_stats_interval_id = rs.runtime_stats_interval_idWHERE rsi.start_time >= DATEADD (hour , -24, GETUTCDATE ())ORDER BY rs.avg_physical_io_reads DESC ;Queries with multiple plans? These queries are especially interesting because they are candidates for regressions due to plan choice change. The following query identifies these queries along with all plans:SQLWITH Query_MultPlansAS(SELECT COUNT (*) AS cnt, q.query_idFROM sys.query_store_query_text AS qtJOIN sys.query_store_query AS qON qt.query_text_id = q.query_text_idJOIN sys.query_store_plan AS pON p.query_id = q.query_idGROUP BY q.query_idHAVING COUNT (distinct plan_id) > 1)SELECT q.query_id, object_name(object_id) AS ContainingObject,query_sql_text, plan_id, p.query_plan AS plan_xml,p.last_compile_start_time, p.last_execution_timeFROM Query_MultPlans AS qmJOIN sys.query_store_query AS qON qm.query_id = q.query_idJOIN sys.query_store_plan AS pON q.query_id = p.query_idJOIN sys.query_store_query_text qtON qt.query_text_id = q.query_text_idORDER BY query_id, plan_id;Queries that recently regressed in performance (comparing different point in time)? The following query example returns all queries for which execution time doubled in last 48 hours due to a plan choice change. Query compares all runtime stat intervals side by side.SQLSELECTqt.query_sql_text,q.query_id,qt.query_text_id,rs1.runtime_stats_id AS runtime_stats_id_1,rsi1.start_time AS interval_1,p1.plan_id AS plan_1,rs1.avg_duration AS avg_duration_1,rs2.avg_duration AS avg_duration_2,p2.plan_id AS plan_2,rsi2.start_time AS interval_2,rs2.runtime_stats_id AS runtime_stats_id_2FROM sys.query_store_query_text AS qtJOIN sys.query_store_query AS qON qt.query_text_id = q.query_text_idJOIN sys.query_store_plan AS p1ON q.query_id = p1.query_idJOIN sys.query_store_runtime_stats AS rs1ON p1.plan_id = rs1.plan_idJOIN sys.query_store_runtime_stats_interval AS rsi1ON rsi1.runtime_stats_interval_id = rs1.runtime_stats_interval_idJOIN sys.query_store_plan AS p2ON q.query_id = p2.query_idJOIN sys.query_store_runtime_stats AS rs2ON p2.plan_id = rs2.plan_idJOIN sys.query_store_runtime_stats_interval AS rsi2ON rsi2.runtime_stats_interval_id = rs2.runtime_stats_interval_idWHERE rsi1.start_time > DATEADD (hour , -48, GETUTCDATE ())AND rsi2.start_time > rsi1.start_timeAND p1.plan_id <> p2.plan_idAND rs2.avg_duration > 2*rs1.avg_durationORDER BY q.query_id, rsi1.start_time, rsi2.start_time;If you want to see performance all regressions (not only those related to plan choice change) than just remove condition AND p1.plan_id <> p2.plan_id from the previous query.Queries that are waiting the most? This query will return top 10 queries that wait the most.SQLSELECT TOP 10qt.query_text_id,q.query_id,p.plan_id,sum (total_query_wait_time_ms) AS sum_total_wait_msFROM sys.query_store_wait_stats wsJOIN sys.query_store_plan p ON ws.plan_id = p.plan_idJOIN sys.query_store_query q ON p.query_id = q.query_idJOIN sys.query_store_query_text qt ON q.query_text_id = qt.query_text_idGROUP BY qt.query_text_id, q.query_id, p.plan_idORDER BY sum_total_wait_ms DESCQueries that recently regressed in performance (comparing recent vs. history execution)? The next query compares query execution based periods of execution. In this particular example the query compares execution in recent period (1 hour) vs. history period (last day) and identifies those that introduced additional_duration_workload. This metrics is calculated as a difference between recent average execution and history average execution multiplied by the number of recent executions. It actually represents how much of additional duration recent executions introduced compared to history:SQL--- "Recent" workload - last 1 hourDECLARE @recent_start_time datetimeoffset;DECLARE @recent_end_time datetimeoffset;SET @recent_start_time = DATEADD (hour , -1, SYSUTCDATETIME ());SET @recent_end_time = SYSUTCDATETIME ();--- "History" workloadDECLARE @history_start_time datetimeoffset;DECLARE @history_end_time datetimeoffset;SET @history_start_time = DATEADD (hour , -24, SYSUTCDATETIME ());SET @history_end_time = SYSUTCDATETIME ();WITHhist AS(SELECTp.query_id query_id,ROUND (ROUND (CONVERT (FLOAT, SUM (rs.avg_duration * rs.count_executions)) * 0.001, 2), 2) AS total_duration,SUM (rs.count_executions) AS count_executions,COUNT (distinct p.plan_id) AS num_plansFROM sys.query_store_runtime_stats AS rsJOIN sys.query_store_plan AS p ON p.plan_id = rs.plan_idWHERE (rs.first_execution_time >= @history_start_timeAND rs.last_execution_time < @history_end_time)OR (rs.first_execution_time <= @history_start_timeAND rs.last_execution_time > @history_start_time)OR (rs.first_execution_time <= @history_end_timeAND rs.last_execution_time > @history_end_time)GROUP BY p.query_id),recent AS(SELECTp.query_id query_id,ROUND (ROUND (CONVERT (FLOAT, SUM (rs.avg_duration * rs.count_executions)) * 0.001, 2), 2) AS total_duration,SUM (rs.count_executions) AS count_executions,COUNT (distinct p.plan_id) AS num_plansFROM sys.query_store_runtime_stats AS rsJOIN sys.query_store_plan AS p ON p.plan_id = rs.plan_idWHERE   (rs.first_execution_time >= @recent_start_timeAND rs.last_execution_time < @recent_end_time)OR (rs.first_execution_time <= @recent_start_timeAND rs.last_execution_time > @recent_start_time)OR (rs.first_execution_time <= @recent_end_timeAND rs.last_execution_time > @recent_end_time)GROUP BY p.query_id)SELECTresults.query_id AS query_id,results.query_text AS query_text,results.additional_duration_workload AS additional_duration_workload,results.total_duration_recent AS total_duration_recent,results.total_duration_hist AS total_duration_hist,ISNULL (results.count_executions_recent, 0) AS count_executions_recent,ISNULL (results.count_executions_hist, 0) AS count_executions_histFROM(SELECThist.query_id AS query_id,qt.query_sql_text AS query_text,ROUND (CONVERT (float, recent.total_duration/recent.count_executions-hist.total_duration/hist.count_executions)*(recent.count_executions), 2) AS additional_duration_workload,ROUND (recent.total_duration, 2) AS total_duration_recent,ROUND (hist.total_duration, 2) AS total_duration_hist,recent.count_executions AS count_executions_recent,hist.count_executions AS count_executions_histFROM histJOIN recentON hist.query_id = recent.query_idJOIN sys.query_store_query AS qON q.query_id = hist.query_idJOIN sys.query_store_query_text AS qtON q.query_text_id = qt.query_text_id) AS resultsWHERE additional_duration_workload > 0ORDER BY additional_duration_workload DESCOPTION (MERGE JOIN );Maintaining query performance stabilityFor queries executed multiple times you may notice that SQL Server uses different plans, resulting in different resource utilization and duration. With Query Store you can detect when query performance regressed and determine the optimal plan within a period of interest. You can then force that optimal plan for future query execution.You can also identify inconsistent query performance for a query with parameters (either auto-parameterized or manually parameterized). Among different plans you can identify the plan which is fast and optimal enough for all or most of the parameter values and force that plan, keeping predictable performance for the wider set of user scenarios.Force a plan for a query (apply forcing policy)When a plan is forced for a certain query, SQL Server tries to force the plan in the optimizer. If plan forcing fails, an XEvent is fired and the optimizer is instructed to optimize in the normal way.SQLEXEC sp_query_store_force_plan @query_id = 48, @plan_id = 49;When using sp_query_store_force_plan you can only force plans that were recorded by Query Store as a plan for that query. In other words, the only plans available for a query are those that were already used to execute that query while Query Store was active.Plan forcing support for fast forward and static cursorsStarting with SQL Server 2019 (15.x) and Azure SQL Database (all deployment models), Query Store supports the ability to force query execution plans for fast forward and static Transact-SQL and API cursors. Forcing is supported via sp_query_store_force_plan or through SQL Server Management Studio Query Store reports.Remove plan forcing for a queryTo rely again on the SQL Server query optimizer to calculate the optimal query plan, use sp_query_store_unforce_plan to unforce the plan that was selected for the query.SQLEXEC sp_query_store_unforce_plan @query_id = 48, @plan_id = 49;Best practices with Query StoreThis outlines the best practices for using SQL Server Query Store with your workload.Use the latest SQL Server Management StudioSQL Server Management Studio has a set of user interfaces designed for configuring Query Store and for consuming collected data about your workload.Use Query Performance Insight in Azure SQL DatabaseIf you run Query Store in Azure SQL Database, you can use Query Performance Insight to analyze resource consumption over time. While you can use Management Studio and Azure Data Studio to get detailed resource consumption for all your queries, such as CPU, memory, and I/O, Query Performance Insight gives you a quick and efficient way to determine their impact on overall DTU consumption for your database.This section describes optimal configuration defaults that are designed to ensure reliable operation of the Query Store and dependent features. Default configuration is optimized for continuous data collection, that is minimal time spent in OFF/READ_ONLY states.

| USE QUERY PERFORMANCE INSIGHT IN AZURE SQL DATABASE |
| --- |
| Configuration | Description | Default | Comment |
| --- | --- | --- | --- |
| MAX_STORAGE_SIZE_MB | Specifies the limit for the data space that Query Store can take inside the customer database | 100 | Enforced for new databases |
| INTERVAL_LENGTH_MINUTES | Defines size of time window during which collected runtime statistics for query plans are aggregated and persisted. Every active query plan has at most one row for a period of time defined with this configuration | 60 | Enforced for new databases |
| STALE_QUERY_THRESHOLD_DAYS | Time-based cleanup policy that controls the retention period of persisted runtime statistics and inactive queries | 30 | Enforced for new databases and databases with previous default (367) |
| SIZE_BASED_CLEANUP_MODE | Specifies whether automatic data cleanup takes place when Query Store data size approaches the limit | AUTO | Enforced for all databases |
| QUERY_CAPTURE_MODE | Specifies whether all queries or only a subset of queries are tracked | AUTO | Enforced for all databases |
| FLUSH_INTERVAL_SECONDS | Specifies maximum period during which captured runtime statistics are kept in memory, before flushing to disk | 900 | Enforced for new databases |
|  |  |  |  |

These defaults are automatically applied in the final stage of Query Store activation in all Azure SQL Database. After it's enabled, Azure SQL Database won't change configuration values that are set by customers, unless they negatively impact primary workload or reliable operations of the Query Store.Use Query Store with Elastic Pool databasesYou can use Query Store in all databases without concerns, in even densely packed pools. All issues related to excessive resource usage that might have occurred when Query Store was enabled for the large number of databases in the elastic pools have been resolved.Keep Query Store adjusted to your workloadConfigure Query Store based on your workload and performance troubleshooting requirements. The default parameters are good enough to start, but you should monitor how Query Store behaves over time and adjust its configuration accordingly.![Query Store properties](Image00010.jpg)Here are guidelines to follow for setting parameter values:Max Size (MB): Specifies the limit for the data space that Query Store takes inside your database. This is the most important setting that directly affects the operation mode of Query Store.While Query Store collects queries, execution plans, and statistics, its size in the database grows until this limit is reached. When that happens, Query Store automatically changes the operation mode to read-only and stops collecting new data, which means that your performance analysis is no longer accurate.The default value in SQL Server 2016 (13.x) and SQL Server 2017 (14.x) is 100 MB. This size might not be sufficient if your workload generates a large number of different queries and plans or if you want to keep query history for a longer period of time. Starting with SQL Server 2019 (15.x), the default value is 1 GB. Keep track of current space usage and increase the Max Size (MB) value to prevent Query Store from transitioning to read-only mode.The Max Size (MB) limit isn't strictly enforced. Storage size is checked only when Query Store writes data to disk. This interval is set by the Data Flush Interval (Minutes) option. If Query Store has breached the maximum size limit between storage size checks, it transitions to read-only mode. If Size Based Cleanup Mode is enabled, the cleanup mechanism to enforce the maximum size limit is also triggered.Use Management Studio or execute the following script to get the latest information about Query Store size:SQLUSE [QueryStoreDB];GOSELECT actual_state_desc, desired_state_desc, current_storage_size_mb,max_storage_size_mb, readonly_reasonFROM sys.database_query_store_options;The following script sets a new value for Max Size (MB):SQLALTER DATABASE [QueryStoreDB]SET QUERY_STORE (MAX_STORAGE_SIZE_MB = 1024);Data Flush Interval (Minutes): It defines the frequency to persist collected runtime statistics to disk. It's expressed in minutes in the graphical user interface (GUI), but in Transact-SQL it's expressed in seconds. The default is 900 seconds, which is 15 minutes in the graphical user interface. Consider using a higher value if your workload doesn't generate a large number of different queries and plans, or if you can withstand longer time to persist data before a database shutdown.Use SQL Server Management Studio or Transact-SQL to set a different value for Data Flush Interval:SQLALTER DATABASE [QueryStoreDB]SET QUERY_STORE (DATA_FLUSH_INTERVAL_SECONDS = 900);Statistics Collection Interval: Defines the level of granularity for the collected runtime statistic, expressed in minutes. The default is 60 minutes. Consider using a lower value if you require finer granularity or less time to detect and mitigate issues. Keep in mind that the value directly affects the size of Query Store data. Use SQL Server Management Studio or Transact-SQL to set a different value for Statistics Collection Interval:SQLALTER DATABASE [QueryStoreDB]SET QUERY_STORE (INTERVAL_LENGTH_MINUTES = 60);Stale Query Threshold (Days): Time-based cleanup policy that controls the retention period of persisted runtime statistics and inactive queries, expressed in days. By default, Query Store is configured to keep the data for 30 days, which might be unnecessarily long for your scenario.Avoid keeping historical data that you don't plan to use. This practice reduces changes to read-only status. The size of Query Store data and the time to detect and mitigate the issue will be more predictable. Use Management Studio or the following script to configure time-based cleanup policy:SQLALTER DATABASE [QueryStoreDB]SET QUERY_STORE (CLEANUP_POLICY = (STALE_QUERY_THRESHOLD_DAYS = 90));Size Based Cleanup Mode: Specifies whether automatic data cleanup takes place when Query Store data size approaches the limit. Activate size-based cleanup to make sure that Query Store always runs in read-write mode and collects the latest data.SQLALTER DATABASE [QueryStoreDB]SET QUERY_STORE (SIZE_BASED_CLEANUP_MODE = AUTO );Query Store Capture Mode: Specifies the query capture policy for Query Store.

*   All: Captures all queries. This option is the default in SQL Server 2016 (13.x) and SQL Server 2017 (14.x).
*   Auto: Infrequent queries and queries with insignificant compile and execution duration are ignored. Thresholds for execution count, compile, and runtime duration are internally determined. Starting with SQL Server 2019 (15.x), this is the default option.
*   None: Query Store stops capturing new queries.
*   Custom: Allows additional control and the capability to fine-tune the data collection policy. The new custom settings define what happens during the internal capture policy time threshold. This is a time boundary during which the configurable conditions are evaluated and, if any are true, the query is eligible to be captured by Query Store.

The following script sets QUERY_CAPTURE_MODE to AUTO:SQLALTER DATABASE [QueryStoreDB]SET QUERY_STORE (QUERY_CAPTURE_MODE = AUTO );ExamplesThe following example sets QUERY_CAPTURE_MODE to AUTO and sets other recommended options in SQL Server 2016 (13.x):SQLALTER DATABASE [QueryStoreDB]SET QUERY_STORE = ON(OPERATION_MODE = READ_WRITE,CLEANUP_POLICY = ( STALE_QUERY_THRESHOLD_DAYS = 90 ),DATA_FLUSH_INTERVAL_SECONDS = 900,QUERY_CAPTURE_MODE = AUTO ,MAX_STORAGE_SIZE_MB = 1000,INTERVAL_LENGTH_MINUTES = 60);The following example sets QUERY_CAPTURE_MODE to AUTO and sets other recommended options in SQL Server 2017 (14.x) to include wait statistics:SQLALTER DATABASE [QueryStoreDB]SET QUERY_STORE = ON(OPERATION_MODE = READ_WRITE,CLEANUP_POLICY = ( STALE_QUERY_THRESHOLD_DAYS = 90 ),DATA_FLUSH_INTERVAL_SECONDS = 900,QUERY_CAPTURE_MODE = AUTO ,MAX_STORAGE_SIZE_MB = 1000,INTERVAL_LENGTH_MINUTES = 60,SIZE_BASED_CLEANUP_MODE = AUTO ,MAX_PLANS_PER_QUERY = 200,WAIT_STATS_CAPTURE_MODE = ON);The following example sets QUERY_CAPTURE_MODE to AUTO and sets other recommended options in SQL Server 2019 (15.x), and optionally sets the CUSTOM capture policy with its defaults, instead of the new default AUTO capture mode:SQLALTER DATABASE [QueryStoreDB]SET QUERY_STORE = ON(OPERATION_MODE = READ_WRITE,CLEANUP_POLICY = ( STALE_QUERY_THRESHOLD_DAYS = 90 ),DATA_FLUSH_INTERVAL_SECONDS = 900,MAX_STORAGE_SIZE_MB = 1000,INTERVAL_LENGTH_MINUTES = 60,SIZE_BASED_CLEANUP_MODE = AUTO ,MAX_PLANS_PER_QUERY = 200,WAIT_STATS_CAPTURE_MODE = ON ,QUERY_CAPTURE_MODE = CUSTOM,QUERY_CAPTURE_POLICY = (STALE_CAPTURE_POLICY_THRESHOLD = 24 HOURS ,EXECUTION_COUNT = 30,TOTAL_COMPILE_CPU_TIME_MS = 1000,TOTAL_EXECUTION_CPU_TIME_MS = 100));Start with query performance troubleshootingThe troubleshooting workflow with Query Store is simple, as shown in the following diagram:![Query Store troubleshooting](Image00011.jpg)Enable Query Store by using Management Studio, as described in the previous section, or execute the following Transact-SQL statement:SQLALTER DATABASE [DatabaseOne] SET QUERY_STORE = ON ;It takes some time until Query Store collects the data set that accurately represents your workload. Usually, one day is enough even for very complex workloads. However, you can start exploring the data and identify queries that need your attention immediately after you enable the feature. Go to the Query Store subfolder under the database node in Object Explorer of Management Studio to open troubleshooting views for specific scenarios.Management Studio Query Store views operate with the set of execution metrics, each expressed as any of the following statistic functions:

| SQL Server version | Execution metric | Statistic function |
| --- | --- | --- |
| SQL Server 2016 (13.x) | CPU time, Duration, Execution count, Logical reads, Logical writes, Memory consumption, Physical reads, CLR time, Degree of parallelism (DOP), and Row count | Average, Maximum, Minimum, Standard Deviation, Total |
| SQL Server 2017 (14.x) | CPU time, Duration, Execution count, Logical reads, Logical writes, Memory consumption, Physical reads, CLR time, Degree of parallelism, Row count, Log memory, TempDB memory, and Wait times | Average, Maximum, Minimum, Standard Deviation, Total |

The following graphic shows how to locate Query Store views:![Query Store views](Image00006.jpg)The following table explains when to use each of the Query Store views:

| SQL Server Management Studio view | Scenario |
| --- | --- |
| Regressed Queries | Pinpoint queries for which execution metrics have recently regressed (for example, changed to worse). Use this view to correlate observed performance problems in your application with the actual queries that need to be fixed or improved. |
| Overall Resource Consumption | Analyze the total resource consumption for the database for any of the execution metrics. Use this view to identify resource patterns (daily vs. nightly workloads) and optimize overall consumption for your database. |
| Top Resource Consuming Queries | Choose an execution metric of interest, and identify queries that had the most extreme values for a provided time interval. Use this view to focus your attention on the most relevant queries that have the biggest impact to database resource consumption. |
| Queries With Forced Plans | Lists previously forced plans using Query Store. Use this view to quickly access all currently forced plans. |
| Queries With High Variation | Analyze queries with high-execution variation as it relates to any of the available dimensions, such as Duration, CPU time, IO, and Memory usage, in the desired time interval. Use this view to identify queries with widely variant performance that can be affecting user experience across your applications. |
| Query Wait Statistics | Analyze wait categories that are most active in a database and which queries contribute most to the selected wait category. Use this view to analyze wait statistics and identify queries that might be affecting user experience across your applications.
Applies to: Starting with SQL Server Management Studio v18.0 and SQL Server 2017 (14.x). |
| Tracked Queries | Track the execution of the most important queries in real time. Typically, you use this view when you have queries with forced plans and you want to make sure that query performance is stable. |

When you identify a query with suboptimal performance, your action depends on the nature of the problem.

*   If the query was executed with multiple plans and the last plan is significantly worse than the previous plan, you can use the plan forcing mechanism to force it. SQL Server tries to force the plan in the optimizer. If plan forcing fails, an XEvent is fired and the optimizer is instructed to optimize in the normal way.

![Query Store force plan](Image00012.jpg)The previous graphic might feature different shapes for specific query plans, with the following meanings for each possible status:

| Shape | Meaning |
| --- | --- |
| Circle | Query completed, which means that a regular execution successfully finished. |
| Square | Cancelled, which means that a client-initiated aborted execution. |
| Triangle | Failed, which means that an exception aborted execution. |

Also, the size of the shape reflects the query execution count within the specified time interval. The size increases with a higher number of executions.

*   You might conclude that your query is missing an index for optimal execution. This information is surfaced within the query execution plan. Create the missing index, and check the query performance by usingQuery Store.

![Query Store show plan](Image00013.jpg)If you run your workload on SQL Database, sign up for SQL Database Index Advisor to automatically receive index recommendations.

*   In some cases, you might enforce statistic recompilation if you see that the difference between the estimated and the actual number of rows in the execution plan is significant.
*   Rewrite problematic queries, for example, to take advantage of query parameterization or to implement more optimal logic.

Verify that Query Store collects query data continuouslyQuery Store can silently change the operation mode. Regularly monitor the state of Query Store to ensure that Query Store is operating, and to take action to avoid failures due to preventable causes. Execute the following query to determine the operation mode and view the most relevant parameters:SQLUSE [QueryStoreDB];GOSELECT actual_state_desc, desired_state_desc, current_storage_size_mb,max_storage_size_mb, readonly_reason, interval_length_minutes,stale_query_threshold_days, size_based_cleanup_mode_desc,query_capture_mode_descFROM sys.database_query_store_options;The difference between the actual_state_desc and desired_state_desc indicates that a change of the operation mode occurred automatically. The most common change is for Query Store to silently switch to read-only mode. In extremely rare circumstances, Query Store can end up in the ERROR state because of internal errors.When the actual state is read-only, use the readonly_reason column to determine the root cause. Typically, you find that Query Store transitioned to read-only mode because the size quota was exceeded. In that case, the readonly_reason is set to 65536.Consider the following steps to switch Query Store to read-write mode and activate data collection:

*   Increase the maximum storage size by using the MAX_STORAGE_SIZE_MB option of ALTER DATABASE.
*   Clean up Query Store data by using the following statement:

SQLALTER DATABASE [QueryStoreDB] SET QUERY_STORE CLEAR ;You can apply one or both of these steps by executing the following statement that explicitly changes the operation mode back to read-write:SQLALTER DATABASE [QueryStoreDB]SET QUERY_STORE (OPERATION_MODE = READ_WRITE);Take the following steps to be proactive:

*   You can prevent silent changes of operation mode by applying best practices. Ensure that Query Store size is always below the maximally allowed value to dramatically reduce a chance of transitioning to read-only mode. Activate size-based policy as described in the Configure Query Store section so that Query Store automatically cleans data when the size approaches the limit.
*   To make sure that most recent data is retained, configure time-based policy to remove stale information regularly.
*   Finally, consider setting  Query Store Capture Mode to  Auto because it filters out queries that are usually less relevant for your workload.

SQLALTER DATABASE [QueryStoreDB]SET QUERY_STORE (OPERATION_MODE = READ_WRITE);GOSELECT actual_state_desc, desired_state_desc, current_storage_size_mb,max_storage_size_mb, readonly_reason, interval_length_minutes,stale_query_threshold_days, size_based_cleanup_mode_desc,query_capture_mode_descFROM sys.database_query_store_options;If the problem persists, it indicates that corruption of Query Store data is persisted on the disk.Starting with SQL Server 2017 (14.x), Query Store can be recovered by executing the sp_query_store_consistency_check stored procedure within the affected database. Query Store must be disabled before you attempt the recovery operation. For SQL Server 2016 (13.x), you need to clear the data from Query Store as shown.If the recovery was unsuccessful, you can try clearing Query Store before you set the read-write mode.SQLALTER DATABASE [QueryStoreDB]SET QUERY_STORE CLEAR ;GOALTER DATABASE [QueryStoreDB]SET QUERY_STORE (OPERATION_MODE = READ_WRITE);GOSELECT actual_state_desc, desired_state_desc, current_storage_size_mb,max_storage_size_mb, readonly_reason, interval_length_minutes,stale_query_threshold_days, size_based_cleanup_mode_desc,query_capture_mode_descFROM sys.database_query_store_options;Set the optimal Query Store Capture ModeKeep the most relevant data in Query Store. The following table describes typical scenarios for each Query Store Capture Mode:

| SET THE OPTIMAL QUERY STORE CAPTURE MODE |
| --- |
| Query Store Capture Mode | Scenario |
| --- | --- |
| All | Analyze your workload thoroughly in terms of all queries' shapes and their execution frequencies and other statistics. Identify new queries in your workload.
Detect if ad-hoc queries are used to identify opportunities for user or auto parameterization.
Note: This is the default capture mode in SQL Server 2016 (13.x) and SQL Server 2017 (14.x). |
| Auto | Focus your attention on relevant and actionable queries. An example is those queries that execute regularly or that have significant resource consumption. Note: Starting with SQL Server 2019 (15.x), this is the default capture mode. |
| None | You've already captured the query set that you want to monitor in runtime and you want to eliminate the distractions that other queries might introduce. None is suitable for testing and benchmarking environments.
None is also appropriate for software vendors who ship Query Store configuration configured to monitor their application workload.
None should be used with caution because you might miss the opportunity to track and optimize important new queries. Avoid using None unless you have a specific scenario that requires it. |
| Custom | SQL Server 2019 (15.x) introduces a Custom capture mode under the ALTER DATABASE SET QUERY_STORE command. When enabled, additional Query Store configurations are available under a new Query Store capture policy setting to fine-tune data collection in a specific server. The new custom settings define what happens during the internal capture policy time threshold. This is a time boundary during which the configurable conditions are evaluated and, if any are true, the query is eligible to be captured by Query Store. |
|  |  |

Keep the most relevant data in Query StoreConfigure Query Store to contain only the relevant data so that it runs continuously and provides a great troubleshooting experience with a minimal impact on your regular workload. The following table provides best practices:

| KEEP THE MOST RELEVANT DATA IN QUERY STORE |
| --- |
| Best practice | Setting |
| --- | --- |
| Limit retained historical data. | Configure time-based policy to activate autocleanup. |
| Filter out nonrelevant queries. | Configure Query Store Capture Mode to Auto . |
| Delete less relevant queries when the maximum size is reached. | Activate size-based cleanup policy. |
|  |  |

Avoid using non-parameterized queriesUsing non-parameterized queries when that isn't necessary isn't a best practice. An example is in the case of ad-hoc analysis. Cached plans can't be reused, which forces Query Optimizer to compile queries for every unique query text.Also, Query Store can rapidly exceed the size quota because of a potentially large number of different query texts and consequently a large number of different execution plans with similar shape. As a result, performance of your workload is suboptimal, and Query Store might switch to read-only mode or constantly delete data to try to keep up with the incoming queries.Consider the following options:

*   Parameterize queries where applicable. For example, wrap queries inside a stored procedure or sp_executesql.
*   Use the optimize for ad hoc workloads option if your workload contains many single-use ad-hoc batches with different query plans.
    *   Compare the number of distinct query_hash values with the total number of entries in sys.query_store_query. If the ratio is close to 1, your ad-hoc workload generates different queries.
*   Apply forced parameterization for the database or for a subset of queries if the number of different query plans isn't large.
    *   Use a plan guide to force parameterization only for the selected query.
    *   Configure forced parameterization by using the parameterization database option command, if there are a small number of different query plans in your workload. An example is when the ratio between the count of distinct query_hash and the total number of entries in sys.query_store_query is much less than 1.
*   Set QUERY_CAPTURE_MODE to AUTO to automatically filter out ad-hoc queries with small resource consumption.

Avoid a DROP and CREATE pattern for containing objectsQuery Store associates query entry with a containing object, such as stored procedure, function, and trigger. When you re-create a containing object, a new query entry is generated for the same query text. This prevents you from tracking performance statistics for that query over time and using a plan forcing mechanism. To avoid this situation, use the ALTER <object> process to change a containing object definition whenever it's possible.Check the status of forced plans regularlyPlan forcing is a convenient mechanism to fix performance for the critical queries and make them more predictable. As with plan hints and plan guides, forcing a plan isn't a guarantee that it will be used in future executions. Typically, when database schema changes in a way that objects referenced by the execution plan are altered or dropped, plan forcing starts failing. In that case, SQL Server falls back to query recompilation while the actual forcing failure reason is surfaced in sys.query_store_plan. The following query returns information about forced plans:SQLUSE [QueryStoreDB];GOSELECT p.plan_id, p.query_id, q.object_id as containing_object_id,force_failure_count, last_force_failure_reason_descFROM sys.query_store_plan AS pJOIN sys.query_store_query AS q on p.query_id = q.query_idWHERE is_forced_plan = 1;For a full list of reasons, see sys.query_store_plan. You can also use the query_store_plan_forcing_failed XEvent to track and troubleshoot plan forcing failures.Avoid renaming databases for queries with forced plansExecution plans reference objects by using three-part names like database.schema.object.If you rename a database, plan forcing fails, which causes recompilation in all subsequent query executions.Using Query Store in mission-critical serversThe global trace flags 7745 and 7752 can be used to improve availability of databases by using Query Store.

*   Trace flag 7745 prevents the default behavior where Query Store writes data to disk before SQL Server can be shut down. This means that Query Store data that has been collected but not yet persisted to disk will be lost, up to the time window defined with DATA_FLUSH_INTERVAL_SECONDS.
*   Trace flag 7752 enables asynchronous load of Query Store. This allows a database to become online and queries to be executed before Query Store has been fully recovered. The default behavior is to do a synchronous load of Query Store. The default behavior prevents queries from executing before Query Store has been recovered but also prevents any queries from being missed in the data collection.

If you're using Query Store for just-in-time workload insights in SQL Server 2016 (13.x), plan to install the performance scalability improvements in SQL Server 2016 (13.x) SP2 CU2 (KB 4340759 ) as soon as possible. Without these improvements, when the database is under heavy workloads, spinlock contention may occur and server performance may become slow. In particular, you may see heavy contention on the QUERY_STORE_ASYNC_PERSIST spinlock or SPL_QUERY_STORE_STATS_COOKIE_CACHE spinlock. After this improvement is applied, Query Store will no longer cause spinlock contention.If you're using Query Store for just-in-time workload insights in SQL Server (SQL Server 2016 (13.x) through SQL Server 2017 (14.x)), plan to install the performance scalability improvement in SQL Server 2016 (13.x) SP2 CU15, SQL Server 2017 (14.x) CU22, and SQL Server 2019 (15.x) CU8 as soon as possible. Without this improvement, when the database is under heavy ad-hoc workloads, the Query Store may use a large amount of memory and server performance may become slow. After this improvement is applied, Query Store imposes internal limits to the amount of memory its various components can use, and can automatically change the operation mode to read-only until enough memory has been returned to the Database Engine. Note that Query Store internal memory limits are not documented because they are subject to change.Performance Dashboard built-inWith the new SSMS 17.2, we are releasing the Performance Dashboard embedded as a built-in Standard Report. This means that it is available for any SQL Server instance starting with SQL Server 2008, without any extra downloads or running any extra scripts. Just connect to your server in SSMS and open the Performance Dashboard.How to start it?As seen below, just bring up the Reports context menu at the server level, and select the Standard Reports.[![](Image00014.jpg)](https://msdnshared.blob.core.windows.net/media/2017/08/image35.png)What to use it for?The Performance Report allows a DBA to quickly identify whether there is any current performance bottleneck on the connected SQL Server. And if a bottleneck is found, easily capture additional diagnostic data that may be necessary to resolve the problem. Some common performance problems where the Performance Dashboard can help to solve include:

*   CPU bottlenecks (and what queries are consuming the most CPU)
*   I/O bottlenecks (and what queries are performing the most IO)
*   Index recommendations generated by the query optimizer (missing indexes)
*   Blocking
*   Resource contention (including latch contention)

See below an example where a CPU bottleneck is present:[![](Image00015.jpg)](https://msdnshared.blob.core.windows.net/media/2017/08/image36.png)What has changed since the 2012 release?Besides being completely self-contained in SSMS, we have made a few changes to improve usability:

*   Under Historical Information section:
    *   Added wait categorization to Waits report.
    *   Filtered out all idle and sleep waits from Waits report.
    *   Added new Latches report.
*   Under Miscellaneous Information, added a score column to the report. This report shows potential indexes that the query optimizer identified during query compilation. However, these recommendations should not be taken at face value.
    1.  We recommend that only the indexes with a score greater than 100,000 should be evaluated for creation, as those have the highest anticipated improvement for user queries.
    2.  Also, always evaluate if a new index suggestion is comparable to an existing index in the same table, where the same practical results can be achieved simply by changing an existing index instead of creating a new index. For example, given a new suggested index on columns C1, C2 and C3, first evaluate if there is an existing index over columns C1 and C2\. If so, then it may be preferable to simply add column C3 to the existing index (preserving the order of pre-existing columns) to avoid creating a new index.

What permissions are needed to run the report?This is aimed at sysadmin roles. Other roles require VIEW SERVER STATE and ALTER TRACE permissions.Configure SQL Server on Linux with the mssql-conf toolmssql-conf is a configuration script that installs with SQL Server 2019 (15.x) for Red Hat Enterprise Linux, SUSE Linux Enterprise Server, and Ubuntu. You can use this utility to set the following parameters:

| Parameter | Description |
| --- | --- |
| Agent | Enable SQL Server Agent |
| Collation | Set a new collation for SQL Server on Linux. |
| Customer feedback | Choose whether or not SQL Server sends feedback to Microsoft. |
| Database Mail Profile | Set the default database mail profile for SQL Server on Linux. |
| Default data directory | Change the default directory for new SQL Server database data files (.mdf). |
| Default log directory | Changes the default directory for new SQL Server database log (.ldf) files. |
| Default master database file directory | Changes the default directory for the master database files on existing SQL installation. |
| Default master database file name | Changes the name of master database files. |
| Default dump directory | Change the default directory for new memory dumps and other troubleshooting files. |
| Default error log directory | Changes the default directory for new SQL Server ErrorLog, Default Profiler Trace, System Health Session XE, and Hekaton Session XE files. |
| Default backup directory | Change the default directory for new backup files. |
| Dump type | Choose the type of dump memory dump file to collect. |
| High availability | Enable Availability Groups. |
| Local Audit directory | Set a directory to add Local Audit files. |
| Locale | Set the locale for SQL Server to use. |
| Memory limit | Set the memory limit for SQL Server. |
| Microsoft Distributed Transaction Coordinator | Configure and troubleshoot MSDTC on Linux. |
| MLServices EULAs | Accept R and Python EULAs for mlservices packages. Applies to SQL Server 2019 only. |
| Network settings | Additional network settings for SQL Server. |
| outboundnetworkaccess | Enable outbound network access for mlservices R, Python, and Java extensions. |
| TCP port | Change the port where SQL Server listens for connections. |
| TLS | Configure Transport Level Security. |
| Traceflags | Set the traceflags that the service is going to use. |

Usage tips

*   For Always On Availability Groups and shared disk clusters, always make the same configuration changes on each node.
*   For the shared disk cluster scenario, do not attempt to restart the mssql-server service to apply changes. SQL Server is running as an application. Instead, take the resource offline and then back online.
*   These examples run mssql-conf by specifying the full path: /opt/mssql/bin/mssql-conf. If you choose to navigate to that path instead, run mssql-conf in the context of the current directory: ./mssql-conf.

Enable SQL Server AgentThe sqlagent.enabled setting enables SQL Server Agent. By default, SQL Server Agent is disabled. If sqlagent.enabled is not present in the mssql.conf settings file, then SQL Server internally assumes that SQL Server Agent is disabled.To change this setting, use the following steps:

1.  Enable the SQL Server Agent:

Bashsudo /opt/mssql/bin/mssql-conf set sqlagent.enabled true

2.  Restart the SQL Server service:

Bashsudo systemctl restart mssql-serverSet the default database mail profile for SQL Server on LinuxThe sqlpagent.databasemailprofile allows you to set the default DB Mail profile for email alerts.Bashsudo /opt/mssql/bin/mssql-conf set sqlagent.databasemailprofile <profile_name>SQL Agent error logsThe sqlpagent.errorlogfile and sqlpagent.errorlogginglevel settings allows you to set the SQL Agent log file path and logging level respectively.Bashsudo /opt/mssql/bin/mssql-conf set sqlagent.errorfile <path>SQL Agent logging levels are bitmask values that equal:

*   1 = Errors
*   2 = Warnings
*   4 = Info

If you want to capture all levels, use 7 as the value.Bashsudo /opt/mssql/bin/mssql-conf set sqlagent.errorlogginglevel <level>Change the SQL Server collationThe set-collation option changes the collation value to any of the supported collations.

1.  First backup any user databases on your server.
2.  Then use the sp_detach_db stored procedure to detach the user databases.
3.  Run the set-collation option and follow the prompts:

Bashsudo /opt/mssql/bin/mssql-conf set-collation

4.  The mssql-conf utility will attempt to change to the specified collation value and restart the service. If there are any errors, it rolls back the collation to the previous value.
5.  Restore your user database backups.

For a list of supported collations, run the sys.fn_helpcollations function: SELECT Name from sys.fn_helpcollations().Configure customer feedbackThe telemetry.customerfeedback setting changes whether SQL Server sends feedback to Microsoft or not. By default, this value is set to true for all editions. To change the value, run the following commands:ImportantYou can not turn off customer feedback for free editions of SQL Server, Express and Developer.

1.  Run the mssql-conf script as root with the set command for telemetry.customerfeedback. The following example turns off customer feedback by specifying false.

Bashsudo /opt/mssql/bin/mssql-conf set telemetry.customerfeedback false

2.  Restart the SQL Server service:

Bashsudo systemctl restart mssql-serverChange the default data or log directory locationThe filelocation.defaultdatadir and filelocation.defaultlogdir settings change the location where the new database and log files are created. By default, this location is /var/opt/mssql/data. To change these settings, use the following steps:

1.  Create the target directory for new database data and log files. The following example creates a new /tmp/data directory:

Bashsudo mkdir /tmp/data

2.  Change the owner and group of the directory to the mssql user:

Bashsudo chown mssql /tmp/datasudo chgrp mssql /tmp/data

3.  Use mssql-conf to change the default data directory with the set command:

Bashsudo /opt/mssql/bin/mssql-conf set filelocation.defaultdatadir /tmp/data

4.  Restart the SQL Server service:

Bashsudo systemctl restart mssql-server

5.  Now all the database files for the new databases created will be stored in this new location. If you would like to change the location of the log (.ldf) files of the new databases, you can use the following "set" command:

Bashsudo /opt/mssql/bin/mssql-conf set filelocation.defaultlogdir /tmp/log

6.  This command also assumes that a /tmp/log directory exists, and that it is under the user and group mssql.

Change the default master database file directory locationThe filelocation.masterdatafile and filelocation.masterlogfile setting changes the location where the SQL Server engine looks for the master database files. By default, this location is /var/opt/mssql/data.To change these settings, use the following steps:

1.  Create the target directory for new error log files. The following example creates a new /tmp/masterdatabasedir directory:

Bashsudo mkdir /tmp/masterdatabasedir

2.  Change the owner and group of the directory to the mssql user:

Bashsudo chown mssql /tmp/masterdatabasedirsudo chgrp mssql /tmp/masterdatabasedir

3.  Use mssql-conf to change the default master database directory for the master data and log files with the set command:

Bashsudo /opt/mssql/bin/mssql-conf set filelocation.masterdatafile /tmp/masterdatabasedir/master.mdfsudo /opt/mssql/bin/mssql-conf set filelocation.masterlogfile /tmp/masterdatabasedir/mastlog.ldf

4.  Stop the SQL Server service:

Bashsudo systemctl stop mssql-server

5.  Move the master.mdf and masterlog.ldf:

Bashsudo mv /var/opt/mssql/data/master.mdf /tmp/masterdatabasedir/master.mdfsudo mv /var/opt/mssql/data/mastlog.ldf /tmp/masterdatabasedir/mastlog.ldf

6.  Start the SQL Server service:

Bashsudo systemctl start mssql-serverChange the name of master database filesThe filelocation.masterdatafile and filelocation.masterlogfile setting changes the location where the SQL Server engine looks for the master database files. You can also use this to change the name of the master database and log files.To change these settings, use the following steps:

1.  Stop the SQL Server service:

Bashsudo systemctl stop mssql-server

2.  Use mssql-conf to change the expected master database names for the master data and log files with the set command:

Bashsudo /opt/mssql/bin/mssql-conf set filelocation.masterdatafile /var/opt/mssql/data/masternew.mdfsudo /opt/mssql/bin/mssql-conf set filelocation.mastlogfile /var/opt/mssql/data/mastlognew.ldf

3.  Change the name of the master database data and log files

Bashsudo mv /var/opt/mssql/data/master.mdf /var/opt/mssql/data/masternew.mdfsudo mv /var/opt/mssql/data/mastlog.ldf /var/opt/mssql/data/mastlognew.ldf

4.  Start the SQL Server service:

Bashsudo systemctl start mssql-serverChange the default dump directory locationThe filelocation.defaultdumpdir setting changes the default location where the memory and SQL dumps are generated whenever there is a crash. By default, these files are generated in /var/opt/mssql/log.To set up this new location, use the following commands:

1.  Create the target directory for new dump files. The following example creates a new /tmp/dump directory:

Bashsudo mkdir /tmp/dump

2.  Change the owner and group of the directory to the mssql user:

Bashsudo chown mssql /tmp/dumpsudo chgrp mssql /tmp/dump

3.  Use mssql-conf to change the default data directory with the set command:

Bashsudo /opt/mssql/bin/mssql-conf set filelocation.defaultdumpdir /tmp/dump

4.  Restart the SQL Server service:

Bashsudo systemctl restart mssql-serverChange the default error log file directory locationThe filelocation.errorlogfile setting changes the location where the new error log, default profiler trace, system health session XE and Hekaton session XE files are created. By default, this location is /var/opt/mssql/log. The directory in which SQL errorlog file is set becomes the default log directory for other logs.To change these settings:

1.  Create the target directory for new error log files. The following example creates a new /tmp/logs directory:

Bashsudo mkdir /tmp/logs

2.  Change the owner and group of the directory to the mssql user:

Bashsudo chown mssql /tmp/logssudo chgrp mssql /tmp/logs

3.  Use mssql-conf to change the default errorlog filename with the set command:

Bashsudo /opt/mssql/bin/mssql-conf set filelocation.errorlogfile /tmp/logs/errorlog

4.  Restart the SQL Server service:

Bashsudo systemctl restart mssql-serverThe errorlog.numerrorlogs setting will allow you to specify the number of error logs maintained before cycling the log.Change the default backup directory locationThe filelocation.defaultbackupdir setting changes the default location where the backup files are generated. By default, these files are generated in /var/opt/mssql/data.To set up this new location, use the following commands:

1.  Create the target directory for new backup files. The following example creates a new /tmp/backup directory:

Bashsudo mkdir /tmp/backup

2.  Change the owner and group of the directory to the mssql user:

Bashsudo chown mssql /tmp/backupsudo chgrp mssql /tmp/backup

3.  Use mssql-conf to change the default backup directory with the "set" command:

Bashsudo /opt/mssql/bin/mssql-conf set filelocation.defaultbackupdir /tmp/backup

4.  Restart the SQL Server service:

Bashsudo systemctl restart mssql-serverSpecify core dump settingsIf an exception occurs in one of the SQL Server processes, SQL Server creates a memory dump.There are two options for controlling the type of memory dumps that SQL Server collects: coredump.coredumptype and coredump.captureminiandfull. These relate to the two phases of core dump capture.The first phase capture is controlled by the coredump.coredumptype setting, which determines the type of dump file generated during an exception. The second phase is enabled when the coredump.captureminiandfull setting. If coredump.captureminiandfull is set to true, the dump file specified by coredump.coredumptype is generated and a second mini dump is also generated. Setting coredump.captureminiandfull to false disables the second capture attempt.

1.  Decide whether to capture both mini and full dumps with the coredump.captureminiandfull setting.

Bashsudo /opt/mssql/bin/mssql-conf set coredump.captureminiandfull <true or false>Default: false

2.  Specify the type of dump file with the coredump.coredumptype setting.

Bashsudo /opt/mssql/bin/mssql-conf set coredump.coredumptype <dump_type>Default: miniplusThe following table lists the possible coredump.coredumptype values.

| Type | Description |
| --- | --- |
| mini | Mini is the smallest dump file type. It uses the Linux system information to determine threads and modules in the process. The dump contains only the host environment thread stacks and modules. It does not contain indirect memory references or globals. |
| miniplus | MiniPlus is similar to mini, but it includes additional memory. It understands the internals of SQLPAL and the host environment, adding the following memory regions to the dump: - Various globals
- All memory above 64TB
- All named regions found in /proc/$pid/maps
- Indirect memory from threads and stacks
- Thread information
- Associated Teb's and Peb's
- Module Information
- VMM and VAD tree |
| filtered | Filtered uses a subtraction-based design where all memory in the process is included unless specifically excluded. The design understands the internals of SQLPAL and the host environment, excluding certain regions from the dump. |
| full | Full is a complete process dump that includes all regions located in /proc/$pid/maps . This is not controlled by coredump.captureminiandfull  setting. |

High AvailabilityThe hadr.hadrenabled option enables availability groups on your SQL Server instance. The following command enables availability groups by setting hadr.hadrenabled to 1\. You must restart SQL Server for the setting to take effect.Bashsudo /opt/mssql/bin/mssql-conf set hadr.hadrenabled  1sudo systemctl restart mssql-serverSet local audit directoryThe telemetry.userrequestedlocalauditdirectory setting enables Local Audit and lets you set the directory where the Local Audit logs are created.

1.  Create a target directory for new Local Audit logs. The following example creates a new /tmp/audit directory:

Bashsudo mkdir /tmp/audit

2.  Change the owner and group of the directory to the mssql user:

Bashsudo chown mssql /tmp/auditsudo chgrp mssql /tmp/audit

3.  Run the mssql-conf script as root with the set command for telemetry.userrequestedlocalauditdirectory:

Bashsudo /opt/mssql/bin/mssql-conf set telemetry.userrequestedlocalauditdirectory /tmp/audit

4.  Restart the SQL Server service:

Bashsudo systemctl restart mssql-serverChange the SQL Server localeThe language.lcid setting changes the SQL Server locale to any supported language identifier (LCID).

1.  The following example changes the locale to French (1036):

Bashsudo /opt/mssql/bin/mssql-conf set language.lcid 1036

2.  Restart the SQL Server service to apply the changes:

Bashsudo systemctl restart mssql-serverSet the memory limitThe memory.memorylimitmb setting controls the amount physical memory (in MB) available to SQL Server. The default is 80% of the physical memory.

1.  Run the mssql-conf script as root with the set command for memory.memorylimitmb. The following example changes the memory available to SQL Server to 3.25 GB (3328 MB).

Bashsudo /opt/mssql/bin/mssql-conf set memory.memorylimitmb 3328

2.  Restart the SQL Server service to apply the changes:

Bashsudo systemctl restart mssql-serverAdditional memory settingsThe following options are available to the memory settings.

| Option | Description |
| --- | --- |
| memory.disablememorypressure | SQL Server disable memory pressure. Values can be true or false. |
| memory.memory_optimized | Enable or disable SQL Server memory optimized features - persistent memory file enlightenment, memory protection. Values can be true or false. |

Configure MSDTCThe network.rpcport and distributedtransaction.servertcpport settings are used to configure the Microsoft Distributed Transaction Coordinator (MSDTC). To change these settings, run the following commands:

1.  Run the mssql-conf script as root with the set command for "network.rpcport":

Bashsudo /opt/mssql/bin/mssql-conf set network.rpcport <rcp_port>

2.  Then set the "distributedtransaction.servertcpport" setting:

Bashsudo /opt/mssql/bin/mssql-conf set distributedtransaction.servertcpport <servertcpport_port>In addition to setting these values, you must also configure routing and update the firewall for port 135.There are several other settings for mssql-conf that you can use to monitor and troubleshoot MSDTC. The following table briefly describes these settings.

| CONFIGURE MSDTC |
| --- |
| mssql-conf setting | Description |
| --- | --- |
| distributedtransaction.allowonlysecurerpccalls | Configure secure only RPC calls for distributed transactions |
| distributedtransaction.fallbacktounsecurerpcifnecessary | Configure security only RPC calls for distributed transactions |
| distributedtransaction.maxlogsize | DTC transaction log file size in MB. Default is 64MB |
| distributedtransaction.memorybuffersize | Circular buffer size in which traces are stored. This size is in MB and default is 10MB |
| distributedtransaction.servertcpport | MSDTC rpc server port |
| distributedtransaction.trace_cm | Traces in the connection manager |
| distributedtransaction.trace_contact | Traces the contact pool and contacts |
| distributedtransaction.trace_gateway | Traces Gateway source |
| distributedtransaction.trace_log | Log tracing |
| distributedtransaction.trace_misc | Traces that cannot be categorized into the other categories |
| distributedtransaction.trace_proxy | Traces that are generated in the MSDTC proxy |
| distributedtransaction.trace_svc | Traces service and .exe file startup |
| distributedtransaction.trace_trace | The trace infrastructure itself |
| distributedtransaction.trace_util | Traces utility routines that are called from multiple locations |
| distributedtransaction.trace_xa | XA Transaction Manager (XATM) tracing source |
| distributedtransaction.tracefilepath | Folder in which trace files should be stored |
| distributedtransaction.turnoffrpcsecurity | Enable or disable RPC security for distributed transactions |
|  |  |

Accept MLServices EULAsAdding machine learning R or Python packages to the database engine requires that you accept the licensing terms for open-source distributions of R and Python. The following table enumerates all available commands or options related to mlservices EULAs. The same EULA parameter is used for R and Python, depending on what you installed.Bash# For all packages: database engine and mlservices# Setup prompts for mlservices EULAs, which you need to acceptsudo /opt/mssql/bin/mssql-conf setup# Add R or Python to an existing installationsudo /opt/mssql/bin/mssql-conf setup accept-eula-ml# Alternative valid syntax# Adds the EULA section to the INI and sets acceptulam to yessudo /opt/mssql/bin/mssql-conf set EULA accepteulaml Y# Rescind EULA acceptance and removes the settingsudo /opt/mssql/bin/mssql-conf unset EULA accepteulamlYou can also add EULA acceptance directly to the mssql.conf file:ini[EULA]accepteula = Yaccepteulaml = YEnable outbound network accessOutbound network access for R, Python, and Java extensions in the SQL Server Machine Learning Services feature is disabled by default. To enable outbound requests, set the "outboundnetworkaccess" Boolean property using mssql-conf.After setting the property, restart SQL Server Launchpad service to read the updated values from the INI file. A restart message reminds you whenever an extensibility-related setting is modified.Bash# Adds the extensibility section and property.# Sets "outboundnetworkaccess" to true.# This setting is required if you want to access data or operations off the server.sudo /opt/mssql/bin/mssql-conf set extensibility outboundnetworkaccess 1# Turns off network access but preserves the settingsudo /opt/mssql/bin/mssql-conf set extensibility outboundnetworkaccess 0# Removes the setting and rescinds network accesssudo /opt/mssql/bin/mssql-conf unset extensibility.outboundnetworkaccessYou can also add "outboundnetworkaccess" directly to the mssql.conf file:ini[extensibility]outboundnetworkaccess = 1Change the TCP portThe network.tcpport setting changes the TCP port where SQL Server listens for connections. By default, this port is set to 1433\. To change the port, run the following commands:

1.  Run the mssql-conf script as root with the "set" command for "network.tcpport":

Bashsudo /opt/mssql/bin/mssql-conf set network.tcpport <new_tcp_port>

2.  Restart the SQL Server service:

Bashsudo systemctl restart mssql-server

3.  When connecting to SQL Server now, you must specify the custom port with a comma (,) after the hostname or IP address. For example, to connect with SQLCMD, you would use the following command:

Bashsqlcmd -S localhost,<new_tcp_port> -U test -P testSpecify TLS settingsThe following options configure TLS for an instance of SQL Server running on Linux.

| SPECIFY TLS SETTINGS |
| --- |
| Option | Description |
| --- | --- |
| network.forceencryption | If 1, then SQL Server forces all connections to be encrypted. By default, this option is 0. |
| network.tlscert | The absolute path to the certificate file that SQL Server uses for TLS. Example: /etc/ssl/certs/mssql.pem The certificate file must be accessible by the mssql account. Microsoft recommends restricting access to the file using chown mssql:mssql <file>; chmod 400 <file>. |
| network.tlskey | The absolute path to the private key file that SQL Server uses for TLS. Example: /etc/ssl/private/mssql.key The certificate file must be accessible by the mssql account. Microsoft recommends restricting access to the file using chown mssql:mssql <file>; chmod 400 <file>. |
| network.tlsprotocols | A comma-separated list of which TLS protocols are allowed by SQL Server. SQL Server always attempts to negotiate the strongest allowed protocol. If a client does not support any allowed protocol, SQL Server rejects the connection attempt. For compatibility, all supported protocols are allowed by default (1.2, 1.1, 1.0). If your clients support TLS 1.2, Microsoft recommends allowing only TLS 1.2. |
| network.tlsciphers | Specifies which ciphers are allowed by SQL Server for TLS. This string must be formatted per OpenSSL's cipher list format. In general, you should not need to change this option. By default, the following ciphers are allowed:
ECDHE-ECDSA-AES128-GCM-SHA256:ECDHE-ECDSA-AES256-GCM-SHA384:ECDHE-RSA-AES128-GCM-SHA256:ECDHE-RSA-AES256-GCM-SHA384:ECDHE-ECDSA-AES128-SHA256:ECDHE-ECDSA-AES256-SHA384:ECDHE-RSA-AES128-SHA256:ECDHE-RSA-AES256-SHA384:ECDHE-ECDSA-AES256-SHA:ECDHE-ECDSA-AES128-SHA:ECDHE-RSA-AES256-SHA:ECDHE-RSA-AES128-SHA:AES256-GCM-SHA384:AES128-GCM-SHA256:AES256-SHA256:AES128-SHA256:AES256-SHA:AES128-SHA |
| network.kerberoskeytabfile | Path to the Kerberos keytab file |
|  |  |

Network settingsThe following options are additional network settings configurable using mssql-conf.

| NETWORK SETTINGS |
| --- |
| Option | Description |
| --- | --- |
| network.disablesssd | Disable querying SSSD for AD account information and default to LDAP calls. Values can be true or false. |
| network.enablekdcfromkrb5conf | Enable looking up KDC information from krb5.conf. Values can be true or false. |
| network.forcesecureldap | Force using LDAPS to contact domain controller. Values can be true or false. |
| network.ipaddress | IP address for incoming connections. |
| network.kerberoscredupdatefrequency | Time in seconds between checks for kerberos credentials that need to be updated. Value is an integer. |
| network.privilegedadaccount | Privileged AD user to use for AD authentication. Value is <username>. |
| uncmapping | Maps UNC path to a local path. For example, sudo /opt/mssql/bin/mssql-conf set uncmapping //servername/sharename /tmp/folder. |
|  |  |

Enable/Disable traceflagsThis traceflag option enables or disables traceflags for the startup of the SQL Server service. To enable/disable a traceflag, use the following commands:

1.  Enable a traceflag using the following command. For example, for Traceflag 1234:

Bashsudo /opt/mssql/bin/mssql-conf traceflag 1234 on

2.  You can enable multiple traceflags by specifying them separately:

Bashsudo /opt/mssql/bin/mssql-conf traceflag 2345 3456 on

3.  In a similar way, you can disable one or more enabled traceflags by specifying them and adding the off parameter:

Bashsudo /opt/mssql/bin/mssql-conf traceflag 1234 2345 3456 off

4.  Restart the SQL Server service to apply the changes:

Bashsudo systemctl restart mssql-serverRemove a settingTo unset any setting made with mssql-conf set, call mssql-conf with the unset option and the name of the setting. This clears the setting, effectively returning it to its default value.

1.  The following example clears the network.tcpport option.

Bashsudo /opt/mssql/bin/mssql-conf unset network.tcpport

2.  Restart the SQL Server service.

Bashsudo systemctl restart mssql-serverView current settingsTo view any configured settings, run the following command to output the contents of the mssql.conf file:Bashsudo cat /var/opt/mssql/mssql.confAny settings not shown in this file are using their default values. The next section provides a sample mssql.conf file.mssql.conf formatThe following /var/opt/mssql/mssql.conf file provides an example for each setting. You can use this format to manually make changes to the mssql.conf file as needed. If you do manually change the file, you must restart SQL Server before the changes are applied. To use the mssql.conf file with Docker, you must have Docker persist your data. First add a complete mssql.conf file to your host directory and then run the container.ini[EULA]accepteula = Yaccepteulaml = Y[coredump]captureminiandfull = truecoredumptype = full[distributedtransaction]servertcpport = 51999[filelocation]defaultbackupdir = /var/opt/mssql/data/defaultdatadir = /var/opt/mssql/data/defaultdumpdir = /var/opt/mssql/data/defaultlogdir = /var/opt/mssql/data/[hadr]hadrenabled = 0[language]lcid = 1033[memory]memorylimitmb = 4096[network]forceencryption = 0ipaddress = 10.192.0.0kerberoskeytabfile = /var/opt/mssql/secrets/mssql.keytabrpcport = 13500tcpport = 1401tlscert = /etc/ssl/certs/mssql.pemtlsciphers = ECDHE-ECDSA-AES128-GCM-SHA256:ECDHE-ECDSA-AES256-GCM-SHA384:ECDHE-RSA-AES128-GCM-SHA256:ECDHE-RSA-AES256-GCM-SHA384:ECDHE-ECDSA-AES128-SHA256:ECDHE-ECDSA-AES256-SHA384:ECDHE-RSA-AES128-SHA256:ECDHE-RSA-AES256-SHA384:ECDHE-ECDSA-AES256-SHA:ECDHE-ECDSA-AES128-SHA:ECDHE-RSA-AES256-SHA:ECDHE-RSA-AES128-SHA:AES256-GCM-SHA384:AES128-GCM-SHA256:AES256-SHA256:AES128-SHA256:AES256-SHA:AES128-SHAtlskey = /etc/ssl/private/mssql.keytlsprotocols = 1.2,1.1,1.0[sqlagent]databasemailprofile = defaulterrorlogfile = /var/opt/mssql/log/sqlagentlog.logerrorlogginglevel = 7[telemetry]customerfeedback = trueuserrequestedlocalauditdirectory = /tmp/audit[traceflag]traceflag0 = 1204traceflag1 = 2345traceflag = 3456Install sqlcmd and bcp the SQL Server command-line tools on LinuxThe following steps install the command-line tools, Microsoft ODBC drivers, and their dependencies. The mssql-tools package contains:

*   sqlcmd: Command-line query utility.
*   bcp: Bulk import-export utility.

Install the tools for your platform:Install tools on RHEL 8Use the following steps to install the mssql-tools on Red Hat Enterprise Linux.

1.  Enter superuser mode.

Bashsudo su

2.  Download the Microsoft Red Hat repository configuration file.

Bashcurl https://packages.microsoft.com/config/rhel/8/prod.repo > /etc/yum.repos.d/msprod.repo

3.  Exit superuser mode.

Bashexit

4.  If you had a previous version of mssql-tools installed, remove any older unixODBC packages.

Bashsudo yum remove mssql-tools unixODBC-utf16-devel

5.  Run the following commands to install mssql-tools with the unixODBC developer package.

Bashsudo yum install mssql-tools unixODBC-develBashsudo yum check-updatesudo yum update mssql-tools

6.  Optional: Add /opt/mssql-tools/bin/ to your PATH environment variable in a bash shell.

To make sqlcmd/bcp accessible from the bash shell for login sessions, modify your PATH in the ~/.bash_profile file with the following command:Bashecho 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bash_profileTo make sqlcmd/bcp accessible from the bash shell for interactive/non-login sessions, modify the PATH in the ~/.bashrc file with the following command:Bashecho 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bashrcsource ~/.bashrcInstall tools on Ubuntu 16.04Use the following steps to install the mssql-tools on Ubuntu.Import the public repository GPG keys.Bashcurl https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -

1.  Register the Microsoft Ubuntu repository.

Bashcurl https://packages.microsoft.com/config/ubuntu/16.04/prod.list | sudo tee /etc/apt/sources.list.d/msprod.list

2.  Update the sources list and run the installation command with the unixODBC developer package.

Bashsudo apt-get updatesudo apt-get install mssql-tools unixodbc-devTo update to the latest version of mssql-tools run the following commands:Bashsudo apt-get updatesudo apt-get install mssql-tools

3.  Optional: Add /opt/mssql-tools/bin/ to your PATH environment variable in a bash shell.

To make sqlcmd/bcp accessible from the bash shell for login sessions, modify your PATH in the ~/.bash_profile file with the following command:Bashecho 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bash_profileTo make sqlcmd/bcp accessible from the bash shell for interactive/non-login sessions, modify the PATH in the ~/.bashrc file with the following command:Bashecho 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bashrcsource ~/.bashrcInstall tools on SLES 12Use the following steps to install the mssql-tools on SUSE Linux Enterprise Server.

1.  Add the Microsoft SQL Server repository to Zypper.

Bashsudo zypper addrepo -fc https://packages.microsoft.com/config/sles/12/prod.reposudo zypper --gpg-auto-import-keys refresh

2.  Install mssql-tools with the unixODBC developer package.

Bashsudo zypper install mssql-tools unixODBC-develTo update to the latest version of mssql-tools run the following commands:Bashsudo zypper refreshsudo zypper update mssql-tools

3.  Optional: Add /opt/mssql-tools/bin/ to your PATH environment variable in a bash shell.

To make sqlcmd/bcp accessible from the bash shell for login sessions, modify your PATH in the ~/.bash_profile file with the following command:Bashecho 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bash_profileTo make sqlcmd/bcp accessible from the bash shell for interactive/non-login sessions, modify the PATH in the ~/.bashrc file with the following command:Bashecho 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bashrcsource ~/.bashrcInstall tools on macOSA preview of sqlcmd and bcp is now available on macOS.Install Homebrew  if you don't have it already:

*   /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"

To install the tools for Mac El Capitan and Sierra, use the following commands:Bash# brew untap microsoft/mssql-preview if you installed the preview versionbrew tap microsoft/mssql-release https://github.com/Microsoft/homebrew-mssql-releasebrew updatebrew install mssql-tools#for silent install:#HOMEBREW_NO_ENV_FILTERING=1 ACCEPT_EULA=y brew install mssql-toolsDockerIf you run SQL Server in a Docker container, the SQL Server command-line tools are already included in the SQL Server Linux container image. If you attach to a running container with an interactive bash shell, you can run the tools locally.Offline installationIf your Linux machine does not have access to the online repositories used in the previous sections, you can download the package files directly. These packages are located in the Microsoft repository, https://packages.microsoft.com.

1.  First, locate and copy the mssql-tools package for your Linux distribution:

| Linux distribution | mssql-tools package location |
| --- | --- |
| Red Hat | https://packages.microsoft.com/rhel/7.3/prod |
| SLES | https://packages.microsoft.com/sles/12/prod |
| Ubuntu 16.04 | https://packages.microsoft.com/ubuntu/16.04/prod/pool/main/m/mssql-tools |

2.  Also locate and copy the msodbcsql package, which is a dependency. The msodbcsql package also has a dependency on either unixODBC-devel (Red Hat and SLES) or unixodbc-dev (Ubuntu). The location of the msodbcsql packages are listed in the following table:

| Linux distribution | ODBC packages location |
| --- | --- |
| Red Hat | https://packages.microsoft.com/rhel/8/prod |
| SLES | https://packages.microsoft.com/sles/12/prod |
| Ubuntu 16.04 | msodbcsql unixodbc-dev |

3.  Move the downloaded packages to your Linux machine. If you used a different machine to download the packages, one way to move the packages to your Linux machine is with the scp command.
4.  Install the and packages: Install the mssql-tools and msodbc packages. If you get any dependency errors, ignore them until the next step.

| Platform | Package install commands |
| --- | --- |
| Red Hat | sudo yum localinstall msodbcsql-<version>.rpm sudo yum localinstall mssql-tools-<version>.rpm |
| SLES | sudo zypper install msodbcsql-<version>.rpm sudo zypper install mssql-tools-<version>.rpm |
| Ubuntu | sudo dpkg -i msodbcsql_<version>.deb sudo dpkg -i mssql-tools_<version>.deb |

5.  Resolve missing dependencies: You might have missing dependencies at this point. If not, you can skip this step. In some cases, you must manually locate and install these dependencies.

For RPM packages, you can inspect the required dependencies with the following commands:Bashrpm -qpR msodbcsql-<version>.rpmrpm -qpR mssql-tools-<version>.rpmFor Debian packages, if you have access to approved repositories containing those dependencies, the easiest solution is to use the apt-get command:Bashsudo apt-get -f installThis command completes the installation of the SQL Server packages as well.If this does not work for your Debian package, you can inspect the required dependencies with the following commands:Bashdpkg -I msodbcsql_<version>_amd64.deb | grep "Depends:"dpkg -I mssql-tools_<version>_amd64.deb | grep "Depends:"Mssql-cli a interactive command line tool for SQL ServerMssql-cli is a new and interactive command line tool that provides the following key enhancements over sqlcmd in the Terminal environment:

*   T-SQL IntelliSense
*   Syntax highlighting
*   Pretty formatting for query results, including Vertical Format
*   Multi-line edit mode
*   Configuration file support

Mssql-cli aims to offer an improved interactive command line experience for T-SQL. It is fully open source under the BSD-3 license, and a contribution to the dbcli organization, an open source suite of interactive CLI tools for relational databases including SQL Server, PostgresSQL, and MySQL. The command-line UI is written in Python and the tool leverages the same microservice backend (sqltoolsservice) that powers the VS Code SQL extension, SQL Operations Studio, and the other Python CLI tool we announced earlier, mssql-scripter.![](Image00016.jpg)mssql-cli multi-line queries to build readable queries. Also includes syntax highlighting and “smart” auto-completion.In order to install mssql-cli, you must have Python on your machine. Please refer to the installation guide for OS-specific methods to get Python.Mssql-cli is installed via pip. If you know pip, you can install mssql-cli using command.$ pip install mssql-cliThis command may need to run as sudo if you are installing to the system site packages. Mssql-cli can be installed using the –user option, which does not require sudo.$ pip install --user mssql-cliIf you are having installation issues or would like more specific instructions, please see the installation guide .Once you have mssql-cli installed, connect to your database with the command:$ mssql-cli -S <server name> -U <user name> -d <database name>Use PowerShell on Windows to Manage SQL Server on LinuxThis article introduces SQL Server PowerShell and walks you through a couple of examples on how to use it with SQL Server on Linux. PowerShell support for SQL Server is currently available on Windows, MacOS, & Linux. This article walks you through using a Windows machine to connect to a remote SQL Server instance on Linux.Install the newest version of SQL PowerShell on WindowsSQL PowerShell on Windows is maintained in the PowerShell Gallery. When working with SQL Server, you should always use the most recent version of the SqlServer PowerShell module.Launch PowerShell and import the sqlserver moduleLet's start by launching PowerShell on Windows. Use Win+R, on your Windows computer, and type PowerShell to launch a new Windows PowerShell session.PowerShellSQL Server provides a PowerShell module named SqlServer. You can use the SqlServer module to import the SQL Server components (SQL Server provider and cmdlets) into a PowerShell environment or script.Copy and paste the following command at the PowerShell prompt to import the SqlServer module into your current PowerShell session:PowerShellImport-Module SqlServerType the following command at the PowerShell prompt to verify that the SqlServer module was imported correctly:PowerShellGet-Module -Name SqlServerPowerShell should display information similar to the following output:ModuleType Version    Name          ExportedCommands---------- -------    ----          ----------------Script     21.1.18102 SqlServer     {Add-SqlAvailabilityDatabase, Add-SqlAvailabilityGroupList...Connect to SQL Server and get server informationLet's use PowerShell on Windows to connect to your SQL Server instance on Linux and display a couple of server properties.Copy and paste the following commands at the PowerShell prompt. When you run these commands, PowerShell will:

*   Display a dialog that prompts you for the hostname or IP address of your instance
*   Display the Windows PowerShell credential request dialog, which prompts you for the credentials. You can use your SQL username and SQL password to connect to your SQL Server instance on Linux
*   Use the  Get-SqlInstance cmdlet to connect to the  Server and display a few properties

Optionally, you can just replace the $serverInstance variable with the IP address or the hostname of your SQL Server instance.PowerShell# Prompt for instance & credentials to login into SQL Server$serverInstance = Read-Host "Enter the name of your instance"$credential = Get-Credential# Connect to the Server and get a few propertiesGet-SqlInstance -ServerInstance $serverInstance -Credential $credential# donePowerShell should display information similar to the following output:Instance Name                   Version    ProductLevel UpdateLevel  HostPlatform HostDistribution               -------------                   -------    ------------ -----------  ------------ ----------------               your_server_instance            14.0.3048  RTM          CU13         Linux        UbuntuNoteIf nothing is displayed for these values, the connection to the target SQL Server instance most likely failed. Make sure that you can use the same connection information to connect from SQL Server Management Studio.Using the SQL Server PowerShell ProviderAnother option for connecting to your SQL Server instance is to use the SQL Server PowerShell Provider. This provider allows you to navigate SQL Server instance similar to as if you were navigating the tree structure in Object Explorer, but at the cmdline. By default this provider is presented as a PSDrive named SQLSERVER:\ which you can use to connect & navigate SQL Server instances that your domain account has access to.You can also use SQL authentication with the SQL Server PowerShell Provider. To do this, use the New-PSDrive cmdlet to create a new PSDrive and supply the proper credentials in order to connect.In this example below, you will see one example of how to create a new PSDrive using SQL authentication.PowerShell# NOTE: We are reusing the values saved in the $credential variable from the above example.New-PSDrive -Name SQLonDocker -PSProvider SqlServer -Root 'SQLSERVER:\SQL\localhost,10002\Default\' -Credential $credentialYou can confirm that the drive was created by running the Get-PSDrive cmdlet.PowerShellGet-PSDriveOnce you have created your new PSDrive, you can start navigating it.PowerShelldir SQLonDocker:\DatabasesHere is what the output might look like. You might notice the output is similar to what SSMS will display at the Databases node. It displays the user databases, but not the system databases.PowerShellName                 Status           Size     Space  Recovery Compat. OwnerAvailable  Model     Level----                 ------           ---- ---------- -------- ------- -----AdventureWorks2016   Normal      209.63 MB    1.31 MB Simple       130 saAdventureWorksDW2012 Normal      167.00 MB   32.47 MB Simple       110 saAdventureWorksDW2014 Normal      188.00 MB   78.10 MB Simple       120 saAdventureWorksDW2016 Normal      172.00 MB   74.76 MB Simple       130 saAdventureWorksDW2017 Normal      208.00 MB   40.57 MB Simple       140 saIf you need to see all databases on your instance, one option is to use the Get-SqlDatabase cmdlet.Examine SQL Server error logsThe following steps use PowerShell on Windows to examine error logs connect on your SQL Server instance on Linux. We will also use the Out-GridView cmdlet to show information from the error logs in a grid view display.Copy and paste the following commands at the PowerShell prompt. They might take a few minutes to run. These commands do the following:

*   Display a dialog that prompts you for the hostname or IP address of your instance
*   Display the Windows PowerShell credential request dialog, which prompts you for the credentials. You can use your SQL username and SQL password to connect to your SQL Server instance on Linux
*   Use the  Get-SqlErrorLog cmdlet to connect to the SQL Server instance on Linux and retrieve error logs since  Yesterday
*   Pipe the output to the  Out-GridView cmdlet

Optionally, you can replace the $serverInstance variable with the IP address or the hostname of your SQL Server instance.PowerShell# Prompt for instance & credentials to login into SQL Server$serverInstance = Read-Host "Enter the name of your instance"$credential = Get-Credential# Retrieve error logs since yesterdayGet-SqlErrorLog -ServerInstance $serverInstance -Credential $credential -Since Yesterday | Out-GridView# doneSQL Server PowerShellInstall SQL Server PowerShellThere are two SQL Server PowerShell modules; SqlServer  and SQLPS .The SqlServer module is the current PowerShell module to use.The SQLPS module is included with the SQL Server installation (for backward compatibility) but is no longer updated.The SqlServer module contains updated versions of the cmdlets in SQLPS and includes new cmdlets to support the latest SQL features.Previous versions of the SqlServer module were included with SQL Server Management Studio (SSMS), but only with the 16.x versions of SSMS.To use PowerShell with SSMS 17.0 and later, install the SqlServer module from the PowerShell Gallery.You can also use PowerShell with Azure Data Studio.Why did the module change from SQLPS to SqlServer?To ship SQL PowerShell updates, we had to change the identity of the SQL PowerShell module, and the wrapper known as SQLPS.exe. Because of this change, there are now two SQL PowerShell modules, the SqlServer module, and the SQLPS module.Update your PowerShell scripts if you import the SQLPS module.If you have any PowerShell scripts that run Import-Module -Name SQLPS, and you want to take advantage of the new provider functionality and new cmdlets, you must change them to Import-Module -Name SqlServer. The new module is installed to %ProgramFiles%\WindowsPowerShell\Modules\SqlServer folder. As such, you don't have to update the $env:PSModulePath variable. If you have scripts that use a third-party or community version of a module named SqlServer, use the Prefix parameter to avoid name collisions.It is recommended to start your script with Import-Module SQLServer to avoid side-by-side issues if the SQLPS module is installed on the same machine.This section applies to scripts executed from PowerShell and not the SQL Agent. The new module can be used with SQL Agent job steps using #NOSQLPS.SQL Server PowerShell ComponentsThe SqlServer module comes with:

*   PowerShell Providers, which enables a simple navigation mechanism similar to file system paths. You can build paths similar to file system paths, where the drive is associated with a SQL Server management object model, and the nodes are based on the object model classes. You can then use familiar commands such as cd and dir to navigate the paths similar to the way you navigate folders in a command prompt window. You can use other commands, such as ren or del, to perform actions on the nodes in the path.
*   A set of cmdlets that support actions such as running a sqlcmd script containing Transact-SQL or XQuery statements.
*   The AS provider and cmdlets, which before they were installed separately.

SQL Server versionsSQL PowerShell cmdlets can be used to manage instances of Azure SQL Database, Azure Synapse Analytics, and all supported SQL Server products.SQL Server identifiers that contain characters not supported in PowerShell pathsThe Encode-Sqlname and Decode-Sqlname cmdlets help you specify SQL Server identifiers that contain characters not supported in PowerShell paths.Use the Convert-UrnToPath cmdlet to convert a Unique Resource Name for a Database Engine object to a path for the SQL Server PowerShell provider.Query Expressions and Unique Resource NamesQuery expressions are strings that use syntax similar to XPath to specify a set of criteria that enumerates one or more objects in an object model hierarchy. A Unique Resource Name (URN) is a specific type of query expression string that uniquely identifies a single object.SQL Server AgentThere's no change to the module used by SQL Server Agent. As such, SQL Server Agent jobs, which have PowerShell type job steps use the SQLPS module. However, starting with SQL Server 2019, you can disable SQLPS. To do so, on the first line of a job step of the type PowerShell you can add #NOSQLPS, which stops the SQL Agent from auto-loading the SQLPS module. When you do this, your SQL Agent Job runs the version of PowerShell installed on the machine, and then you can use any other PowerShell module you like.If you want to use the SqlServer module in your SQL Agent Job step, you can place this code on the first two lines of your script.PowerShell#NOSQLPSImport-Module -Name SqlServerManage SQL Server on Linux with PowerShell CoreThis introduces SQL Server PowerShell and walks you through a couple of examples on how to use it with PowerShell Core (PS Core) on macOS & Linux. PowerShell Core is now an Open Source project on GitHub.Cross-platform editor optionsAll of the steps PowerShell Core below will work in a regular terminal, or you can run them from a terminal within VS Code or Azure Data Studio. Both VS Code and Azure Data Studio are available on macOS and Linux. For more information on Azure Data Studio, see this quickstart. You may also want to consider using the PowerShell extension for it.Install the SqlServer moduleThe SqlServer module is maintained in the PowerShell Gallery. When working with SQL Server, you should always use the most recent version of the SqlServer PowerShell module.To install the SqlServer module, open a PowerShell Core session and run the following code:powerhsellInstall-Module -Name SqlServerUsing the SqlServer moduleLet's start by launching PowerShell Core. If you are on macOS or Linux, Open a terminal session on your computer, and type pwsh to launch a new PowerShell Core session. On Windows, use Win+R, and type pwsh to launch a new PowerShell Core session.pwshSQL Server provides a PowerShell module named SqlServer. You can use the SqlServer module to import the SQL Server components (SQL Server provider and cmdlets) into a PowerShell environment or script.Copy and paste the following command at the PowerShell prompt to import the SqlServer module into your current PowerShell session:PowerShellImport-Module SqlServerType the following command at the PowerShell prompt to verify that the SqlServer module was imported correctly:PowerShellGet-Module -Name SqlServerPowerShell should display information similar to the following output:ModuleType Version    Name          ExportedCommands---------- -------    ----          ----------------Script     21.1.18102 SqlServer     {Add-SqlAvailabilityDatabase, Add-SqlAvailabilityGroupList...Connect to SQL Server and get server informationThe following steps use PowerShell Core to connect to your SQL Server instance on Linux and display a couple of server properties.Copy and paste the following commands at the PowerShell prompt. When you run these commands, PowerShell will:

*   Display a dialog that prompts you for the hostname or IP address of your instance
*   Display the PowerShell credential request dialog, which prompts you for the credentials. You can use your SQL username and SQL password to connect to your SQL Server instance on Linux
*   Use the  Get-SqlInstance cmdlet to connect to the  Server and display a few properties

Optionally, you can just replace the $serverInstance variable with the IP address or the hostname of your SQL Server instance.PowerShell# Prompt for instance & credentials to login into SQL Server$serverInstance = Read-Host "Enter the name of your instance"$credential = Get-Credential# Connect to the Server and return a few propertiesGet-SqlInstance -ServerInstance $serverInstance -Credential $credential# donePowerShell should display information similar to the following output:Instance Name                   Version    ProductLevel UpdateLevel  HostPlatform HostDistribution-------------                   -------    ------------ -----------  ------------ ----------------your_server_instance            14.0.3048  RTM          CU13         Linux        UbuntuNoteIf nothing is displayed for these values, the connection to the target SQL Server instance most likely failed. Make sure that you can use the same connection information to connect from SQL Server Management Studio.Using the SQL Server PowerShell ProviderAnother option for connecting to your SQL Server instance is to use the SQL Server PowerShell Provider. Using the provider allows you to navigate SQL Server instance similar to as if you were navigating the tree structure in Object Explorer, but at the cmdline. By default this provider is presented as a PSDrive named SQLSERVER:\ which you can use to connect & navigate SQL Server instances that your domain account has access to.You can also use SQL authentication with the SQL Server PowerShell Provider. To do this, use the New-PSDrive cmdlet to create a new PSDrive and supply the proper credentials to connect.In this example below, you will see an example of how to create a new PSDrive using SQL authentication.PowerShell# NOTE: We are reusing the values saved in the $credential variable from the above example.New-PSDrive -Name SQLonDocker -PSProvider SqlServer -Root 'SQLSERVER:\SQL\localhost,10002\Default\' -Credential $credentialYou can confirm that the drive was created by running the Get-PSDrive cmdlet.PowerShellGet-PSDriveOnce you have created your new PSDrive, you can start navigating it.PowerShelldir SQLonDocker:\DatabasesHere is what the output might look like. You might notice this output is similar to what SSMS will display at the Databases node. It displays the user databases, but not the system databases.PowerShellName                 Status           Size     Space  Recovery Compat. OwnerAvailable  Model     Level----                 ------           ---- ---------- -------- ------- -----AdventureWorks2016   Normal      209.63 MB    1.31 MB Simple       130 saAdventureWorksDW2012 Normal      167.00 MB   32.47 MB Simple       110 saAdventureWorksDW2014 Normal      188.00 MB   78.10 MB Simple       120 saAdventureWorksDW2016 Normal      172.00 MB   74.76 MB Simple       130 saAdventureWorksDW2017 Normal      208.00 MB   40.57 MB Simple       140 saIf you need to see all databases on your instance, one option is to use the Get-SqlDatabase cmdlet.Get DatabasesAn important cmdlet to know is the Get-SqlDatabase. For many operations that involve a database, or objects within a database, the Get-SqlDatabase cmdlet can be used. If you supply values for both the -ServerInstance and -Database parameters, only that one database object will be retrieved. However, if you specify only the -ServerInstance parameter, a full list of all databases on that instance will be returned.PowerShell# NOTE: We are reusing the values saved in the $credential variable from the above example.# Connect to the Instance and retrieve all databasesGet-SqlDatabase -ServerInstance ServerB -Credential $credentialHere is a sample of what might be returned by the Get-SqlDatabase command above:PowerShellName                 Status           Size     Space  Recovery Compat. OwnerAvailable  Model     Level----                 ------           ---- ---------- -------- ------- -----AdventureWorks2016   Normal      209.63 MB    1.31 MB Simple       130 saAdventureWorksDW2012 Normal      167.00 MB   32.47 MB Simple       110 saAdventureWorksDW2014 Normal      188.00 MB   78.10 MB Simple       120 saAdventureWorksDW2016 Normal      172.00 MB   74.88 MB Simple       130 saAdventureWorksDW2017 Normal      208.00 MB   40.63 MB Simple       140 samaster               Normal        6.00 MB  600.00 KB Simple       140 samodel                Normal       16.00 MB    5.70 MB Full         140 samsdb                 Normal       15.50 MB    1.14 MB Simple       140 satempdb               Normal       16.00 MB    5.49 MB Simple       140 saExamine SQL Server error logsThe following steps use PowerShell Core to examine error logs connect on your SQL Server instance on Linux.Copy and paste the following commands at the PowerShell prompt. They might take a few minutes to run. These commands do the following steps:

*   Display a dialog that prompts you for the hostname or IP address of your instance
*   Display the PowerShell credential request dialog that prompts you for the credentials. You can use your SQL username and SQL password to connect to your SQL Server instance on Linux
*   Use the  Get-SqlErrorLog cmdlet to connect to the SQL Server instance on Linux and retrieve error logs since  Yesterday

Optionally, you can replace the $serverInstance variable with the IP address or the hostname of your SQL Server instance.PowerShell# Prompt for instance & credentials to login into SQL Server$serverInstance = Read-Host "Enter the name of your instance"$credential = Get-Credential# Retrieve error logs since yesterdayGet-SqlErrorLog -ServerInstance $serverInstance -Credential $credential -Since Yesterday# doneExplore cmdlets currently available in PS CoreWhile the SqlServer module currently has 109 cmdlets available in Windows PowerShell, only 62 of the 109 are available in PSCore. A full list of 62 cmdlets currently available is included below.The following command will show you all of the cmdlets available on the version of PowerShell you are using.PowerShellGet-Command -Module SqlServer -CommandType Cmdlet |Sort-Object -Property Noun |SELECT Name

*   ConvertFrom-EncodedSqlName
*   ConvertTo-EncodedSqlName
*   Get-SqlAgent
*   Get-SqlAgentJob
*   Get-SqlAgentJobHistory
*   Get-SqlAgentJobSchedule
*   Get-SqlAgentJobStep
*   Get-SqlAgentSchedule
*   Invoke-SqlAssessment
*   Get-SqlAssessmentItem
*   Remove-SqlAvailabilityDatabase
*   Resume-SqlAvailabilityDatabase
*   Add-SqlAvailabilityDatabase
*   Suspend-SqlAvailabilityDatabase
*   New-SqlAvailabilityGroup
*   Set-SqlAvailabilityGroup
*   Remove-SqlAvailabilityGroup
*   Switch-SqlAvailabilityGroup
*   Join-SqlAvailabilityGroup
*   Revoke-SqlAvailabilityGroupCreateAnyDatabase
*   Grant-SqlAvailabilityGroupCreateAnyDatabase
*   New-SqlAvailabilityGroupListener
*   Set-SqlAvailabilityGroupListener
*   Add-SqlAvailabilityGroupListenerStaticIp
*   Set-SqlAvailabilityReplica
*   Remove-SqlAvailabilityReplica
*   New-SqlAvailabilityReplica
*   Set-SqlAvailabilityReplicaRoleToSecondary
*   New-SqlBackupEncryptionOption
*   Get-SqlBackupHistory
*   Invoke-Sqlcmd
*   New-SqlCngColumnMasterKeySettings
*   Remove-SqlColumnEncryptionKey
*   Get-SqlColumnEncryptionKey
*   Remove-SqlColumnEncryptionKeyValue
*   Add-SqlColumnEncryptionKeyValue
*   Get-SqlColumnMasterKey
*   Remove-SqlColumnMasterKey
*   New-SqlColumnMasterKey
*   Get-SqlCredential
*   Set-SqlCredential
*   New-SqlCredential
*   Remove-SqlCredential
*   New-SqlCspColumnMasterKeySettings
*   Get-SqlDatabase
*   Restore-SqlDatabase
*   Backup-SqlDatabase
*   Set-SqlErrorLog
*   Get-SqlErrorLog
*   New-SqlHADREndpoint
*   Set-SqlHADREndpoint
*   Get-SqlInstance
*   Add-SqlLogin
*   Remove-SqlLogin
*   Get-SqlLogin
*   Set-SqlSmartAdmin
*   Get-SqlSmartAdmin
*   Read-SqlTableData
*   Write-SqlTableData
*   Read-SqlViewData
*   Read-SqlXEvent
*   Convert-UrnToPath

Get started with Log Shipping on LinuxSQL Server Log shipping is a HA configuration where a database from a primary server is replicated onto one or more secondary servers. In a nutshell, a backup of the source database is restored onto the secondary server. Then the primary server creates transaction log backups periodically, and the secondary servers restore them, updating the secondary copy of the database.![Diagram showing the log shipping workflow.](Image00017.jpg)As described in the this picture, a log shipping session involves the following steps:

*   Backing up the transaction log file on the primary SQL Server instance
*   Copying the transaction log backup file across the network to one or more secondary SQL Server instances
*   Restoring the transaction log backup file on the secondary SQL Server instances

Setup a network share for Log Shipping using CIFSConfigure Primary Server

*   Run the following to install Samba

Bashsudo apt-get install samba #For Ubuntusudo yum -y install samba #For RHEL/CentOS

*   Create a directory to store the logs for Log Shipping and give mssql the required permissions

Bashmkdir /var/opt/mssql/tlogschown mssql:mssql /var/opt/mssql/tlogschmod 0700 /var/opt/mssql/tlogs

*   Edit the /etc/samba/smb.conf file (you need root permissions for that) and add the following section:

Bash[tlogs]path=/var/opt/mssql/tlogsavailable=yesread only=yesbrowsable=yespublic=yeswritable=no

*   Create a mssql user for Samba

Bashsudo smbpasswd -a mssql

*   Restart the Samba services

Bashsudo systemctl restart smbd.service nmbd.serviceConfigure Secondary Server

*   Run the following to install the CIFS client

Bashsudo apt-get install cifs-utils #For Ubuntusudo yum -y install cifs-utils #For RHEL/CentOS

*   Create a file to store your credentials. Use the password you recently set for your mssql Samba account

Console    vim /var/opt/mssql/.tlogcreds    #Paste the following in .tlogcreds    username=mssql    domain=<domain>    password=<password>

*   Run the following commands to create an empty directory for mounting and set permission and ownership correctly

Bashmkdir /var/opt/mssql/tlogssudo chown root:root /var/opt/mssql/tlogssudo chmod 0550 /var/opt/mssql/tlogssudo chown root:root /var/opt/mssql/.tlogcredssudo chmod 0660 /var/opt/mssql/.tlogcreds

*   Add the line to etc/fstab to persist the share

Console    //<ip_address_of_primary_server>/tlogs /var/opt/mssql/tlogs cifs credentials=/var/opt/mssql/.tlogcreds,ro,uid=mssql,gid=mssql 0 0

*   Mount the shares

Bashsudo mount –aSetup Log Shipping via T-SQL

*   Run this script from your primary server

SQLBACKUP DATABASE SampleDBTO DISK = '/var/opt/mssql/tlogs/SampleDB.bak'GOSQLDECLARE @LS_BackupJobId​ AS uniqueidentifierDECLARE @LS_PrimaryId​ AS uniqueidentifierDECLARE @SP_Add_RetCode​ As intEXECUTE @SP_Add_RetCode = master.dbo.sp_add_log_shipping_primary_database         @database = N'SampleDB',@backup_directory = N'/var/opt/mssql/tlogs',@backup_share = N'/var/opt/mssql/tlogs',@backup_job_name = N'LSBackup_SampleDB'        ,@backup_retention_period = 4320        ,@backup_compression = 2,@backup_threshold = 60        ,@threshold_alert_enabled = 1,@history_retention_period = 5760        ,@backup_job_id = @LS_BackupJobId OUTPUT        ,@primary_id = @LS_PrimaryId OUTPUT,@overwrite = 1IF (@@ERROR = 0 AND @SP_Add_RetCode = 0)BEGINDECLARE @LS_BackUpScheduleUID​ As uniqueidentifierDECLARE @LS_BackUpScheduleID​ AS intEXECUTE msdb.dbo.sp_add_schedule@schedule_name =N'LSBackupSchedule',@enabled = 1,@freq_type = 4,@freq_interval = 1,@freq_subday_type = 4,@freq_subday_interval = 15,@freq_recurrence_factor = 0,@active_start_date = 20170418,@active_end_date = 99991231,@active_start_time = 0,@active_end_time = 235900        ,@schedule_uid = @LS_BackUpScheduleUID OUTPUT        ,@schedule_id = @LS_BackUpScheduleID OUTPUTEXECUTE msdb.dbo.sp_attach_schedule@job_id = @LS_BackupJobId,@schedule_id = @LS_BackUpScheduleID  EXECUTE msdb.dbo.sp_update_job@job_id = @LS_BackupJobId,@enabled = 1ENDEXECUTE master.dbo.sp_add_log_shipping_alert_jobEXECUTE master.dbo.sp_add_log_shipping_primary_secondary@primary_database = N'SampleDB',@secondary_server = N'<ip_address_of_secondary_server>',@secondary_database = N'SampleDB',@overwrite = 1

*   Run this script from your secondary server

SQLRESTORE DATABASE SampleDB FROM DISK = '/var/opt/mssql/tlogs/SampleDB.bak'WITH NORECOVERY;SQLDECLARE @LS_Secondary__CopyJobId​ AS uniqueidentifierDECLARE @LS_Secondary__RestoreJobId​ AS uniqueidentifierDECLARE @LS_Secondary__SecondaryId​ AS uniqueidentifierDECLARE @LS_Add_RetCode​ As intEXECUTE @LS_Add_RetCode = master.dbo.sp_add_log_shipping_secondary_primary@primary_server = N'<ip_address_of_primary_server>',@primary_database = N'SampleDB',@backup_source_directory = N'/var/opt/mssql/tlogs/',@backup_destination_directory = N'/var/opt/mssql/tlogs/',@copy_job_name = N'LSCopy_SampleDB',@restore_job_name = N'LSRestore_SampleDB',@file_retention_period = 4320,@overwrite = 1        ,@copy_job_id = @LS_Secondary__CopyJobId OUTPUT        ,@restore_job_id = @LS_Secondary__RestoreJobId OUTPUT        ,@secondary_id = @LS_Secondary__SecondaryId OUTPUTIF (@@ERROR = 0 AND @LS_Add_RetCode = 0)BEGINDECLARE @LS_SecondaryCopyJobScheduleUID​ As uniqueidentifierDECLARE @LS_SecondaryCopyJobScheduleID​ AS intEXECUTE msdb.dbo.sp_add_schedule@schedule_name =N'DefaultCopyJobSchedule',@enabled = 1,@freq_type = 4,@freq_interval = 1,@freq_subday_type = 4,@freq_subday_interval = 15,@freq_recurrence_factor = 0,@active_start_date = 20170418,@active_end_date = 99991231,@active_start_time = 0,@active_end_time = 235900        ,@schedule_uid = @LS_SecondaryCopyJobScheduleUID OUTPUT        ,@schedule_id = @LS_SecondaryCopyJobScheduleID OUTPUTEXECUTE msdb.dbo.sp_attach_schedule@job_id = @LS_Secondary__CopyJobId,@schedule_id = @LS_SecondaryCopyJobScheduleID  DECLARE @LS_SecondaryRestoreJobScheduleUID​ As uniqueidentifierDECLARE @LS_SecondaryRestoreJobScheduleID​ AS intEXECUTE msdb.dbo.sp_add_schedule@schedule_name =N'DefaultRestoreJobSchedule',@enabled = 1,@freq_type = 4,@freq_interval = 1,@freq_subday_type = 4,@freq_subday_interval = 15,@freq_recurrence_factor = 0,@active_start_date = 20170418,@active_end_date = 99991231,@active_start_time = 0,@active_end_time = 235900        ,@schedule_uid = @LS_SecondaryRestoreJobScheduleUID OUTPUT        ,@schedule_id = @LS_SecondaryRestoreJobScheduleID OUTPUTEXECUTE msdb.dbo.sp_attach_schedule@job_id = @LS_Secondary__RestoreJobId,@schedule_id = @LS_SecondaryRestoreJobScheduleID  ENDDECLARE @LS_Add_RetCode2​ As intIF (@@ERROR = 0 AND @LS_Add_RetCode = 0)BEGINEXECUTE @LS_Add_RetCode2 = master.dbo.sp_add_log_shipping_secondary_database@secondary_database = N'SampleDB',@primary_server = N'<ip_address_of_primary_server>',@primary_database = N'SampleDB',@restore_delay = 0,@restore_mode = 0        ,@disconnect_users​ = 0,@restore_threshold = 45   ,@threshold_alert_enabled = 1        ,@history_retention_period​ = 5760,@overwrite = 1ENDIF (@@error = 0 AND @LS_Add_RetCode = 0)BEGINEXECUTE msdb.dbo.sp_update_job@job_id = @LS_Secondary__CopyJobId,@enabled = 1EXECUTE msdb.dbo.sp_update_job@job_id = @LS_Secondary__RestoreJobId,@enabled = 1ENDVerify Log Shipping works

*   Verify that Log Shipping works by starting the following job on the primary server

SQLUSE msdb ; GO  EXECUTE dbo.sp_start_job N'LSBackup_SampleDB' ; GO  

*   Verify that Log Shipping works by starting the following job on the secondary server

SQLUSE msdb ; GO  EXECUTE dbo.sp_start_job N'LSCopy_SampleDB' ; GO  EXECUTE dbo.sp_start_job N'LSRestore_SampleDB' ; GO  

*   Verify that Log Shipping failover works by executing the following command

SQLRESTORE DATABASE SampleDB WITH RECOVERY ;DB Mail and Email Alerts with SQL Agent on LinuxThe following steps show you how to set up DB Mail and use it with SQL Server Agent (mssql-server-agent) on Linux.1\. Enable DB MailSQLUSE masterGOsp_configure 'show advanced options',1GORECONFIGURE WITH OVERRIDEGOsp_configure 'Database Mail XPs', 1GORECONFIGUREGO2\. Create a new accountSQLEXECUTE msdb.dbo.sysmail_add_account_sp@account_name = 'SQLAlerts',@description = 'Account for Automated DBA Notifications',@email_address = 'sqlagenttest@gmail.com',@replyto_address = 'sqlagenttest@gmail.com',@display_name = 'SQL Agent',@mailserver_name = 'smtp.gmail.com',@port = 587,@enable_ssl = 1,@username = 'sqlagenttest@gmail.com',@password = '<password>'GO3\. Create a default profileSQLEXECUTE msdb.dbo.sysmail_add_profile_sp@profile_name = 'default',@description = 'Profile for sending Automated DBA Notifications'GO4\. Add the Database Mail account to a Database Mail profileSQLEXECUTE msdb.dbo.sysmail_add_principalprofile_sp@profile_name = 'default',@principal_name = 'public',@is_default = 1 ;5\. Add account to profileSQLEXECUTE msdb.dbo.sysmail_add_profileaccount_sp  @profile_name = 'default',  @account_name = 'SQLAlerts',  @sequence_number = 1;6\. Send test emailEXECUTE msdb.dbo.sp_send_dbmail@profile_name = 'default',@recipients = 'recipient-email@gmail.com',@Subject = 'Testing DBMail',@Body = 'This message is a test for DBMail'GO7\. Set DB Mail Profile using mssql-conf or environment variableYou can use the mssql-conf utility or environment variables to register your DB Mail profile. In this case, let's call our profile default.Bash# via mssql-confsudo /opt/mssql/bin/mssql-conf set sqlagent.databasemailprofile default# via environment variableMSSQL_AGENT_EMAIL_PROFILE=default8\. Set up an operator for SQLAgent job notificationsSQLEXEC msdb.dbo.sp_add_operator@name=N'JobAdmins',@enabled=1,@email_address=N'recipient-email@gmail.com',@category_name=N'[Uncategorized]'GO9\. Send email when 'Agent Test Job' succeedsEXEC msdb.dbo.sp_update_job@job_name='Agent Test Job',@notify_level_email=1,@notify_email_operator_name=N'JobAdmins'GOBusiness continuity and database recovery - SQL Server on LinuxThis provides an overview of business continuity solutions for high availability and disaster recovery in SQL Server.One common task everyone deploying SQL Server has to account for is making sure that all mission critical SQL Server instances and the databases within them are available when the business and end users need them, whether that is 9 to 5 or around the clock. The goal is to keep the business up and running with minimal or no interruption. This concept is also known as business continuity.SQL Server 2017 introduces many new features or enhancements to existing ones, some of which are for availability. The biggest addition to SQL Server 2017 is the support for SQL Server on Linux distributions.This article is focused on covering the availability scenarios in SQL Server 2017 as well as the new and enhanced availability features in SQL Server 2017\. The scenarios include hybrid ones that will be able to span SQL Server deployments on both Windows Server and Linux, as well as ones that can increase the number of readable copies of a database. While this article does not cover availability options external to SQL Server, such as those provided by virtualization, everything discussed here applies to SQL Server installations inside a guest virtual machine whether in the public cloud or hosted by an on premises hypervisor server.SQL Server 2017 scenarios using the availability featuresAvailability groups, FCIs, and log shipping can be used in a variety of ways, and not necessarily just for availability purposes. There are four main ways the availability features can be used:

*   High availability
*   Disaster recovery
*   Migrations and upgrades
*   Scaling out readable copies of one or more databases

Each section will discuss the relevant features that can be used for that particular scenario. The one feature not covered is SQL Server replication. While not officially designated as an availability feature under the Always On umbrella, it is often used for making data redundant in certain scenarios. Replication will be added to SQL Server on Linux in a future release.High availabilityEnsuring that SQL Server instances or database are available in the case of a problem that is local to a data center or single region in the cloud region is important. This section will cover how the SQL Server availability features can assist in that task. All of the features described are available both on Windows Server as well as on Linux.Always on availability groupsIntroduced in SQL Server 2012, Always On Availability Groups (availability groups) provide database-level protection by sending each transaction of a database to another instance, known as a replica, that contains a copy of that database in a special state. An availability group can be deployed on Standard or Enterprise Editions. The instances participating in an availability group can be either standalone or Always On Failover Cluster Instances (FCIs, described in the next section). Since the transactions are sent to a replica as they happen, availability groups are recommended where there are requirements for lower recovery point and recovery time objectives. Data movement between replicas can be synchronous or asynchronous, with Enterprise Edition allowing up to three replicas (including the primary) as synchronous. An availability group has one fully read/write copy of the database which is on the primary replica, while all secondary replicas cannot receive transactions directly from end users or applications.Because availability groups only provide database-level, and not instance-level, protection, anything not captured in the transaction log or configured in the database will need to manually synchronized for each secondary replica. Some examples of objects that must be synchronized manually are logins at the instance level, linked servers, and SQL Server Agent jobs.An availability group also has another component called the listener, which allows applications and end users to connect without needing to know which SQL Server instance is hosting the primary replica. Each availability group would have its own listener. While the implementations of the listener are slightly different on Windows Server versus Linux, the functionality it provides and how it is used is the same. The picture below shows a Windows Server-based availability group which is using a Windows Server Failover Cluster (WSFC). An underlying cluster at the OS layer is required for availability whether it is on Linux or Windows Server. The example shows a simple two server, or node, configuration where a WSFC is the underlying cluster.![Simple availability group](Image00018.jpg)Standard and Enterprise Edition have different maximums when it comes to replicas. An availability group in Standard Edition, known as a Basic Availability Group, supports two replicas (one primary and one secondary) with only a single database in the availability group. Enterprise Edition not only allows multiple databases to be configured in a single availability group, but also can have up to nine total replicas (one primary, eight secondary). Enterprise edition also provides other optional benefits such as readable secondary replicas, the ability to make backups off of a secondary replica, and more.When it comes to availability, availability groups can provide either automatic or manual failover. Automatic failover can occur if synchronous data movement is configured and the database on the primary and secondary replica are in a synchronized state. As long as the listener is used and the application uses a later version of .NET (3.5 with an update, or 4.0 and above), the failover should be handled with minimal to no impact to end users if a listener is utilized. Failover to make a secondary replica the new primary replica can be configured to be automatic or manual, and generally is measured in seconds.The list below highlights some differences with availability groups on Windows Server versus Linux:

*   Due to differences in the way the underlying cluster works on Linux and Windows Server, all failovers (manual or automatic) of availability groups are done via the cluster on Linux. On Windows Server-based availability group deployments, manual failovers must be done via SQL Server. Automatic failovers are handled by the underlying cluster on both Windows Server and Linux.
*   In SQL Server 2017, the recommended configuration for availability groups on Linux will be a minimum of three replicas. This is due to the way that the underlying clustering works. An improved solution for a two replica configuration will come post-release.
*   On Linux, the common name used by each listener is defined in DNS and not in the cluster like it is on Windows Server.

In SQL Server 2017, there are some new features and enhancements to availability groups:

*   Cluster types
*   REQUIRED_SECONDARIES_TO_COMMIT
*   Enhanced Microsoft Distributor Transaction Coordinator (DTC) support for Windows Server-based configurations
*   Additional scale out scenarios for read only databases (described later in this article)

Always on availability group cluster typesThe built-in availability form of clustering in Windows Server is enabled via a feature named Failover Clustering. It allows you to build a WSFC to be used with an availability group or FCI. Integration for availability groups and FCIs is provided by a cluster-aware resource DLLs shipped by SQL Server.Each supported Linux distribution ships its own version of the Pacemaker cluster solution. SQL Server 2017 on Linux supports the use of Pacemaker. Pacemaker is an open stack solution that each distribution can then integrate with their stack. While the distributions ship Pacemaker, it is not as integrated as the Failover Clustering feature in Windows Server.A WSFC and Pacemaker are more similar than different. Both provide a way to take individual servers and combine them in a configuration to provide availability, and have concepts of things like resources, constraints (even if implemented differently), failover, and so on. To support Pacemaker for both availability group and FCI configurations including things like automatic failover, Microsoft provides the mssql-server-ha package, which is similar to, but not exactly the same as, the resource DLLs in a WSFC, for Pacemaker. One of the differences between a WSFC and Pacemaker is that there is no network name resource in Pacemaker, which is the component that helps to abstract the name of the listener (or the name of the FCI) on a WSFC. DNS provides that name resolution on Linux.Because of the difference in the cluster stack, some changes needed to be made for availability groups because SQL Server has to handle some of the metadata that is natively handled by a WSFC. The most [!IMPORTANT] change is the introduction of a cluster type for an availability group. This is stored in sys.availability_groups in the cluster_type and cluster_type_desc columns. There are three cluster types:

*   WSFC
*   External
*   None

All availability groups that require availability must use an underlying cluster, which in the case of SQL Server 2017 means a WSFC or Pacemaker. For Windows Server-based availability groups that use an underlying WSFC, the default cluster type is WSFC and does not need to be set. For Linux-based availability groups, when creating the availability group, the cluster type must be set to External. The integration with Pacemaker is configured after the availability group is created, whereas on a WSFC, it is done at creation time.A cluster type of None can be used with both Windows Server and Linux availability groups. Setting the cluster type to None means that the availability group does not require an underlying cluster. This means SQL Server 2017 is the first version of SQL Server to support availability groups without a cluster, but the tradeoff is that this configuration is not supported as a high availability solution.For those who are only looking to just add additional read only copies of a database, or like what an availability group provides for migration/upgrades but do not want to be tied to the additional complexity of an underlying cluster or even the replication, an availability group with a cluster type of None is a perfect solution.The screenshot below shows the support for the different kinds of cluster types in SSMS. You must be running version 17.1 or later. The screenshot below is from version 17.2.![SSMS AG Options](Image00019.jpg)REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMITSQL Server 2016 increased support for the number of synchronous replicas from two to three in Enterprise Edition. However, if one secondary replica was synchronized but the other was having a problem, there was no way to control the behavior to tell the primary to either wait for the misbehaving replica or to allow it to move on. This means that the primary replica at some point would continue to receive write traffic even though the secondary replica would not be in a synchronized state, which means that there is data loss on the secondary replica. In SQL Server 2017, there is now an option to be able to control the behavior of what happens when there are synchronous replicas named REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT. The option works as follows:

*   There are three possible values: 0, 1, and 2
*   The value is the number of secondary replicas that must be synchronized, which has implications for data loss, availability group availability, and failover
*   For WSFCs and a cluster type of None, the default value is 0, and can be manually set to 1 or 2
*   For a cluster type of External, by default, the cluster mechanism will set this and it can be overridden manually. For three synchronous replicas, the default value will be 1. On Linux, the value for REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT is configured on the availability group resource in the cluster. On Windows, it is set via Transact-SQL.

A value that is higher than 0 ensures higher data protection because if the required number of secondary replicas is not available, the primary will not be available until that is resolved. REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT also affects failover behavior since automatic failover could not occur if the right number of secondary replicas were not in the proper state. On Linux, a value of 0 will not allow automatic failover, so on Linux, when using synchronous with automatic failover, the value must be set higher than 0 to achieve automatic failover. 0 on Windows Server is the SQL Server 2016 and earlier behavior.Enhanced Microsoft distributed transaction coordinator supportBefore SQL Server 2016, the only way to get availability in SQL Server for applications that require distributed transactions which use DTC underneath the covers was to deploy FCIs. A distributed transaction can be done in one of two ways:

*   A transaction that spans more than one database in the same SQL Server instance
*   A transaction that spans more than one SQL Server instance or possibly involves a non-SQL Server data source

SQL Server 2016 introduced partial support for DTC with availability groups that covered the latter scenario. SQL Server 2017 completes the story by supporting both scenarios with DTC.Another enhancement to DTC support for availability groups is that in SQL Server 2016, enabling support for DTC to an availability group could only be done when the availability group was created, and could not be added later. In SQL Server 2017, DTC support can also be added to an availability group after it is created.Always on failover cluster instancesClustered installations have been a feature of SQL Server since version 6.5\. FCIs are a proven method of providing availability for the entire installation of SQL Server, known as an instance. This means that everything inside the instance, including databases, SQL Server Agent jobs, linked servers, et al., will move to another server should the underlying server encounter a problem. All FCIs require some sort of shared storage, even if it is provided via networking. The FCI's resources can only be running and owned by one node at any given time. In the picture below, the first node of the cluster owns the FCI, which also means it owns the shared storage resources associated with it denoted by the solid line to the storage.![Failover Cluster Instance](Image00020.jpg)After a failover, ownership changes as is seen in the picture below.![Post Failover](Image00021.jpg)There is zero data loss with an FCI, but the underlying shared storage is a single point of failure since there is one copy of the data. FCIs are often combined with another availability method, such as an availability group or log shipping, to have redundant copies of databases. The additional method deployed should use physically separate storage from the FCI. When the FCI fails over to another node, it stops on one node and starts on another, not unlike powering a server off and turning it on. An FCI goes through the normal recovery process, meaning any transactions that need to be rolled forward will be, and any transactions that are incomplete will be rolled back. Therefore, the database is consistent from a data point to the time of the failure or manual failover, hence no data loss. Databases are only available after recovery is complete, so recovery time will depend on many factors, and will generally be longer than failing over an availability group. The tradeoff is that when you fail over an availability group, there may be additional tasks required to make a database usable, such as enabling a SQL Server Agent jobs job.Like an availability group, FCIs abstract which node of the underlying cluster is hosting it. An FCI always retains the same name. Applications and end users never connect to the nodes; the unique name assigned to the FCI is used. An FCI can participate in an availability group as one of the instances hosing either a primary or secondary replica.The list below highlights some differences with FCIs on Windows Server versus Linux:

*   On Windows Server, an FCI is part of the installation process. An FCI on Linux is configured after installing SQL Server.
*   Linux only supports a single installation of SQL Server per host, so all FCIs will be a default instance. Windows Server supports up to 25 FCIs per WSFC.
*   The common name used by FCIs in Linux is defined in DNS, and should be the same as the resource created for the FCI.

Log shippingIf recovery point and recovery time objectives are more flexible, or databases are not considered to be highly mission critical, log shipping is another proven availability feature in SQL Server. Based on SQL Server's native backups, the process for log shipping automatically generates transaction log backups, copies them to one or more instances known as a warm standby, and automatically applies the transaction log backups to that standby. Log shipping uses SQL Server Agent jobs to automate the process of backing up, copying, and applying the transaction log backups.![Log Shipping](Image00022.jpg)Arguably the biggest advantage of using log shipping in some capacity is that it accounts for human error. The application of transaction logs can be delayed. Therefore, if someone issues something like an UPDATE without a WHERE clause, the standby may not have the change so you could switch to that while you repair the primary system. While log shipping is easy to configure, switching from the primary to a warm standby, known as a role change, is always manual. A role change is initiated via Transact-SQL, and like an availability group, all objects not captured in the transaction log must be manually synchronized. Log shipping also needs to be configured per database, whereas a single availability group can contain multiple databases. Unlike an availability group or FCI, log shipping has no abstraction for a role change. Applications must be able to handle this. Techniques such as a DNS alias (CNAME) could be employed, but there are pros and cons, such as the time it takes for DNS to refresh after the switch.Disaster recoveryWhen your primary availability location experiences a catastrophic event like an earthquake or flood, the business must be prepared to have its systems come online elsewhere. This section will cover how the SQL Server availability features can assist with business continuity.Always on availability groupsOne of the benefits of availability groups is that both high availability and disaster recovery can be configured using a single feature. Without the requirement for ensuring that shared storage is also highly available, it is much easier to have replicas that are local in one data center for high availability, and remote ones in other data centers for disaster recovery each with separate storage. Having additional copies of the database is the tradeoff for ensuring redundancy. An example of an availability group that spans multiple data centers is shown below. One primary replica is responsible for keeping all secondary replicas synchronized.![Availability Group](Image00023.jpg)Outside of an availability group with a cluster type of none, an availability group requires that all replicas are part of the same underlying cluster whether it is a WSFC or Pacemaker. This means that in the picture above, the WSFC is stretched to work in two different data centers which adds complexity. regardless of the platform (Windows Server or Linux). Stretching clusters across distance adds complexity. Introduced in SQL Server 2016, a distributed availability group allows an availability group to span availability groups configured on different clusters. This decouples the requirement to have the nodes all participate in the same cluster, which makes configuring disaster recovery much easier.![A diagram of a Distributed Availability Group.](Image00024.jpg)Always on failover cluster instancesFCIs can be used for disaster recovery. As with a normal availability group, the underlying cluster mechanism must also be extended to all locations which adds complexity. There is an additional consideration for FCIs: the shared storage. The same disks need to be available in the primary and secondary sites, so an external method such as functionality provided by the storage vendor at the hardware layer or using storage Replica in Windows Server, is required to ensure that the disks used by the FCI exist elsewhere.![Always On FCI](Image00025.jpg)Log shippingLog shipping is one of the oldest methods of providing disaster recovery for SQL Server databases. Log shipping is often used in conjunction with availability groups and FCIs to provide cost-effective and simpler disaster recovery where other options may be challenging due to environment, administrative skills, or budget. Similar to the high availability story for log shipping, many environments will delay the loading of a transaction log to account for human error.Migrations and upgradesWhen deploying new instances or upgrading old ones, a business cannot tolerate long outage. This section will discuss how the availability features of SQL Server can be used to minimize the downtime in a planned architecture change, server switch, platform change (such as Windows Server to Linux or vice versa), or during patching.Always on availability groupsAn existing instance containing one or more availability groups can be upgraded in place to SQL Server 2017\. While this will require some amount of downtime, with the right amount of planning, it can be minimized.If the goal is to migrate to new servers and not change the configuration (including the operating system or SQL Server version), those servers could be added as nodes to the existing underlying cluster and added to the availability group. Once the replica or replicas are in the right state, a manual failover could occur to a new server, and then the old ones could be removed from the availability group, and ultimately, decommissioned.Distributed AGs are also another method to migrate to a new configuration or upgrade SQL Server. Because a distributed AG supports different underlying AGs on different architectures, for example, you could change from SQL Server 2016 running on Windows Server 2012 R2 to SQL Server 2017 running on Windows Server 2016.![Distributed AG](Image00026.jpg)Finally, availability groups with a cluster type of None can also be used for migration or upgrading. You cannot mix and match cluster types in a typical availability group configuration, so all replicas would need to be a type of None. A distributed availability group can be used to span availability groups configured with different cluster types. This method is also supported across the different OS platforms.All variants of availability groups for migrations and upgrades allow the most time consuming portion of the work to be done over time - data synchronization. When it comes time to initiate the switch to the new configuration, the cutover will be a brief outage versus one long period of downtime where all the work, including data synchronization, would need to be completed.Availability groups can provide minimal downtime during patching of the underlying OS by manually failing over the primary to a secondary replica while the patching is being completed. From an operating system perspective, doing this would be more common on Windows Server since often, but not always, servicing the underlying OS may require a reboot. Patching Linux sometimes needs a reboot, but it can be infrequent.Patching SQL Server instances participating in an availability group can also minimize downtime depending on how complex the availability group architecture is. To patch servers participating in an availability group, a secondary replica is patched first. Once the right number of replicas are patched, the primary replica is manually failed over to another node to do the upgrade. Any remaining secondary replicas at that point can be upgraded, too.Always on failover cluster instancesFCIs on their own cannot assist with a traditional migration or upgrade; an availability group or log shipping would have to be configured for the databases in the FCI and all other objects accounted for. However, FCIs under Windows Server are still a popular option for when the underlying Windows Servers need to be patched. A manual failover can be initiated, which means a brief outage instead of having the instance completely unavailable for the entire time Windows Server is being patched. An FCI can be upgraded in place to SQL Server 2017.Log shippingLog shipping is still a popular option to both migrate and upgrade databases. Similar to availability groups, but this time using the transaction log as the synchronization method, the data propagation can be started well in advance of the server switch. At the time of the switch, once all traffic is stopped at the source, a final transaction log would need to be taken, copied, and applied to the new configuration. At that point, the database can be brought online. Log shipping is often more tolerant of slower networks, and while the switch may be slightly longer than one done using an availability group or a distributed availability group, it is usually measured in minutes - not hours, days, or weeks.Similar to availability groups, log shipping can provide a way to switch to another server in the event of patching.Other SQL Server deployment methods and availabilityThere are two other deployment methods for SQL Server on Linux: containers and using Azure (or another public cloud provider). The general need for availability as presented throughout this paper exists regardless of how SQL Server is deployed. These two methods have some special considerations when it comes to making SQL Server highly available.Containers using Docker are a new way of deploying SQL Server, either for Windows Server or Linux. A container is a complete image of SQL Server that is ready to run. However, there is currently no native support for clustering, and thus, direct high availability or disaster recovery. Currently, the options to make SQL Server databases available using containers would be log shipping and backup and restore. While an availability group with a cluster type of None can be configured, as noted earlier, it is not considered a true availability configuration. Microsoft is looking at ways to enable availability groups or FCIs using containers.If you are using containers today, if the container is lost, depending on the container platform, it can be deployed again and attached to the shared storage that was used. Some of this mechanism is provided by the container orchestrator. While this does provide some resiliency, there will be some downtime associated with database recovery and is not truly highly available as it would be if using an availability group or FCI.Linux IaaS virtual machines can be deployed with SQL Server installed using Azure. As with on premises-based installations, a supported installation requires the use of STONITH (Shoot the Other Node in the Head) which is external to Pacemaker itself. STONITH is provided via fencing availability agents. Some distributions ship them as part of the platform, others rely on external hardware and software vendors. Check with your preferred Linux distribution to see what forms of STONITH are provided so that a supported solution can be deployed in the public cloud.Cross-platform and Linux distribution interoperabilityWith SQL Server now supported on both Windows Server and Linux, this section covers the scenarios of how they can work together for availability in addition to other purposes, as well as the story for solutions that will incorporate more than one Linux distribution.Before covering the cross-platform and interoperability scenarios, two facts need to be stated:

*   There are no scenarios where a WSFC-based FCI or availability group will work with a Linux-based FCI or availability group directly. A WSFC cannot be extended by a Pacemaker node and vice versa.
*   Mixing Linux distributions is not supported with FCIs or an availability group that has a cluster type of External. All availability group replicas in that scenario must be configured not only the same Linux distribution, but also the same version. The two supported ways that SQL Server can operate across the two platforms or multiple distributions of Linux are availability groups and log shipping.

Distributed availability groupsDistributed availability groups are designed to span availability group configurations, whether those two underlying clusters underneath the availability groups are two different WSFCs, Linux distributions, or one on a WSFC and the other on Linux. A distributed availability group will be the primary method of having a cross platform solution. A distributed availability group is also the primary solution for migrations such as converting from a Windows Server-based SQL Server infrastructure to a Linux-based one if that is what your company wants to do. As noted above, availability groups, and especially distributed availability groups, would minimize the time that an application would be unavailable for use. An example of a distributed availability group that spans a WSFC and Pacemaker is shown below.![Diagram showing a distributed availability group that spans a WSFC and Pacemaker.](Image00027.jpg)If an availability group is configured with a cluster type of None, it can span Windows Server and Linux as well as multiple Linux distributions. Since this is not a true high availability configuration, it should not be used for mission critical deployments, but for read-scale or migration/upgrade scenarios.Log shippingSince log shipping is just based on backup and restore, and there are no differences in the databases, file structures, etc., for SQL Server on Windows Server versus SQL Server on Linux. This means that log shipping can be configured between a Windows Server-based SQL Server installation and a Linux one as well as between distributions of Linux. Everything else remains the same. The only caveat is that log shipping, just like an availability group, cannot work when the source is at a higher SQL Server major version against a target that is at a lower version of SQL Server.read-scaleSince their introduction in SQL Server 2012, secondary replicas have had the ability to be used for read-only queries. There are two ways that can be achieved with an availability group: by allowing direct access to the secondary as well as configuring read only routing which requires the use of the listener. SQL Server 2016 introduced the ability to load balance read-only connections via the listener using a round robin algorithm, allowing read-only requests to be spread across all readable replicas.Scaling readable copies of a database via availability groups was first introduced with distributed availability groups in SQL Server 2016\. This would allow companies to have read-only copies of the database not only locally, but regionally and globally with a minimal amount of configuration and reduce network traffic and latency by having queries executed locally. Each primary replica of an availability group can seed two other availability groups even if it is not the fully read/write copy, so each distributed availability group can support up to 27 copies of the data that are readable.![Diagram showing a Distributed Availability Group related to read-scale.](Image00024.jpg)Starting with SQL Server 2017, It is possible to create a near-real time, read-only solution with availability groups configured with a cluster type of None. If the goal is to use availability groups for readable secondary replicas and not availability, doing this removes the complexity of using a WSFC or Pacemaker, and gives the readable benefits of an availability group in a simpler deployment method.The only major caveat is that due to no underlying cluster with a cluster type of None, configuring read only routing is a little different. From a SQL Server perspective, a listener is still required to route the requests even though there is no cluster. Instead of configuring a traditional listener, the IP address or name of the primary replica is used. The primary replica is then used to route the read only requests.A log shipping warm standby can technically be configured for readable usage by restoring the database WITH STANDBY. However, because the transaction logs require exclusive use of the database for restoration, it means that users cannot be accessing the database while that happens. This makes log shipping a less than ideal solution - especially if near real-time data is required.One thing that should be noted for all read-scale scenarios with availability groups is that unlike using transactional replication where all of the data is live, each secondary replica is not in a state where unique indexes can be applied, the replica is an exact copy of the primary. This means that if any indexes are required for reporting or data needs to be manipulated, it must be done on the database(s) on the primary replica. If you need that flexibility, replication is a better solution for readable data.SummaryInstances and databases of SQL Server 2017 can be made highly available using the same features on both Windows Server and Linux. Besides standard availability scenarios of local high availability and disaster recovery, downtime associated with upgrades and migrations can be minimized with the availability features in SQL Server. Availability groups can also provide additional copies of a database as part of the same architecture to scale out readable copies. Whether you are deploying a new solution using SQL Server 2017 or considering an upgrade, SQL Server 2017 has the availability and reliability you require.SQL Server availability basics for Linux deploymentsStarting with SQL Server 2017 (14.x), SQL Server is supported on both Linux and Windows. Like Windows-based SQL Server deployments, SQL Server databases and instances need to be highly available under Linux. This article covers the technical aspects of planning and deploying highly available Linux-based SQL Server databases and instances, as well as some of the differences from Windows-based installations. Because SQL Server may be new for Linux professionals, and Linux may be new for SQL Server professionals, the article at times introduces concepts that may be familiar to some and unfamiliar to others.SQL Server availability options for Linux deploymentsBesides backup and restore, the same three availability features are available on Linux as for Windows-based deployments:

*   Always On Availability Groups (AGs)
*   Always On Failover Cluster Instances (FCIs)
*   Log Shipping

On Windows, FCIs always require an underlying Windows Server failover cluster (WSFC). Depending on the deployment scenario, an AG usually requires an underlying WSFC, with the exception being the new None variant in SQL Server 2017 (14.x). A WSFC does not exist in Linux.A quick Linux primerWhile some Linux installations may be installed with an interface, most are not, meaning that nearly everything at the operating system layer is done via command line. The common term for this command line in the Linux world is a bash shell.In Linux, many commands need to be executed with elevated privileges, much like many things need to be done in Windows Server as an administrator. There are two main methods to execute with elevated privileges:

1.  Run in the context of the proper user. To change to a different user, use the command su. If su is executed on its own without a username, as long as you know the password, you will now be in a shell as root.
2.  The more common and security conscious way to run things is to use sudo before executing anything. Many of the examples in this article use sudo.

Some common commands, each of which have various switches and options that can be researched online:

*   cd - change the directory
*   chmod - change the permissions of a file or directory
*   chown - change the ownership of a file or directory
*   ls - show the contents of a directory
*   mkdir - create a folder (directory) on a drive
*   mv - move a file from one location to another
*   ps - show all of the working processes
*   rm - delete a file locally on a server
*   rmdir - delete a folder (directory)
*   systemctl - start, stop, or enable services
*   Text editor commands. On Linux, there are various text editor options, such as vi and emacs.

Common tasks for availability configurations of SQL Server on LinuxThis section covers tasks that are common to all Linux-based SQL Server deployments.Ensure that files can be copiedCopying files from one server to another is a task that anyone using SQL Server on Linux should be able to do. This task is very important for AG configurations.Things like permission issues can exist on Linux as well as on Windows-based installations. However, those familiar with how to copy from server to server on Windows may not be familiar with how it is done on Linux. A common method is to use the command-line utility scp, which stands for secure copy. Behind the scenes, scp uses OpenSSH. SSH stands for secure shell. Depending on the Linux distribution, OpenSSH itself may not be installed. If it is not, OpenSSH needs to be installed first.When using scp, you must provide the credentials of the server if it is not the source or destination. For example, usingBashscp MyAGCert.cer username@servername:/folder/subfoldercopies the file MyAGCert.cer to the folder specified on the other server. Note that you must have permissions - and possibly ownership - of the file to copy it, so chown may also need to be employed before copying. Similarly, on the receiving side, the right user needs access to manipulate the file. For example, to restore that certificate file, the mssql user must be able to access it.Samba, which is the Linux variant of server message block (SMB), can also be used to create shares accessed by UNC paths such as \\SERVERNAME\SHARE.Windows-based SMB shares can also be used; SMB shares do not need to be Linux-based, as long as the client portion of Samba is configured properly on the Linux server hosting SQL Server and the share has the right access. For those in a mixed environment, this would be one way to leverage existing infrastructure for Linux-based SQL Server deployments.One thing that is important is that the version of Samba deployed should be SMB 3.0 compliant. When SMB support was added in SQL Server 2012 (11.x), it required all shares to support SMB 3.0\. If using Samba for the share and not Windows Server, the Samba-based share should be using Samba 4.0 or later, and ideally 4.3 or later, which supports SMB 3.1.1.Finally, using a network file system (NFS) share is an option. Using NFS is not an option on Windows-based deployments of SQL Server, and can only be used for Linux-based deployments.Configure the firewallSimilar to Windows, Linux distributions have a built-in firewall. If your company is using an external firewall to the servers, disabling the firewalls in Linux may be acceptable. However, regardless of where the firewall is enabled, ports need to be opened. The following table documents the common ports needed for highly available SQL Server deployments on Linux.

| CONFIGURE THE FIREWALL |
| --- |
| Port Number | Type | Description |
| --- | --- | --- |
| 111 | TCP/UDP | NFS - rpcbind/sunrpc |
| 135 | TCP | Samba (if used) - End Point Mapper |
| 137 | UDP | Samba (if used) - NetBIOS Name Service |
| 138 | UDP | Samba (if used) - NetBIOS Datagram |
| 139 | TCP | Samba (if used) - NetBIOS Session |
| 445 | TCP | Samba (if used) - SMB over TCP |
| 1433 | TCP | SQL Server - default port; if desired, can change with mssql-conf set network.tcpport <portnumber> |
| 2049 | TCP, UDP | NFS (if used) |
| 2224 | TCP | Pacemaker - used by pcsd |
| 3121 | TCP | Pacemaker - Required if there are Pacemaker Remote nodes |
| 3260 | TCP | iSCSI Initiator (if used) - Can be altered in /etc/iscsi/iscsid.config (RHEL), but should match port of iSCSI Target |
| 5022 | TCP | SQL Server - default port used for an AG endpoint; can be changed when creating the endpoint |
| 5403 | TCP | Pacemaker |
| 5404 | UDP | Pacemaker - Required by Corosync if using multicast UDP |
| 5405 | UDP | Pacemaker - Required by Corosync |
| 21064 | TCP | Pacemaker - Required by resources using DLM |
| Variable | TCP | AG endpoint port; default is 5022 |
| Variable | TCP | NFS - port for LOCKD_TCPPORT (found in /etc/sysconfig/nfs on RHEL) |
| Variable | UDP | NFS - port for LOCKD_UDPPORT (found in /etc/sysconfig/nfs on RHEL) |
| Variable | TCP/UDP | NFS - port for MOUNTD_PORT (found in /etc/sysconfig/nfs on RHEL) |
| Variable | TCP/UDP | NFS - port for STATD_PORT (found in /etc/sysconfig/nfs on RHEL) |
|  |  |  |

Conversely, the name of the service under Linux can also be added as an exception instead of the port; for example, high-availability for Pacemaker. Refer to your distribution for the names if this is the direction you wish to pursue. For example, on RHEL the command to add in Pacemaker isBashsudo firewall-cmd --permanent --add-service=high-availabilityInstall SQL Server packages for availabilityOn a Windows-based SQL Server installation, some components are installed even in a basic engine install, while others are not. Under Linux, only the SQL Server engine is installed as part of the installation process. Everything else is optional. For highly available SQL Server instances under Linux, two packages should be installed with SQL Server: SQL Server Agent (mssql-server-agent) and the high availability (HA) package (mssql-server-ha). While SQL Server Agent is technically optional, it is SQL Server's scheduler for jobs and is required by log shipping, so installation is recommended. On Windows-based installations, SQL Server Agent is not optional.When AGs or FCIs are configured on a Windows-based configuration, they are cluster-aware. Cluster awareness means that SQL Server has specific resource DLLs that a WSFC knows about (sqagtres.dll and sqsrvres.dll for FCIs, hadrres.dll for AGs) and are used by the WSFC to ensure that the SQL Server clustered functionality is up, running, and functioning properly. Because clustering is external not only to SQL Server but Linux itself, Microsoft had to code the equivalent of a resource DLL for Linux-based AG and FCI deployments. This is the mssql-server-ha package, also known as the SQL Server resource agent for Pacemaker.The other optional packages for SQL Server on Linux, SQL Server Full-Text Search (mssql-server-fts) and SQL Server Integration Services (mssql-server-is), are not required for high availability, either for an FCI or an AG.Pacemaker for Always On Availability Groups and failover cluster instances on LinuxAs previous noted, the only clustering mechanism currently supported by Microsoft for AGs and FCIs is Pacemaker with Corosync. This section covers the basic information to understand the solution, as well as how to plan and deploy it for SQL Server configurations.HA add-on/extension basicsAll of the currently supported distributions ship a high availability add-on/extension, which is based on the Pacemaker clustering stack. This stack incorporates two key components: Pacemaker and Corosync. All the components of the stack are:

*   Pacemaker - The core clustering component, that does things like coordinate across the clustered machines.
*   Corosync - A framework and set of APIs that provides things like quorum, the ability to restart failed processes, and so on.
*   libQB - Provides things like logging.
*   Resource agent - Specific functionality provided so that an application can integrate with Pacemaker.
*   Fence agent - Scripts/functionality that assist in isolating nodes and deal with them if they are having issues.

This solution is in some ways similar to, but in many ways different from deploying clustered configurations using Windows. In Windows, the availability form of clustering, called a Windows Server failover cluster (WSFC), is built into the operating system, and the feature that enables the creation of a WSFC, failover clustering, is disabled by default. In Windows, AGs and FCIs are built on top of a WSFC, and share tight integration because of the specific resource DLL that is provided by SQL Server. This tightly coupled solution is possible by and large because it is all from one vendor.![HA Basics](Image00028.jpg)On Linux, while each supported distribution has Pacemaker available, each distribution can customize and have slightly different implementations and versions. Some of the differences will be reflected in the instructions in this article. The clustering layer is open source, so even though it ships with the distributions, it is not tightly integrated in the same way a WSFC is under Windows. This is why Microsoft provides mssql-server-ha, so that SQL Server and the Pacemaker stack can provide close to, but not exactly the same, experience for AGs and FCIs as under Windows.Pacemaker concepts and terminologyThis section documents the common concepts and terminology for a Pacemaker implementation.NodeA node is a server participating in the cluster. A Pacemaker cluster natively supports up to 16 nodes. This number can be exceeded if Corosync is not running on additional nodes, but Corosync is required for SQL Server. Therefore, the maximum number of nodes a cluster can have for any SQL Server-based configuration is 16; this is the Pacemaker limit, and has nothing to do with maximum limitations for AGs or FCIs imposed by SQL Server.ResourceBoth a WSFC and a Pacemaker cluster have the concept of a resource. A resource is specific functionality that runs in context of the cluster, such as a disk or an IP address. For example, under Pacemaker both FCI and AG resources can get created. This is not dissimilar to what is done in a WSFC, where you see a SQL Server resource for either an FCI or an AG resource when configuring an AG, but is not exactly the same due to the underlying differences in how SQL Server integrates with Pacemaker.Pacemaker has standard and clone resources. Clone resources are ones that run simultaneously on all nodes. An example would be an IP address that runs on multiple nodes for load balancing purposes. Any resource that gets created for FCIs uses a standard resource, since only one node can host an FCI at any given time.Resource groups/setsSimilar to roles in a WSFC, a Pacemaker cluster has the concept of a resource group. A resource group (called a set in SLES) is a collection of resources that function together and can fail over from one node to another as a single unit. Resource groups cannot contain resources that are configured as master or slave; thus, they cannot be used for AGs. While a resource group can be used for FCIs, it is not generally a recommended configuration.ConstraintsWSFCs have various parameters for resources as well as things like dependencies, which tell the WSFC of a parent/child relationship between two different resources. A dependency is just a rule telling the WSFC which resource needs to be online first.A Pacemaker cluster does not have the concept of dependencies, but there are constraints. There are three kinds of constraints: colocation, location, and ordering.

*   A colocation constraint enforces whether or not two resources should be running on the same node.
*   A location constraint tells the Pacemaker cluster where a resource can (or cannot) run.
*   An ordering constraint tells the Pacemaker cluster the order in which the resources should start.

Quorum, fence agents, and STONITHQuorum under Pacemaker is somewhat similar to a WSFC in concept. The whole purpose of a cluster's quorum mechanism is to ensure that the cluster stays up and running. Both a WSFC and the HA add-ons for the Linux distributions have the concept of voting, where each node counts towards quorum. You want a majority of the votes up, otherwise, in a worst case scenario, the cluster will be shut down.Unlike a WSFC, there is no witness resource to work with quorum. Like a WSFC, the goal is to keep the number of voters odd. Quorum configuration has different considerations for AGs than FCIs.WSFCs monitor the status of the nodes participating and handle them when a problem occurs. Later versions of WSFCs offer such features as quarantining a node that is misbehaving or unavailable (node is not on, network communication is down, etc.). On the Linux side, this type of functionality is provided by a fence agent. The concept is sometimes referred to as fencing. However, these fence agents are generally specific to the deployment, and often provided by hardware vendors and some software vendors, such as those who provide hypervisors. For example, VMware provides a fence agent that can be used for Linux VMs virtualized using vSphere.Quorum and fencing ties into another concept called STONITH, or Shoot the Other Node in the Head. STONITH is required to have a supported Pacemaker cluster on all Linux distributions.corosync.confThe corosync.conf file contains the configuration of the cluster. It is located in /etc/corosync. In the course of normal day-to-day operations, this file should never have to be edited if the cluster is set up properly.Cluster log locationLog locations for Pacemaker clusters differ depending on the distribution.

*   RHEL and SLES - /var/log/cluster/corosync.log
*   Ubuntu - /var/log/corosync/corosync.log

To change the default logging location, modify corosync.conf.Plan Pacemaker clusters for SQL ServerThis section discusses the important planning points for a Pacemaker cluster.Virtualizing Linux-based Pacemaker clusters for SQL ServerUsing virtual machines to deploy Linux-based SQL Server deployments for AGs and FCIs is covered by the same rules as for their Windows-based counterparts. There is a base set of rules for supportability of virtualized SQL Server deployments provided by Microsoft in Microsoft Support KB 956893\. Different hypervisors such as Microsoft's Hyper-V and VMware's ESXi may have different variances on top of that, due to differences in the platforms themselves.When it comes to AGs and FCIs under virtualization, ensure that anti-affinity is set for the nodes of a given Pacemaker cluster. When configured for high availability in an AG or FCI configuration, the VMs hosting SQL Server should never be running on the same hypervisor host. For example, if a two-node FCI is deployed, there would need to be at least three hypervisor hosts so that there is somewhere for one of the VMs hosting a node to go in the event of a host failure, especially if using features like Live Migration or vMotion.NetworkingUnlike a WSFC, Pacemaker does not require a dedicated name or at least one dedicated IP address for the Pacemaker cluster itself. AGs and FCIs will require IP addresses (see the documentation for each for more information), but not names, since there is no network name resource. SLES does allow the configuration of an IP address for administration purposes, but it is not required.Like a WSFC, Pacemaker would prefer redundant networking, meaning distinct network cards (NICs or pNICs for physical) having individual IP addresses. In terms of the cluster configuration, each IP address would have what is known as its own ring. However, as with WSFCs today, many implementations are virtualized or in the public cloud where there is really only a single virtualized NIC (vNIC) presented to the server. If all pNICs and vNICs are connected to the same physical or virtual switch, there is no true redundancy at the network layer, so configuring multiple NICs is a bit of an illusion to the virtual machine. Network redundancy is usually built into the hypervisor for virtualized deployments, and is definitely built into the public cloud.One difference with multiple NICs and Pacemaker versus a WSFC is that Pacemaker allows multiple IP addresses on the same subnet, whereas a WSFC does not.Quorum and STONITHQuorum configuration and requirements are related to AG or FCI-specific deployments of SQL Server.STONITH is required for a supported Pacemaker cluster. Use the documentation from the distribution to configure STONITH.InteroperabilityThis section documents how a Linux-based cluster can interact with a WSFC or with other distributions of Linux.WSFCCurrently, there is no direct way for a WSFC and a Pacemaker cluster to work together. This means that there is no way to create an AG or FCI that works across a WSFC and Pacemaker. However, there are two interoperability solutions, both of which are designed for AGs. The only way an FCI can participate in a cross-platform configuration is if it is participating as an instance in one of these two scenarios:

*   An AG with a cluster type of None.
*   A distributed AG, which is a special type of availability group that allows two different AGs to be configured as their own availability group.

Other Linux distributionsOn Linux, all nodes of a Pacemaker cluster must be on the same distribution. For example, this means that a RHEL node cannot be part of a Pacemaker cluster that has a SLES node. The main reason for this was previously stated: the distributions may have different versions and functionality, so things could not work properly. Mixing distributions has the same story as mixing WSFCs and Linux: use None or distributed AGs.Backup and restore SQL Server databases on LinuxYou can take backups of databases from SQL Server 2017 on Linux with many different options. On a Linux server, you can use sqlcmd to connect to the SQL Server and take backups. From Windows, you can connect to SQL Server on Linux and take backups with the user interface. The backup functionality is the same across platforms. For example, you can backup databases locally, to remote drives, or to Microsoft Azure Blob storage service.SQL Server on Linux only supports backing up to Azure Blob storage using block blobs. Using a storage key for backup and restore will result in a page blog being used, which isn't supported. Use a Shared Access Signature instead.Backup a databaseIn the following example sqlcmd connects to the local SQL Server instance and takes a full backup of a user database called demodb.Bashsqlcmd -S localhost -U SA -Q "BACKUP DATABASE [demodb] TO DISK = N'/var/opt/mssql/data/demodb.bak' WITH NOFORMAT, NOINIT, NAME = 'demodb-full', SKIP, NOREWIND, NOUNLOAD, STATS = 10"When you run the command, SQL Server will prompt for a password. After you enter the password, the shell will return the results of the backup progress. For example:Password:10 percent processed.21 percent processed.32 percent processed.40 percent processed.51 percent processed.61 percent processed.72 percent processed.80 percent processed.91 percent processed.Processed 296 pages for database 'demodb', file 'demodb' on file 1.100 percent processed.Processed 2 pages for database 'demodb', file 'demodb_log' on file 1.BACKUP DATABASE successfully processed 298 pages in 0.064 seconds (36.376 MB/sec).Backup the transaction logIf your database is in the full recovery model, you can also make transaction log backups for more granular restore options. In the following example, sqlcmd connects to the local SQL Server instance and takes a transaction log backup.Bashsqlcmd -S localhost -U SA -Q "BACKUP LOG [demodb] TO DISK = N'/var/opt/mssql/data/demodb_LogBackup.bak' WITH NOFORMAT, NOINIT, NAME = N'demodb_LogBackup', NOSKIP, NOREWIND, NOUNLOAD, STATS = 5"Restore a databaseIn the following example sqlcmd connects to the local instance of SQL Server and restores the demodb database. Note that the NORECOVERY option is used to allow for additional restores of log file backups. If you do not plan to restore additional log files, remove the NORECOVERY option.Bashsqlcmd -S localhost -U SA -Q "RESTORE DATABASE [demodb] FROM DISK = N'/var/opt/mssql/data/demodb.bak' WITH FILE = 1, NOUNLOAD, REPLACE, NORECOVERY, STATS = 5"Restore the transaction logThe following command restores the previous transaction log backup.Bashsqlcmd -S localhost -U SA -Q "RESTORE LOG demodb FROM DISK = N'/var/opt/mssql/data/demodb_LogBackup.bak'"Backup and Restore with SQL Server Management Studio (SSMS)You can use SSMS from a Windows computer to connect to a Linux database and take a backup through the user-interface.The following steps walk through taking a backup with SSMS.

1.  Start SSMS and connect to your server in SQL Server 2017 on Linux.
2.  In Object Explorer, right-click on your database, Click Tasks, and then click Back Up....
3.  In the Backup Up Database dialog, verify the parameters and options, and click OK.

SQL Server completes the database backup.Restore with SQL Server Management Studio (SSMS)The following steps walk you through restoring a database with SSMS.

1.  In SSMS right-click Databases and click Restore Databases....
2.  Under Source click Device: and then click the ellipses (...).
3.  Locate your database backup file and click OK.
4.  Under Restore plan, verify the backup file and settings. Click OK.
5.  SQL Server restores the database.

SQL Server on Linux VDI client SDK SpecificationThis covers the interfaces provided by the SQL Server on Linux virtual device interface (VDI) client SDK. Independent software vendors (ISVs) can use the Virtual Backup Device Application Programming Interface (API) to integrate SQL Server into their products. In general, VDI on Linux behaves similarly to VDI on Windows with the following changes:

*   Windows Shared Memory becomes POSIX shared memory.
*   Windows Semaphores become POSIX semaphores.
*   Windows types like HRESULT and DWORD are changed to integer equivalents.
*   The COM interfaces are removed and replaced with a pair of C++ Classes.
*   SQL Server on Linux does not support named instances so references to instance name have been removed.
*   The shared library is implemented in libsqlvdi.so installed at /opt/mssql/lib/libsqlvdi.so

This document is an addendum to vbackup.chm that details the MS SQL Server VDI Specifications on Windows.User Permissions SetupOn Linux, POSIX primitives are owned by the user creating them and their default group. For objects created by SQL Server, these will by default be owned by the mssql user and the mssql group. To allow sharing between SQL Server and the VDI client, one of the following two methods are recommended:

1.  Run the VDI Client as the mssql user

Execute the following command to switch to mssql user:Bashsudo su mssql

2.  Add the mssql user to the vdiuser's group, and the vdiuser to the mssql group.

Execute the following commands:Bashsudo useradd vdiusersudo usermod -a -G mssql vdiusersudo usermod -a -G vdiuser mssqlRestart the server to pick up new groups for SQL Server and vdiuserClient FunctionsThis chapter contains descriptions of each of the client functions. The descriptions include the following information:

*   Function purpose
*   Function syntax
*   Parameter list
*   Return values
*   Remarks

ClientVirtualDeviceSet::CreatePurpose This function creates the virtual device set.Syntaxint ClientVirtualDeviceSet::Create (char *​ name,​ ​ // name for the setVDConfig   *​ cfg​ ​ // configuration for the set);

| CLIENTVIRTUALDEVICESET::CREATE |
| --- |
| Parameters | Argument | Explanation |
| --- | --- | --- |
|  | name | This identifies the virtual device set. The rules for names used by CreateFileMapping() must be followed. Any character except backslash () may be used. This is a character string. Prefixing the string with the user's product or company name and database name is recommended. |
|  | cfg | This is the configuration for the virtual device set. For more information, see "Configuration" later in this document. |
|  |  |  |

| CLIENTVIRTUALDEVICESET::CREATE |
| --- |
| Return Values | Argument | Explanation |
| --- | --- | --- |
|  | NOERROR | The function succeeded. |
|  | VD_E_NOTSUPPORTED | One or more of the fields in the configuration was invalid or otherwise unsupported. |
|  | VD_E_PROTOCOL | The virtual device set already exists. |
|  |  |  |

Remarks The Create method should be called only once per BACKUP or RESTORE operation. After invoking the Close method, the client can reuse the interface to create another virtual device set.ClientVirtualDeviceSet::GetConfigurationPurpose This function is used to wait for the server to configure the virtual device set. Syntaxint ClientVirtualDeviceSet::GetConfiguration (time_t​ ​ timeout,​ // in millisecondsVDConfig *​ ​ cfg​ // selected configuration);

| CLIENTVIRTUALDEVICESET::GETCONFIGURATION |
| --- |
| Parameters | Argument | Explanation |
| --- | --- | --- |
|  | timeout | This is the time-out in milliseconds. Use INFINITE or any negative integer to prevent time-out. |
|  | cfg | Upon successful execution, this contains the configuration selected by the server. For more information, see "Configuration" later in this document. |
|  |  |  |

| CLIENTVIRTUALDEVICESET::GETCONFIGURATION |
| --- |
| Return Values | Argument | Explanation |
| --- | --- | --- |
|  | NOERROR | The configuration was returned. |
|  | VD_E_ABORT | SignalAbort was invoked. |
|  | VD_E_TIMEOUT | The function timed out. |
|  |  |  |

Remarks This function blocks in an Alertable state. After successful invocation, the devices in the virtual device set may be opened.ClientVirtualDeviceSet::OpenDevicePurpose This function opens one of the devices in the virtual device set. Syntaxint ClientVirtualDeviceSet::OpenDevice (char *​ ​ name,​ ​ // name for the setClientVirtualDevice **​ ​ ppVirtualDevice​ // returns interface to device);

| CLIENTVIRTUALDEVICESET::OPENDEVICE |
| --- |
| Parameters | Argument | Explanation |
| --- | --- | --- |
|  | name | This identifies the virtual device set. |
|  | ppVirtualDevice | When the function succeeds, a pointer to the virtual device is returned. This device is used for GetCommand and CompleteCommand. |
|  | NOERROR | The function succeeded. |
|  | VD_E_ABORT | Abort was requested. |
|  | VD_E_OPEN | All devices are open. |
|  | VD_E_PROTOCOL | The set is not in the initializing state or this particular device is already open. |
|  | VD_E_INVALID | The device name is invalid. It is not one of the names known to comprise the set. |
|  |  |  |

Remarks VD_E_OPEN may be returned without problem. The client may call OpenDevice by means of a loop until this code is returned. If more than one device is configured, for example n devices, the virtual device set will return n unique device interfaces.The GetConfiguration function can be used to wait until the devices can be opened. If this function does not succeed, then a null value is returned through the ppVirtualDevice.ClientVirtualDevice::GetCommandPurpose This function is used to obtain the next command queued to a device. When requested, this function waits for the next command.Syntaxint ClientVirtualDevice::GetCommand (time_t​ ​ timeout,​ // time-out in millisecondsVDC_Command**​ ppCmd​ // returns the next command);

| CLIENTVIRTUALDEVICE::GETCOMMAND |
| --- |
| Parameters | Argument | Explanation |
| --- | --- | --- |
|  | timeout | This is the time to wait, in milliseconds. Use INFINTE to wait indefinitely. Use 0 to poll for a command. VD_E_TIMEOUT is returned if no command is currently available . If the time-out occurs, the client decides the next action. |
|  | Timeout | This is the time to wait, in milliseconds. Use INFINTE or a negative value to wait indefinitely. Use 0 to poll for a command. VD_E_TIMEOUT is returned if no command is available before the timeout expires. If the timeout occurs, the client decides the next action. |
|  | ppCmd | When a command is successfully returned, the parameter returns the address of a command to execute. The memory returned is read-only. When the command is completed, this pointer is passed to the CompleteCommand routine. For details about each command, see "Commands" later in this document. |
|  |  |  |

| CLIENTVIRTUALDEVICE::GETCOMMAND |
| --- |
| Return Values | Argument | Explanation |
| --- | --- | --- |
|  | NOERROR | A command was fetched. |
|  | VD_E_CLOSE | The device has been closed by the server. |
|  | VD_E_TIMEOUT | No command was available and the time-out expired. |
|  | VD_E_ABORT | Either the client or the server has used the SignalAbort to force a shutdown. |
|  |  |  |

Remarks When VD_E_CLOSE is returned, SQL Server has closed the device. This is part of the normal shutdown. After all devices have been closed, the client invokes ClientVirtualDeviceSet::Close to close the virtual device set. When this routine must block to wait for a command, the thread is left in an Alertable condition.ClientVirtualDevice::CompleteCommandPurpose This function is used to notify SQL Server that a command has finished. Completion information appropriate for the command should be returned. For more information, see "Commands" later in this document.Syntaxint ClientVirtualDevice::CompleteCommand (VDC_Command pCmd,​ ​ // the commandint ​ completionCode,​ ​ // completion codeunsigned long ​ bytesTransferred,​ // bytes transferredint64_t ​ position​ ​ // current position);

| CLIENTVIRTUALDEVICE::COMPLETECOMMAND |
| --- |
| Parameters | Argument | Explanation |
| --- | --- | --- |
|  | pCmd | This is the address of a command previously returned from ClientVirtualDevice::GetCommand. |
|  | completionCode | This is a status code that indicates the completion status. This parameter must be returned for all commands. The code returned should be appropriate to the command being performed. ERROR_SUCCESS is used in all cases to denote a successfully executed command. For the complete list of possible codes, see the file, vdierror.h. A list of typical status codes for each command appears in "Commands" later in this document. |
|  | bytesTransferred | This is the number of successfully transferred bytes. This is returned only for data transfer commands Read and Write. |
|  | position | This is a response to the GetPosition command only. |
|  |  |  |

| CLIENTVIRTUALDEVICE::COMPLETECOMMAND |
| --- |
| Return Values | Argument | Explanation |
| --- | --- | --- |
|  | NOERROR | The completion was correctly noted. |
|  | VD_E_INVALID | pCmd was not an active command. |
|  | VD_E_ABORT | Abort was signaled. |
|  | VD_E_PROTOCOL | The device is not open. |
|  |  |  |

Remarks NoneClientVirtualDeviceSet::SignalAbortPurpose This function is used to signal that an abnormal termination should occur.Syntaxint ClientVirtualDeviceSet::SignalAbort ();

| CLIENTVIRTUALDEVICESET::SIGNALABORT |
| --- |
| Parameters | Argument | Explanation |
| --- | --- | --- |
|  | None | Not applicable |
|  |  |  |

| CLIENTVIRTUALDEVICESET::SIGNALABORT |
| --- |
| Return Values | Argument | Explanation |
| --- | --- | --- |
|  | NOERROR | The Abort notification was successfully posted. |
|  |  |  |

Remarks At any time, the client may choose to abort the BACKUP or RESTORE operation. This routine signals that all operations should cease. The state of the overall virtual device set enters an Abnormally Terminated state. No further commands are returned on any devices. All uncompleted commands are automatically completed, returning ERROR_OPERATION_ABORTED as a completion code. The client should call ClientVirtualDeviceSet::Close after it has safely terminated any outstanding use of buffers provided to the client. For more information, see "Abnormal Termination" earlier in this document.ClientVirtualDeviceSet::ClosePurpose This function closes the virtual device set created by ClientVirtualDeviceSet::Create. It results in the release of all resources associated with the virtual device set.Syntaxint ClientVirtualDeviceSet::Close ();

| CLIENTVIRTUALDEVICESET::CLOSE |
| --- |
| Parameters | Argument | Explanation |
| --- | --- | --- |
|  | None | Not applicable |
|  |  |  |

| CLIENTVIRTUALDEVICESET::CLOSE |
| --- |
| Return Values | Argument | Explanation |
| --- | --- | --- |
|  | NOERROR | This is returned when the virtual device set was successfully closed. |
|  | VD_E_PROTOCOL | No action was taken because the virtual device set was not open. |
|  | VD_E_OPEN | Devices were still open. |
|  |  |  |

Remarks The invocation of Close is a client declaration that all resources used by the virtual device set should be released. The client must ensure that all activity involving data buffers and virtual devices is terminated before invoking Close. All virtual device interfaces returned by OpenDevice are invalidated by Close. The client is permitted to issue a Create call on the virtual device set interface after the Close call is returned. Such a call would create a new virtual device set for a subsequent BACKUP or RESTORE operation. If Close is called when one or more virtual devices are still open, VD_E_OPEN is returned. In this case, SignalAbort is internally triggered, to ensure a proper shutdown if possible. VDI resources are released. The client should wait for a VD_E_CLOSE indication on each device before invoking ClientVirtualDeviceSet::Close. If the client knows that the virtual device set is already in an Abnormally Terminated state, then it should not expect a VD_E_CLOSE indication from GetCommand, and may invoke ClientVirtualDeviceSet::Close as soon as activity on the shared buffers is terminated. For more information, see "Abnormal Termination" earlier in this document.ClientVirtualDeviceSet::OpenInSecondaryPurpose This function opens the virtual device set in a secondary client. The primary client must have already used Create and GetConfiguration to set up the virtual device set.Syntaxint ClientVirtualDeviceSet::OpenInSecondary (char *​ setName​ ​ // name of the set);

| CLIENTVIRTUALDEVICESET::OPENINSECONDARY |
| --- |
| Parameters | Argument | Explanation |
| --- | --- | --- |
|  | setName | This identifies the set. This name is case-sensitive and must match the name used by the primary client when it invoked ClientVirtualDeviceSet::Create. |
|  |  |  |

| CLIENTVIRTUALDEVICESET::OPENINSECONDARY |
| --- |
| Return Values | Argument | Explanation |
| --- | --- | --- |
|  | NOERROR | The function succeeded. |
|  | VD_E_PROTOCOL | The virtual device set has not been created, has already been opened on this client, or the virtual device set is not ready to accept open requests from secondary clients. |
|  | VD_E_ABORT | The operation is being aborted. |
|  |  |  |

Remarks When using a multiple process model, the primary client is responsible for detecting normal and abnormal termination of secondary clients.ClientVirtualDeviceSet::GetBufferHandlePurpose Some applications may require more than one process to operate on the buffers returned by ClientVirtualDevice::GetCommand. In such cases, the process that receives the command can use GetBufferHandle to obtain a process independent handle that identifies the buffer. This handle can then be communicated to any other process that also has the same Virtual Device Set open. That process would then use ClientVirtualDeviceSet::MapBufferHandle to obtain the address of the buffer. The address will likely be a different address than in its partner because each process may be mapping buffers at different addresses.Syntaxint ClientVirtualDeviceSet::GetBufferHandle (uint8_t*​ ​ pBuffer,​ ​ // in: buffer addressunsigned int*​ ​ pBufferHandle​ // out: buffer handle);

| CLIENTVIRTUALDEVICESET::GETBUFFERHANDLE |
| --- |
| Parameters | Argument | Explanation |
| --- | --- | --- |
|  | pBuffer | This is the address of a buffer obtained from a Read or Write command. |
|  | BufferHandle | A unique identifier for the buffer is returned. |
|  |  |  |

| CLIENTVIRTUALDEVICESET::GETBUFFERHANDLE |
| --- |
| Return Values | Argument | Explanation |
| --- | --- | --- |
|  | NOERROR | The function succeeded. |
|  | VD_E_PROTOCOL | The virtual device set is not currently open. |
|  | VD_E_INVALID | The pBuffer is not a valid address. |
|  |  |  |

Remarks The process that invokes the GetBufferHandle function is responsible for invoking ClientVirtualDevice::CompleteCommand when the data transfer is complete.ClientVirtualDeviceSet::MapBufferHandlePurpose This function is used to obtain a valid buffer address from a buffer handle obtained from some other process.Syntaxint ClientVirtualDeviceSet::MapBufferHandle (i​ ​ nt ​ dwBuffer,​ // in: buffer handleuint8_t**​ ppBuffer​ ​ // out: buffer address);

| CLIENTVIRTUALDEVICESET::MAPBUFFERHANDLE |
| --- |
| Parameters | Argument | Explanation |
| --- | --- | --- |
|  | dwBuffer | This is the handle returned by ClientVirtualDeviceSet::GetBufferHandle. |
|  | ppBuffer | This is the address of the buffer that is valid in the current process. |
|  |  |  |

| CLIENTVIRTUALDEVICESET::MAPBUFFERHANDLE |
| --- |
| Return Values | Argument | Explanation |
| --- | --- | --- |
|  | NOERROR | The function succeeded. |
|  | VD_E_PROTOCOL | The virtual device set is not currently open. |
|  | VD_E_INVALID | The ppBuffer is an invalid handle. |
|  |  |  |

Remarks Care must be taken to communicate the handles correctly. Handles are local to a single virtual device set. The partner processes sharing a handle must ensure that buffer handles are used only within the scope of the virtual device set from which the buffer was originally obtained.Failover Cluster Instances - SQL Server on LinuxThis describes the concepts related to SQL Server failover cluster instances (FCI) on Linux.The Clustering Layer

*   In RHEL, the clustering layer is based on Red Hat Enterprise Linux (RHEL) HA add-on.
*   In SLES, the clustering layer is based on SUSE Linux Enterprise High Availability Extension (HAE).

Both the RHEL HA add-on and the SUSE HAE are built on Pacemaker.As the following diagram shows, storage is presented to two servers. Clustering components - Corosync and Pacemaker - coordinate communications and resource management. One of the servers has the active connection to the storage resources and the SQL Server. When Pacemaker detects a failure the clustering components manage moving the resources to the other node.![Red Hat Enterprise Linux 7 Shared Disk SQL Cluster](Image00029.jpg)At this point, SQL Server's integration with Pacemaker on Linux is not as coupled as with WSFC on Windows. From within SQL, there is no knowledge about the presence of the cluster, all orchestration is outside in and the service is controlled as a standalone instance by Pacemaker. Also, virtual network name is specific to WSFC, there is no equivalent of the same in Pacemaker. It is expected that @@servername and sys.servers to return the node name, while the cluster dmvs sys.dm_os_cluster_nodes and sys.dm_os_cluster_properties will no records. To use a connection string that points to a string server name and not use the IP, they will have to register in their DNS server the IP used to create the virtual IP resource (as explained in the following sections) with the chosen server name.Number of Instances and NodesOne key difference with SQL Server on Linux is that there can only be one install of SQL Server per Linux server. That installation is called an instance. This means that unlike Windows Server which supports up to 25 FCIs per Windows Server failover cluster (WSFC), a Linux-based FCI will only have a single instance. This one instance is also a default instance; there is no concept of a named instance on Linux.A Pacemaker cluster can only have up to 16 nodes when Corosync is involved, so a single FCI can span up to 16 servers. An FCI implemented with Standard Edition of SQL Server supports up to two nodes of a cluster even if the Pacemaker cluster has the maximum 16 nodes.In a SQL Server FCI, the SQL Server instance is active on either one node or the other.IP Address and NameOn a Linux Pacemaker cluster, each SQL Server FCI needs its own unique IP address and name. If the FCI configuration spans multiple subnets, one IP address will be required per subnet. The unique name and IP address(es) are used to access the FCI so that applications and end users do not need to know which underlying server of the Pacemaker cluster.The name of the FCI in DNS should be the same as the name of the FCI resource that gets created in the Pacemaker cluster. Both the name and IP address must be registered in DNS.Shared StorageAll FCIs, whether they are on Linux or Windows Server, require some form of shared storage. This storage is presented to all servers that can possibly host the FCI, but only a single server can use the storage for the FCI at any given time. The options available for shared storage under Linux are:

*   iSCSI
*   Network File System (NFS)
*   Server Message Block (SMB) Under Windows Server, there are slightly different options. One option not currently supported for Linux-based FCIs is the ability to use a disk that is local to the node for TempDB, which is SQL Server's temporary workspace.

In a configuration that spans multiple locations, what is stored at one data center must be synchronized with the other. In the event of a failover, the FCI will be able to come online and the storage is seen to be the same. Achieving this will require some external method for storage replication, whether it is done via the underlying storage hardware or some software-based utility.The process for presenting shared storage is the same for the different supported methods:

*   Configure the shared storage
*   Mount the storage as a folder to the servers that will serve as nodes of the Pacemaker cluster for the FCI
*   If required, move the SQL Server system databases to shared storage
*   Test that SQL Server works from each server connected to the shared storage

One major difference with SQL Server on Linux is that while you can configure the default user data and log file location, the system databases must always exist at /var/opt/mssql/data. On Windows Server, there is the ability to move the system databases including TempDB. This fact plays into how shared storage is configured for an FCI.The default paths for non-system databases can be changed using the mssql-conf utility. You can also store SQL Server data and transaction in other locations as long as they have the proper security even if it is not a default location; the location would need to be stated.Configure RHEL failover cluster instance (FCI) cluster for SQL ServerThis provides instructions to create a two-node shared disk failover cluster for SQL Server on Red Hat Enterprise Linux. The clustering layer is based on Red Hat Enterprise Linux (RHEL) HA add-on built on top of Pacemaker. The SQL Server instance is active on either one node or the other.As the following diagram shows, storage is presented to two servers. Clustering components - Corosync and Pacemaker - coordinate communications and resource management. One of the servers has the active connection to the storage resources and the SQL Server. When Pacemaker detects a failure the clustering components manage moving the resources to the other node.![Red Hat Enterprise Linux 7 Shared Disk SQL Cluster](Image00029.jpg)The following sections walk through the steps to set up a failover cluster solution.To complete the following end-to-end scenario, you need two machines to deploy the two nodes cluster and another server to configure the NFS server. Below steps outline how these servers will be configured.Setup and configure the operating system on each cluster nodeThe first step is to configure the operating system on the cluster nodes. For this walk through, use RHEL with a valid subscription for the HA add-on.Install and configure SQL Server on each cluster node

1.  Install and setup SQL Server on both nodes.
2.  Designate one node as primary and the other as secondary, for purposes of configuration. Use these terms for the following this guide.
3.  On the secondary node, stop and disable SQL Server.

The following example stops and disables SQL Server:Bashsudo systemctl stop mssql-serversudo systemctl disable mssql-serverAt setup time, a Server Master Key is generated for the SQL Server instance and placed at /var/opt/mssql/secrets/machine-key. On Linux, SQL Server always runs as a local account called mssql. Because it's a local account, its identity isn't shared across nodes. Therefore, you need to copy the encryption key from primary node to each secondary node so each local mssql account can access it to decrypt the Server Master Key.

1.  On the primary node, create a SQL server login for Pacemaker and grant the login permission to run sp_server_diagnostics. Pacemaker uses this account to verify which node is running SQL Server.

Bashsudo systemctl start mssql-serverConnect to the SQL Server master database with the sa account and run the following:bashsqlUSE [master]GOCREATE LOGIN [<loginName>] with PASSWORD= N'<loginPassword>'ALTER SERVER ROLE [sysadmin] ADD MEMBER [<loginName>]Alternatively, you can set the permissions at a more granular level. The Pacemaker login requires VIEW SERVER STATE to query health status with sp_server_diagnostics, setupadmin and ALTER ANY LINKED SERVER to update the FCI instance name with the resource name by running sp_dropserver and sp_addserver.

2.  On the primary node, stop and disable SQL Server.
3.  Configure the hosts file for each cluster node. The host file must include the IP address and name of every cluster node.

Check the IP address for each node. The following script shows the IP address of your current node.Bashsudo ip addr showSet the computer name on each node. Give each node a unique name that is 15 characters or less. Set the computer name by adding it to /etc/hosts. The following script lets you edit /etc/hosts with vi.Bashsudo vi /etc/hostsThe following example shows /etc/hosts with additions for two nodes named sqlfcivm1 and sqlfcivm2.Bash127.0.0.1   localhost localhost4 localhost4.localdomain4::1       localhost localhost6 localhost6.localdomain610.128.18.128 sqlfcivm110.128.16.77 sqlfcivm2In the next section you will configure shared storage and move your database files to that storage.Configure shared storage and move database filesThere are a variety of solutions for providing shared storage. This walk-through demonstrates configuring shared storage with NFS. We recommend to follow best practices and use Kerberos to secure NFS.On the NFS Server do the following:

1.  Install nfs-utils

Bashsudo yum -y install nfs-utils

2.  Enable and start rpcbind

Bashsudo systemctl enable rpcbind && sudo systemctl start rpcbind

3.  Enable and start nfs-server

Bashsudo systemctl enable nfs-server && sudo systemctl start nfs-server

4.  Edit /etc/exports to export the directory you want to share. You need 1 line for each share you want. For example:

Bash/mnt/nfs  10.8.8.0/24(rw,sync,no_subtree_check,no_root_squash)

1.  Export the shares

Bashsudo exportfs -rav

2.  Verify that the paths are shared/exported, run from the NFS server

Bashsudo showmount -e

3.  Add exception in SELinux

Bashsudo setsebool -P nfs_export_all_rw 1

4.  Open the firewall the server.

Bashsudo firewall-cmd --permanent --add-service=nfssudo firewall-cmd --permanent --add-service=mountdsudo firewall-cmd --permanent --add-service=rpc-bindsudo firewall-cmd --reloadConfigure all cluster nodes to connect to the NFS shared storageDo the following steps on all cluster nodes.

1.  Install nfs-utils

Bashsudo yum -y install nfs-utils

1.  Open up the firewall on clients and NFS server

Bashsudo firewall-cmd --permanent --add-service=nfssudo firewall-cmd --permanent --add-service=mountdsudo firewall-cmd --permanent --add-service=rpc-bindsudo firewall-cmd --reload

2.  Verify that you can see the NFS shares on client machines

Bashsudo showmount -e <IP OF NFS SERVER>

3.  Repeat these steps on all cluster nodes.

Mount database files directory to point to the shared storage

1.  On the primary node only , save the database files to a temporary location.The following script, creates a new temporary directory, copies the database files to the new directory, and removes the old database files. As SQL Server runs as local user mssql, you need to make sure that after data transfer to the mounted share, local user has read-write access to the share.

$ sudo su mssql$ mkdir /var/opt/mssql/tmp$ cp /var/opt/mssql/data/* /var/opt/mssql/tmp$ rm /var/opt/mssql/data/*$ exit

1.  On all cluster nodes edit /etc/fstab file to include the mount command.

Bash<IP OF NFS SERVER>:<shared_storage_path> <database_files_directory_path> nfs timeo=14,intrThe following script shows an example of the edit.10.8.8.0:/mnt/nfs /var/opt/mssql/data nfs timeo=14,intr

1.  Run mount -a command for the system to update the mounted paths.
2.  Copy the database and log files that you saved to /var/opt/mssql/tmp to the newly mounted share /var/opt/mssql/data. This only needs to be done on the primary node. Make sure that you give read write permissions to 'mssql' local user.

$ sudo chown mssql /var/opt/mssql/data$ sudo chgrp mssql /var/opt/mssql/data$ sudo su mssql$ cp /var/opt/mssql/tmp/* /var/opt/mssql/data/$ rm /var/opt/mssql/tmp/*$ exit

1.  Validate that SQL Server starts successfully with the new file path. Do this on each node. At this point only one node should run SQL Server at a time. They cannot both run at the same time because they will both try to access the data files simultaneously (to avoid accidentally starting SQL Server on both nodes, use a File System cluster resource to make sure the share is not mounted twice by the different nodes). The following commands start SQL Server, check the status, and then stop SQL Server.

Bashsudo systemctl start mssql-serversudo systemctl status mssql-serversudo systemctl stop mssql-serverAt this point both instances of SQL Server are configured to run with the database files on the shared storage. The next step is to configure SQL Server for Pacemaker.Install and configure Pacemaker on each cluster node

2.  On both cluster nodes, create a file to store the SQL Server username and password for the Pacemaker login. The following command creates and populates this file:

Bashsudo touch /var/opt/mssql/secrets/passwdecho '<loginName>' | sudo tee -a /var/opt/mssql/secrets/passwdecho '<loginPassword>' | sudo tee -a /var/opt/mssql/secrets/passwdsudo chown root:root /var/opt/mssql/secrets/passwdsudo chmod 600 /var/opt/mssql/secrets/passwd    

3.  On both cluster nodes, open the Pacemaker firewall ports. To open these ports with firewalld, run the following command:

Bashsudo firewall-cmd --permanent --add-service=high-availabilitysudo firewall-cmd --reloadIf you're using another firewall that doesn't have a built-in high-availability configuration, the following ports need to be opened for Pacemaker to be able to communicate with other nodes in the cluster

*   TCP: Ports 2224, 3121, 21064
*   UDP: Port 5405

4.  Install Pacemaker packages on each node.

Bashsudo yum install pacemaker pcs fence-agents-all resource-agents

5.  Set the password for the default user that is created when installing Pacemaker and Corosync packages. Use the same password on both nodes.

Bashsudo passwd hacluster

6.  Enable and start pcsd service and Pacemaker. This will allow nodes to rejoin the cluster after the reboot. Run the following command on both nodes.

Bashsudo systemctl enable pcsdsudo systemctl start pcsdsudo systemctl enable pacemaker

7.  Install the FCI resource agent for SQL Server. Run the following commands on both nodes.

Bashsudo yum install mssql-server-haCreate the cluster

1.  On one of the nodes, create the cluster.

Bashsudo pcs cluster auth <nodeName1 nodeName2 ...> -u haclustersudo pcs cluster setup --name <clusterName> <nodeName1 nodeName2 ...>sudo pcs cluster start --all

2.  Configure the cluster resources for SQL Server, File System and virtual IP resources and push the configuration to the cluster. You need the following information:
    *   SQL Server Resource Name: A name for the clustered SQL Server resource.
    *   Floating IP Resource Name: A name for the virtual IP address resource.
    *   IP Address: The IP address that clients will use to connect to the clustered instance of SQL Server.
    *   File System Resource Name: A name for the File System resource.
    *   device: The NFS share path
    *   device: The local path that it's mounted to the share
    *   fstype: File share type (i.e. nfs)

Update the values from the following script for your environment. Run on one node to configure and start the clustered service.Bashsudo pcs cluster cib cfgsudo pcs -f cfg resource create <sqlServerResourceName> ocf:mssql:fcisudo pcs -f cfg resource create <floatingIPResourceName> ocf:heartbeat:IPaddr2 ip=<ip Address>sudo pcs -f cfg resource create <fileShareResourceName> Filesystem device=<networkPath> directory=<localPath>         fstype=<fileShareType>sudo pcs -f cfg constraint colocation add <virtualIPResourceName> <sqlResourceName>sudo pcs -f cfg constraint colocation add <fileShareResourceName> <sqlResourceName>sudo pcs cluster cib-push cfgFor example, the following script creates a SQL Server clustered resource named mssqlha, and a floating IP resources with IP address 10.0.0.99\. It also creates a Filesystem resource and adds constraints so all resources are colocated on same node as SQL resource.Bashsudo pcs cluster cib cfgsudo pcs -f cfg resource create mssqlha ocf:mssql:fcisudo pcs -f cfg resource create virtualip ocf:heartbeat:IPaddr2 ip=10.0.0.99sudo pcs -f cfg resource create fs Filesystem device="10.8.8.0:/mnt/nfs" directory="/var/opt/mssql/data" fstype="nfs"sudo pcs -f cfg constraint colocation add virtualip mssqlhasudo pcs -f cfg constraint colocation add fs mssqlhasudo pcs cluster cib-push cfgAfter the configuration is pushed, SQL Server will start on one node.

3.  Verify that SQL Server is started.

Bashsudo pcs statusThe following examples shows the results when Pacemaker has successfully started a clustered instance of SQL Server.fs     (ocf::heartbeat:Filesystem):    Started sqlfcivm1virtualip     (ocf::heartbeat:IPaddr2):      Started sqlfcivm1mssqlha  (ocf::mssql:fci): Started sqlfcivm1PCSD Status:sqlfcivm1: Onlinesqlfcivm2: OnlineDaemon Status:corosync: active/disabledpacemaker: active/enabledpcsd: active/enabledOperate RHEL failover cluster instance (FCI) for SQL ServerThis describes how to do the following tasks for SQL Server on a shared disk failover cluster with Red Hat Enterprise Linux.

*   Manually failover the cluster
*   Monitor a failover cluster SQL Server service
*   Add a cluster node
*   Remove a cluster node
*   Change the SQL Server resource monitoring frequency

Architecture descriptionThe clustering layer is based on Red Hat Enterprise Linux (RHEL) HA add-on built on top of Pacemaker. Corosync and Pacemaker coordinate cluster communications and resource management. The SQL Server instance is active on either one node or the other.The following diagram illustrates the components in a Linux cluster with SQL Server.![Red Hat Enterprise Linux 7 Shared Disk SQL Cluster](Image00029.jpg)Failover cluster manuallyThe resource move command creates a constraint forcing the resource to start on the target node.  After executing the move command, executing resource clear will remove the constraint so it is possible to move the resource again or have the resource automatically fail over.Bashsudo pcs resource move <sqlResourceName> <targetNodeName> sudo pcs resource clear <sqlResourceName>The following example moves the mssqlha resource to a node named sqlfcivm2, and then removes the constraint so that the resource can move to a different node later.Bashsudo pcs resource move mssqlha sqlfcivm2sudo pcs resource clear mssqlhaMonitor a failover cluster SQL Server serviceView the current cluster status:Bashsudo pcs statusView live status of cluster and resources:Bashsudo crm_monView the resource agent logs at /var/log/cluster/corosync.logAdd a node to a cluster

1.  Check the IP address for each node. The following script shows the IP address of your current node.

Baship addr show

2.  The new node needs a unique name that is 15 characters or less. By default in Red Hat Linux the computer name is localhost.localdomain. This default name may not be unique and is too long. Set the computer name the new node. Set the computer name by adding it to /etc/hosts. The following script lets you edit /etc/hosts with vi.

Bashsudo vi /etc/hostsThe following example shows /etc/hosts with additions for three nodes named sqlfcivm1, sqlfcivm2, andsqlfcivm3.127.0.0.1   localhost localhost4 localhost4.localdomain4::1         localhost localhost6 localhost6.localdomain610.128.18.128 fcivm110.128.16.77 fcivm210.128.14.26 fcivm3The file should be the same on every node.

3.  Stop the SQL Server service on the new node.
4.  Follow the instructions to mount the database file directory to the shared location:

From the NFS server, install nfs-utilsBashsudo yum -y install nfs-utilsOpen up the firewall on clients and NFS serverBashsudo firewall-cmd --permanent --add-service=nfssudo firewall-cmd --permanent --add-service=mountdsudo firewall-cmd --permanent --add-service=rpc-bindsudo firewall-cmd --reloadEdit /etc/fstab file to include the mount command:Bash<IP OF NFS SERVER>:<shared_storage_path> <database_files_directory_path> nfs timeo=14,intrRun mount -a for the changes to take effect.

5.  On the new node, create a file to store the SQL Server username and password for the Pacemaker login. The following command creates and populates this file:

Bashsudo touch /var/opt/mssql/passwdsudo echo "<loginName>" >> /var/opt/mssql/secrets/passwdsudo echo "<loginPassword>" >> /var/opt/mssql/secrets/passwdsudo chown root:root /var/opt/mssql/passwdsudo chmod 600 /var/opt/mssql/passwd

6.  On the new node, open the Pacemaker firewall ports. To open these ports with firewalld, run the following command:

Bashsudo firewall-cmd --permanent --add-service=high-availabilitysudo firewall-cmd --reload

7.  Install Pacemaker packages on the new node.

Bashsudo yum install pacemaker pcs fence-agents-all resource-agents

8.  Set the password for the default user that is created when installing Pacemaker and Corosync packages. Use the same password as the existing nodes.

Bashsudo passwd hacluster

9.  Enable and start pcsd service and Pacemaker. This will allow the new node to rejoin the cluster after the reboot. Run the following command on the new node.

Bashsudo systemctl enable pcsdsudo systemctl start pcsdsudo systemctl enable pacemaker

10.  Install the FCI resource agent for SQL Server. Run the following commands on the new node.

Bashsudo yum install mssql-server-ha

11.  On an existing node from the cluster, authenticate the new node and add it to the cluster:

Bashsudo pcs    cluster auth <nodeName3> -u haclustersudo pcs    cluster node add <nodeName3>The following example adds a node named vm3 to the cluster.Bashsudo pcs    cluster auth  sudo pcs    cluster startRemove nodes from a clusterTo remove a node from a cluster run the following command:Bashsudo pcs    cluster node remove <nodeName>Change the frequency of sqlservr resource monitoring intervalBashsudo pcs    resource op monitor interval=<interval>s <sqlResourceName>The following example sets the monitoring interval to 2 seconds for the mssql resource:Bashsudo pcs    resource op monitor interval=2s mssqlhaTroubleshoot Red Hat Enterprise Linux shared disk cluster for SQL ServerIn troubleshooting the cluster it may help to understand how the three daemons work together to manage cluster resources.

| TROUBLESHOOT RED HAT ENTERPRISE LINUX SHARED DISK CLUSTER FOR SQL SERVER |
| --- |
| Daemon | Description |
| --- | --- |
| Corosync | Provides quorum membership and messaging between cluster nodes. |
| Pacemaker | Resides on top of Corosync and provides state machines for resources. |
| PCSD | Manages both Pacemaker and Corosync through the pcs tools |
|  |  |

PCSD must be running in order to use pcs tools.Current cluster statussudo pcs status returns basic information about the cluster, quorum, nodes, resources, and daemon status for each node.An example of a healthy pacemaker quorum output would be:Cluster name: MyAppSQLLast updated: Wed Oct 31 12:00:00 2016  Last change: Wed Oct 31 11:00:00 2016 by root via crm_resource on sqlvmnode1Stack: corosyncCurrent DC: sqlvmnode1  (version 1.1.13-10.el7_2.4-44eb2dd) - partition with quorum3 nodes and 1 resource configuredOnline: [ sqlvmnode1 sqlvmnode2 sqlvmnode3]Full list of resources:mssqlha (ocf::sql:fci): Started sqlvmnode1PCSD Status:sqlvmnode1: Onlinesqlvmnode2: Onlinesqlvmnode3: OnlineDaemon Status:corosync: active/disabledpacemaker: active/enabledIn the example, partition with quorum means that a majority quorum of nodes is online. If the cluster loses a majority quorum of nodes , pcs status will return partition WITHOUT quorum and all resources will be stopped.online: [sqlvmnode1 sqlvmnode2 sqlvmnode3] returns the name of all nodes currently participating in the cluster. If any nodes are not participating, pcs status returns OFFLINE: [<nodename>].PCSD Status shows the cluster status for each node.Reasons why a node may be offlineCheck the following items when a node is offline.

*   Firewall

The following ports need to be open on all nodes for Pacemaker to be able to communicate.

*   **TCP: 2224, 3121, 21064

*   Pacemaker or Corosync services running
*   Node communication
*   Node name mappings

Always On Availability Groups on LinuxThis describes the characteristics of Always On Availability Groups (AGs) under Linux-based SQL Server installations. It also covers differences between Linux- and Windows Server failover cluster (WSFC)-based AGs.From a high-level standpoint, availability groups under SQL Server on Linux are the same as they are on WSFC-based implementations. That means that all the limitations and features are the same, with some exceptions. The main differences include:

*   Microsoft Distributed Transaction Coordinator (DTC) is supported under Linux starting with SQL Server 2017 CU16\. However, DTC is not yet supported on Availability Groups on Linux. If your applications require the use of distributed transactions and need an AG, deploy SQL Server on Windows.
*   Linux-based deployments that require high availability use Pacemaker for clustering instead of a WSFC.
*   Unlike most configurations for AGs on Windows except for the Workgroup Cluster scenario, Pacemaker never requires Active Directory Domain Services (AD DS).
*   How to fail an AG from one node to another is different between Linux and Windows.
*   Certain settings such as required_synchronized_secondaries_to_commit can only be changed via Pacemaker on Linux, whereas a WSFC-based install uses Transact-SQL.

Number of replicas and cluster nodesAn AG in SQL Server Standard can have two total replicas: one primary, and one secondary that can only be used for availability purposes. It cannot be used for anything else, such as readable queries. An AG in SQL Server Enterprise can have up to nine total replicas: one primary and up to eight secondaries, of which up to three (including the primary) can be synchronous. If using an underlying cluster, there can be a maximum of 16 nodes total when Corosync is involved. An availability group can span at most nine of the 16 nodes with SQL Server Enterprise, and two with SQL Server Standard.A two-replica configuration that requires the ability to automatically fail over to another replica requires the use of a configuration-only replica. Configuration-only replicas were introduced in SQL Server 2017 (14.x) Cumulative Update 1 (CU1), so that should be the minimum version deployed for this configuration.If Pacemaker is used, it must be properly configured so it remains up and running. That means that quorum and STONITH must be implemented properly from a Pacemaker perspective, in addition to any SQL Server requirements such as a configuration-only replica.Readable secondary replicas are only supported with SQL Server Enterprise.Cluster type and failover modeNew to SQL Server 2017 (14.x) is the introduction of a cluster type for AGs. For Linux, there are two valid values: External and None. A cluster type of External means that Pacemaker will be used underneath the AG. Using External for cluster type requires that the failover mode be set to External as well (also new in SQL Server 2017 (14.x)). Automatic failover is supported, but unlike a WSFC, failover mode is set to External, not automatic, when Pacemaker is used. Unlike a WSFC, the Pacemaker portion of the AG is created after the AG is configured.A cluster type of None means that there is no requirement for, nor will the AG use, Pacemaker. Even on servers that have Pacemaker configured, if an AG is configured with a cluster type of None, Pacemaker will not see or manage that AG. A cluster type of None only supports manual failover from a primary to a secondary replica. An AG created with None is primarily targeted for the read-scale out scenario as well as upgrades. While it can work in scenarios like disaster recovery or local availability where no automatic failover is necessary, it is not recommended. The listener story is also more complex without Pacemaker.Cluster type is stored in the SQL Server dynamic management view (DMV) sys.availability_groups, in the columns cluster_type and cluster_type_desc.required_synchronized_secondaries_to_commitNew to SQL Server 2017 (14.x) is a setting that is used by AGs called required_synchronized_secondaries_to_commit. This tells the AG the number of secondary replicas that must be in lockstep with the primary. This enables things like automatic failover (only when integrated with Pacemaker with a cluster type of External), and controls the behavior of things like the availability of the primary if the right number of secondary replicas is either online or offline.The required_synchronized_secondaries_to_commit value is set by default and maintained by Pacemaker/ SQL Server. You can manually override this value.The combination of required_synchronized_secondaries_to_commit and the new sequence number (which is stored in sys.availability_groups) informs Pacemaker and SQL Server that, for example, automatic failover can happen. In that case, a secondary replica would have the same sequence number as the primary, meaning it is up to date with all the latest configuration information.There are three values that can be set for required_synchronized_secondaries_to_commit: 0, 1, or 2\. They control the behavior of what happens when a replica becomes unavailable. The numbers correspond to the number of secondary replicas that must be synchronized with the primary. The behavior is as follows under Linux:

*   0 - Secondary replicas do not need to be in synchronized state with the primary. However if the secondaries are not synchronized, there will be no automatic failover.
*   1 - One secondary replica must be in a synchronized state with the primary; automatic failover is possible. The primary database is unavailable until a secondary synchronous replica is available.
*   2 - Both secondary replicas in a three or more node AG configuration must be synchronized with the primary; automatic failover is possible.

required_synchronized_secondaries_to_commit controls not only the behavior of failovers with synchronous replicas, but data loss. With a value of 1 or 2, a secondary replica is always required to be synchronized, so there will always be data redundancy. That means no data loss.To change the value of required_synchronized_secondaries_to_commit, use the following syntax:Red Hat Enterprise Linux (RHEL) and UbuntuBashsudo pcs resource update <AGResourceName> required_synchronized_secondaries_to_commit=<Value>SUSE Linux Enterprise Server (SLES)Bashsudo crm resource param ms-<AGResourceName> set required_synchronized_secondaries_to_commit <value>where AGResourceName is the name of the resource configured for the AG, and Value is 0, 1, or 2\. To set it back to the default of Pacemaker managing the parameter, execute the same statement with no value.Automatic failover of an AG is possible when the following conditions are met:

*   The primary and the secondary replica are set to synchronous data movement.
*   The secondary has a state of synchronized (not synchronizing), meaning the two are at the same data point.
*   The cluster type is set to External. Automatic failover is not possible with a cluster type of None.
*   The sequence_number of the secondary replica to become the primary has the highest sequence number - in other words, the secondary replica's sequence_number matches the one from the original primary replica.

If these conditions are met and the server hosting the primary replica fails, the AG will change ownership to a synchronous replica. The behavior for synchronous replicas (of which there can be three total: one primary and two secondary replicas) can further be controlled by required_synchronized_secondaries_to_commit. This works with AGs on both Windows and Linux, but is configured completely differently. On Linux, the value is configured automatically by the cluster on the AG resource itself.Configuration-only replica and quorumAlso new in SQL Server 2017 (14.x) as of CU1 is a configuration-only replica. Because Pacemaker is different than a WSFC, especially when it comes to quorum and requiring STONITH, having just a two-node configuration will not work when it comes to an AG. For an FCI, the quorum mechanisms provided by Pacemaker can be fine, because all FCI failover arbitration happens at the cluster layer. For an AG, arbitration under Linux happens in SQL Server, where all the metadata is stored. This is where the configuration-only replica comes into play.Without anything else, a third node and at least one synchronized replica would be required. The configuration-only replica stores the AG configuration in the master database, same as the other replicas in the AG configuration. The configuration-only replica does not have the user databases participating in the AG. The configuration data is sent synchronously from the primary. This configuration data is then used during failovers, whether they are automatic or manual.For an AG to maintain quorum and enable automatic failovers with a cluster type of External, it either must:

*   Have three synchronous replicas (SQL Server Enterprise only); or
*   Have two replicas (primary and secondary) as well as a configuration only replica.

Manual failovers can happen whether using External or None cluster types for AG configurations. While a configuration-only replica can be configured with an AG that has a cluster type of None, it is not recommended, since it complicates the deployment. For those configurations, manually modify required_synchronized_secondaries_to_commit to have a value of at least 1, so that there is at least one synchronized replica.A configuration-only replica can be hosted on any edition of SQL Server, including SQL Server Express. This will minimize licensing costs and ensures it works with AGs in SQL Server Standard. This means that the third required server just needs to meet the minimum specification for SQL Server, since it is not receiving user transaction traffic for the AG.When a configuration-only replica is used, it has the following behavior:

*   By default, required_synchronized_secondaries_to_commit is set to 0\. This can be manually modified to 1 if desired.
*   If the primary fails and required_synchronized_secondaries_to_commit is 0, the secondary replica will become the new primary and be available for both reading and writing. If the value is 1, automatic failover will occur, but will not accept new transactions until the other replica is online.
*   If a secondary replica fails and required_synchronized_secondaries_to_commit is 0, the primary replica still accepts transactions, but if the primary fails at this point, there is no protection for the data nor failover possible (manual or automatic), since a secondary replica is not available.
*   If the configuration-only replicas fails, the AG will function normally, but no automatic failover is possible.
*   If both a synchronous secondary replica and the configuration-only replica fail, the primary cannot accept transactions, and there is nowhere for the primary to fail to.

In CU1 there is a known bug in the logging in the corosync.log file that is generated via mssql-server-ha. If a secondary replica is not able to become the primary due to the number of required replicas available, the current message says "Expected to receive 1 sequence numbers but only received 2\. Not enough replicas are online to safely promote the local replica." The numbers should be reversed, and it should say "Expected to receive 2 sequence numbers but only received 1\. Not enough replicas are online to safely promote the local replica."Multiple availability groupsMore than one AG can be created per Pacemaker cluster or set of servers. The only limitation is system resources. AG ownership is shown by the master. Different AGs can be owned by different nodes; they do not all need to be running on the same node.Drive and folder location for databasesAs on Windows-based AGs, the drive and folder structure for the user databases participating in an AG should be identical. For example, if the user databases are in /var/opt/mssql/userdata on Server A, that same folder should exist on Server B.The listener under LinuxThe listener is optional functionality for an AG. It provides a single point of entry for all connections (read/write to the primary replica and/or read-only to secondary replicas) so that applications and end users do not need to know which server is hosting the data. In a WSFC, this is the combination of a network name resource and an IP resource, which is then registered in AD DS (if needed) as well as DNS. In combination with the AG resource itself, it provides that abstraction.The listener under Linux is configured differently, but its functionality is the same. There is no concept of a network name resource in Pacemaker, nor is an object created in AD DS; there is just an IP address resource created in Pacemaker that can run on any of the nodes. An entry associated with the IP resource for the listener in DNS with a "friendly name" needs to be created. The IP resource for the listener will only be active on the server hosting the primary replica for that availability group.If Pacemaker is used and an IP address resource is created that is associated with the listener, there will be a brief outage as the IP address stops on the one server and starts on the other, whether it is automatic or manual failover. While this provides abstraction through the combination of a single name and IP address, it does not mask the outage. An application must be able to handle the disconnect by having some sort of functionality to detect this and reconnect.However, the combination of the DNS name and IP address is still not enough to provide all the functionality that a listener on a WSFC provides, such as read-only routing for secondary replicas. When configuring an AG, a "listener" still needs to be configured in SQL Server. This can be seen in the wizard as well as the Transact-SQL syntax. There are two ways that this can be configured to function the same as on Windows:

*   For an AG with a cluster type of External, the IP address associated with the "listener" created in SQL Server should be the IP address of the resource created in Pacemaker.
*   For an AG created with a cluster type of None, use the IP address associated with the primary replica.

The instance associated with the provided IP address then becomes the coordinator for things like the read-only routing requests from applications.Interoperability with Windows-based availability groups and replicasAn AG that has a cluster type of External or one that is WSFC cannot have its replicas cross platforms. This is true whether the AG is SQL Server Standard or SQL Server Enterprise. That means in a traditional AG configuration with an underlying cluster, one replica cannot be on a WSFC and the other on Linux with Pacemaker.An AG with a cluster type of NONE can have its replicas cross OS boundaries, so there could be both Linux- and Windows-based replicas in the same AG. An example is shown here where the primary replica is Windows-based, while the secondary is on one of the Linux distributions.![Hybrid None](Image00030.jpg)A distributed AG can also cross OS boundaries. The underlying AGs are bound by the rules for how they are configured, such as one configured with External being Linux-only, but the AG that it is joined to could be configured using a WSFC. Consider the following example:![Hybrid Dist AG](Image00031.jpg)High availability and data protection for availability group configurationsThis presents supported deployment configurations for SQL Server Always On availability groups on Linux servers. An availability group supports high availability and data protection. Automatic failure detection, automatic failover, and transparent reconnection after failover provide high availability. Synchronized replicas provide data protection.On a Windows Server Failover Cluster (WSFC), a common configuration for high availability uses two synchronous replicas and a third server or file share to provide quorum. The file-share witness validates the availability group configuration - status of synchronization, and the role of the replica, for example. This configuration ensures that the secondary replica chosen as the failover target has the latest data and availability group configuration changes.The WSFC synchronizes configuration metadata for failover arbitration between the availability group replicas and the file-share witness. When an availability group is not on a WSFC, the SQL Server instances store configuration metadata in the master database.For example, an availability group on a Linux cluster has CLUSTER_TYPE = EXTERNAL. There is no WSFC to arbitrate failover. In this case the configuration metadata is managed and maintained by the SQL Server instances. Because there is no witness server in this cluster, a third SQL Server instance is required to store configuration state metadata. All three SQL Server instances together provide distributed metadata storage for the cluster.The cluster manager can query the instances of SQL Server in the availability group, and orchestrate failover to maintain high availability. In a Linux cluster, Pacemaker is the cluster manager.SQL Server 2017 CU 1 enables high availability for an availability group with CLUSTER_TYPE = EXTERNAL for two synchronous replicas plus a configuration only replica. The configuration only replica can be hosted on any edition of SQL Server 2017 CU1 or later - including SQL Server Express edition. The configuration only replica maintains configuration information about the availability group in the master database but does not contain the user databases in the availability group.How the configuration affects default resource settingsSQL Server 2017 introduces the REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT cluster resource setting. This setting guarantees the specified number of secondary replicas write the transaction data to log before the primary replica commits each transaction. When you use an external cluster manager, this setting affects both high availability and data protection. The default value for the setting depends on the architecture at the time the cluster resource is created. When you install the SQL Server resource agent - mssql-server-ha - and create a cluster resource for the availability group, the cluster manager detects the availability group configuration and sets REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT accordingly.If supported by the configuration, the resource agent parameter REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT is set to the value that provides high availability and data protection.The following sections explain the default behavior for the cluster resource.Choose an availability group design to meet specific business requirements for high availability, data protection, and read-scale.The following configurations describe the availability group design patterns and the capabilities of each pattern. These design patterns apply to availability groups with CLUSTER_TYPE = EXTERNAL for high availability solutions.

*   Three synchronous replicas
*   Two synchronous replicas
*   Two synchronous replicas and a configuration only replica

Three synchronous replicasThis configuration consists of three synchronous replicas. By default, it provides high availability and data protection. It can also provide read-scale.![Three replicas](Image00032.jpg)An availability group with three synchronous replicas can provide read-scale, high availability, and data protection. The following table describes availability behavior.

| THREE SYNCHRONOUS REPLICAS |
| --- |
| Availability behavior | read-scale | High availability & data protection | Data protection |
| --- | --- | --- | --- |
| REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT= | 0 | 1* | 2 |
| Primary outage | Automatic failover. New primary is R/W.  | Automatic failover. New primary is R/W.  | Automatic failover. New primary is not available for user transactions until former primary recovers and joins availability group as secondary.  |
| One secondary replica outage   | Primary is R/W. No automatic failover if primary fails. | Primary is R/W. No automatic failover if primary fails as well. | Primary is not available for user transactions.  |
|  |  |  |  |

Two synchronous replicasThis configuration enables data protection. Like the other availability group configurations, it can enable read-scale. The two synchronous replicas configuration does not provide automatic high availability. A two replica configuration is only applicable to SQL Server 2017 RTM and is no longer supported with higher (CU1 and beyond) versions of SQL Server 2017..![Two synchronous replicas](Image00033.jpg)An availability group with two synchronous replicas provides read-scale and data protection. The following table describes availability behavior.

| TWO SYNCHRONOUS REPLICAS |
| --- |
| Availability behavior | read-scale | Data protection |
| --- | --- | --- |
| REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT= | 0 * | 1 |
| Primary outage | Manual failover. Might have data loss. New primary is R/W. | Automatic failover. New primary is not available for user transactions until former primary recovers and joins availability group as secondary. |
| One secondary replica outage   | Primary is R/W, running exposed to data loss.  | Primary is not available for user transactions until secondary recovers. |
|  |  |  |

Two synchronous replicas and a configuration only replicaAn availability group with two (or more) synchronous replicas and a configuration only replica provides data protection and may also provide high availability. The following diagram represents this architecture:![Configuration only availability group](Image00034.jpg)

1.  Synchronous replication of user data to the secondary replica. It also includes availability group configuration metadata.
2.  Synchronous replication of availability group configuration metadata. It does not include user data.

In the availability group diagram, a primary replica pushes configuration data to both the secondary replica and the configuration only replica. The secondary replica also receives user data. The configuration only replica does not receive user data. The secondary replica is in synchronous availability mode. The configuration only replica does not contain the databases in the availability group - only metadata about the availability group. Configuration data on the configuration only replica is committed synchronously.The default value for REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT is 0. The following table describes availability behavior.

| Availability behavior | High availability & data protection | Data protection |
| --- | --- | --- |
| REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT= | 0 * | 1 |
| Primary outage | Automatic failover. New primary is R/W. | Automatic failover. New primary is not available for user transactions. |
| Secondary replica outage | Primary is R/W, running exposed to data loss (if primary fails and cannot be recovered). No automatic failover if primary fails as well.  | Primary is not available for user transactions. No replica to fail over to if primary fails as well.  |
| Configuration only replica outage | Primary is R/W. No automatic failover if primary fails as well.  | Primary is R/W. No automatic failover if primary fails as well.  |
| Synchronous secondary + configuration only replica outage | Primary is not available for user transactions. No automatic failover.  | Primary is not available for user transactions. No replica to failover to if primary fails as well.  |

Requirements

*   All replicas in an availability group with a configuration only replica must be SQL Server 2017 CU 1 or later.
*   Any edition of SQL Server can host a configuration only replica, including SQL Server Express.
*   The availability group needs at least one secondary replica - in addition to the primary replica.
*   Configuration only replicas do not count towards the maximum number of replicas per instance of SQL Server. SQL Server standard edition allows up to three replicas, SQL Server Enterprise Edition allows up to 9.

Considerations

*   No more than one configuration only replica per availability group.
*   A configuration only replica cannot be a primary replica.
*   You cannot modify the availability mode of a configuration only replica. To change from a configuration only replica to a synchronous or asynchronous secondary replica, remove the configuration only replica, and add a secondary replica with the required availability mode.
*   A configuration only replica is synchronous with the availability group metadata. There is no user data.
*   An availability group with one primary replica and one configuration only replica, but no secondary replica is not valid.
*   You cannot create an availability group on an instance of SQL Server Express edition.

Understand SQL Server resource agent for pacemakerSQL Server 2017 CTP 1.4 added sequence_number to sys.availability_groups to allow Pacemaker to identify how up-to-date secondary replicas are with the primary replica. sequence_number is a monotonically increasing BIGINT that represents how up-to-date the local availability group replica is. Pacemaker updates the sequence_number with each availability group configuration change. Examples of configuration changes include failover, replica addition, or removal. The number is updated on the primary, then replicated to secondary replicas. Thus a secondary replica that has up-to-date configuration has the same sequence number as the primary.When Pacemaker decides to promote a replica to primary, it first sends a pre-promote notification to all replicas. The replicas return the sequence number. Next, when Pacemaker actually tries to promote a replica to primary, the replica only promotes itself if its sequence number is the highest of all the sequence numbers. If its own sequence number does not match the highest sequence number, the replica rejects the promote operation. In this way only the replica with the highest sequence number can be promoted to primary, ensuring no data loss.This process requires at least one replica available for promotion with the same sequence number as the previous primary. The Pacemaker resource agent sets REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT such that at least one synchronous secondary replica is up-to-date and available to be the target of an automatic failover by default. With each monitoring action, the value of REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT is computed (and updated if necessary). The REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT value is 'number of synchronous replicas' divided by 2\. At failover time, the resource agent requires (total number of replicas - REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT replicas) to respond to the pre-promote notification. The replica with the highest sequence_number is promoted to primary.For example, An availability group with three synchronous replicas - one primary replica and two synchronous secondary replicas.

*   REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT is 1; (3 / 2 -> 1).
*   The required number of replicas to respond to pre-promote action is 2; (3 - 1 = 2).

In this scenario, two replicas have to respond for the failover to be triggered. For successful automatic failover after a primary replica outage, both secondary replicas need to be up-to-date and respond to the pre-promote notification. If they are online and synchronous, they have the same sequence number. The availability group promotes one of them. If only one of the secondary replicas responds to the pre-promote action, the resource agent cannot guarantee that the secondary that responded has the highest sequence_number, and a failover is not triggered.You can choose to override the default behavior, and prevent the availability group resource from setting REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT automatically.The following script sets REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT to 0 on an availability group named <**ag1**>. Before you run replace <**ag1**> with the name of your availability group.Bashsudo pcs resource update <**ag1**> required_synchronized_secondaries_to_commit=0To revert to default value, based on the availability group configuration run:Bashsudo pcs resource update <**ag1**> required_synchronized_secondaries_to_commit=SQL Server Always On Availability Group for high availability on LinuxThis describes how to create a SQL Server Always On Availability Group (AG) for high availability on Linux. There are two configuration types for AGs. A high availability configuration uses a cluster manager to provide business continuity. This configuration can also include read-scale replicas. This document explains how to create the AG for high availability.You can also create an AG without a cluster manager for read-scale. The AG for read scale only provides read-only replicas for performance scale-out. It does not provide high availability.Configurations that guarantee high availability and data protection require either two or three synchronous commit replicas. With three synchronous replicas, the AG can automatically recover even if one server is not available.All servers must be either physical or virtual, and virtual servers must be on the same virtualization platform. This requirement is because the fencing agents are platform specific.RoadmapThe steps to create an AG on Linux servers for high availability are different from the steps on a Windows Server failover cluster. The following list describes the high-level steps:

1.  Configure SQL Server on three cluster servers.
2.  Create the AG. This step is covered in this current article.
3.  Configure a cluster resource manager, like Pacemaker.

Production environments require a fencing agent, like STONITH for high availability. The demonstrations in this documentation do not use fencing agents. The demonstrations are for testing and validation only.A Linux cluster uses fencing to return the cluster to a known state. The way to configure fencing depends on the distribution and the environment. Currently, fencing is not available in some cloud environments.

4.  Add the AG as a resource in the cluster.

PrerequisitesBefore you create the availability group, you need to:

*   Set your environment so that all the servers that will host availability replicas can communicate.
*   Install SQL Server.

To set the computer name, edit /etc/hostname. The following script lets you edit /etc/hostname with vi:Bashsudo vi /etc/hostname

1.  Configure the hosts file.

The hosts file on every server contains the IP addresses and names of all servers that will participate in the availability group.The following command returns the IP address of the current server:Bashsudo ip addr showUpdate /etc/hosts. The following script lets you edit /etc/hosts with vi:Bashsudo vi /etc/hostsThe following example shows /etc/hosts on node1 with additions for node1, node2, and node3\. In this document, node1 refers to the server that hosts the primary replica. And node2 and node3 refer to servers that host the secondary replicas.127.0.0.1   localhost localhost4 localhost4.localdomain4::1       localhost localhost6 localhost6.localdomain610.128.18.12 node110.128.16.77 node210.128.15.33 node3Enable AlwaysOn availability groups and restart mssql-serverEnable AlwaysOn availability groups on each node that hosts a SQL Server instance. Then restart mssql-server. Run the following script:Bashsudo /opt/mssql/bin/mssql-conf set hadr.hadrenabled  1sudo systemctl restart mssql-serverEnable an AlwaysOn_health event sessionYou can optionally enable AlwaysOn availability groups extended events to help with root-cause diagnosis when you troubleshoot an availability group. Run the following command on each instance of SQL Server:SQLALTER EVENT SESSION   AlwaysOn_health ON SERVER WITH (STARTUP_STATE=ON );GOFor more information about this XE session, see Always On extended events.Create a certificateThe SQL Server service on Linux uses certificates to authenticate communication between the mirroring endpoints.The following Transact-SQL script creates a master key and a certificate. It then backs up the certificate and secures the file with a private key. Update the script with strong passwords. Connect to the primary SQL Server instance. To create the certificate, run the following Transact-SQL script:SQLCREATE MASTER KEY ENCRYPTION BY PASSWORD = '**<Master_Key_Password>**';CREATE CERTIFICATE dbm_certificate WITH SUBJECT = 'dbm';BACKUP CERTIFICATE dbm_certificateTO FILE = '/var/opt/mssql/data/dbm_certificate.cer'WITH PRIVATE KEY (FILE = '/var/opt/mssql/data/dbm_certificate.pvk',ENCRYPTION BY PASSWORD = '**<Private_Key_Password>**');At this point, your primary SQL Server replica has a certificate at /var/opt/mssql/data/dbm_certificate.cer and a private key at var/opt/mssql/data/dbm_certificate.pvk. Copy these two files to the same location on all servers that will host availability replicas. Use the mssql user, or give permission to the mssql user to access these files.For example, on the source server, the following command copies the files to the target machine. Replace the **<node2>** values with the names of the SQL Server instances that will host the replicas.Bashcd /var/opt/mssql/datascp dbm_certificate.* root@**<node2>**:/var/opt/mssql/data/On each target server, give permission to the mssql user to access the certificate.Bashcd /var/opt/mssql/datachown mssql:mssql dbm_certificate.*Create the certificate on secondary serversThe following Transact-SQL script creates a master key and a certificate from the backup that you created on the primary SQL Server replica. Update the script with strong passwords. The decryption password is the same password that you used to create the .pvk file in a previous step. To create the certificate, run the following script on all secondary servers:SQLCREATE MASTER KEY ENCRYPTION BY PASSWORD = '**<Master_Key_Password>**';CREATE CERTIFICATE dbm_certificateFROM FILE = '/var/opt/mssql/data/dbm_certificate.cer'WITH PRIVATE KEY (FILE = '/var/opt/mssql/data/dbm_certificate.pvk',DECRYPTION BY PASSWORD = '**<Private_Key_Password>**');Create the database mirroring endpoints on all replicasDatabase mirroring endpoints use the Transmission Control Protocol (TCP) to send and receive messages between the server instances that participate in database mirroring sessions or host availability replicas. The database mirroring endpoint listens on a unique TCP port number.The following Transact-SQL script creates a listening endpoint named Hadr_endpoint for the availability group. It starts the endpoint and gives connection permission to the certificate that you created. Before you run the script, replace the values between **< ... >**. Optionally you can include an IP address LISTENER_IP = (0.0.0.0). The listener IP address must be an IPv4 address. You can also use 0.0.0.0.Update the following Transact-SQL script for your environment on all SQL Server instances:SQLCREATE ENDPOINT [Hadr_endpoint]AS TCP (LISTENER_PORT = **<5022>**)FOR DATABASE_MIRRORING (​     ROLE = ALL ,​     AUTHENTICATION = CERTIFICATE dbm_certificate,​ ENCRYPTION = REQUIRED ALGORITHM AES​ );ALTER ENDPOINT [Hadr_endpoint] STATE = STARTED;If you use SQL Server Express Edition on one node to host a configuration-only replica, the only valid value for ROLE is WITNESS. Run the following script on SQL Server Express Edition:SQLCREATE ENDPOINT [Hadr_endpoint]AS TCP (LISTENER_PORT = **<5022>**)FOR DATABASE_MIRRORING (​     ROLE = WITNESS,​     AUTHENTICATION = CERTIFICATE dbm_certificate,​ ENCRYPTION = REQUIRED ALGORITHM AES​ );ALTER ENDPOINT [Hadr_endpoint] STATE = STARTED;The TCP port on the firewall must be open for the listener port.Create the AGThe examples in this section explain how to create the availability group using Transact-SQL. You can also use the SQL Server Management Studio Availability Group Wizard. When you create an AG with the wizard, it will return an error when you join the replicas to the AG. To fix this, grant ALTER, CONTROL, and VIEW DEFINITIONS to the pacemaker on the AG on all replicas. Once permissions are granted on the primary replica, join the nodes to the AG through the wizard, but for HA to function properly, grant permission on all replicas.Create the AG for high availability on Linux. Use the CREATE AVAILABILITY GROUP with CLUSTER_TYPE = EXTERNAL.

*   Availability group - CLUSTER_TYPE = EXTERNAL Specifies that an external cluster entity manages the AG. Pacemaker is an example of an external cluster entity. When the AG cluster type is external,
*   Set Primary and secondary replicas FAILOVER_MODE = EXTERNAL. Specifies that the replica interacts with an external cluster manager, like Pacemaker.

The following Transact-SQL scripts create an AG for high availability named ag1\. The script configures the AG replicas with SEEDING_MODE = AUTOMATIC. This setting causes SQL Server to automatically create the database on each secondary server. Update the following script for your environment. Replace the <node1>, <node2>, or <node3> values with the names of the SQL Server instances that host the replicas. Replace the <5022> with the port you set for the data mirroring endpoint. To create the AG, run the following Transact-SQL on the SQL Server instance that hosts the primary replica.

*   Create AG with three synchronous replicas

SQLCREATE AVAILABILITY GROUP [ag1]     WITH (DB_FAILOVER = ON , CLUSTER_TYPE = EXTERNAL )     FOR REPLICA ONN'<node1>' ​       ​ WITH (  ​        ENDPOINT_URL = N'tcp://<node1>:<5022>',  ​        AVAILABILITY_MODE = SYNCHRONOUS_COMMIT,  ​        FAILOVER_MODE = EXTERNAL ,  ​        SEEDING_MODE = AUTOMATIC  ​        ),N'<node2>'  ​     WITH (  ​        ENDPOINT_URL = N'tcp://<node2>:<5022>',  ​        AVAILABILITY_MODE = SYNCHRONOUS_COMMIT,  ​        FAILOVER_MODE = EXTERNAL ,  ​        SEEDING_MODE = AUTOMATIC  ​        ),  ​    N'<node3>'         WITH (  ​       ENDPOINT_URL = N'tcp://<node3>:<5022>',  ​       AVAILABILITY_MODE = SYNCHRONOUS_COMMIT,  ​       FAILOVER_MODE = EXTERNAL ,  ​       SEEDING_MODE = AUTOMATIC  ​       );ALTER AVAILABILITY GROUP [ag1] GRANT CREATE ANY DATABASE ;

*   Create AG with two synchronous replicas and a configuration replica:

SQLCREATE AVAILABILITY GROUP [ag1]    WITH (CLUSTER_TYPE = EXTERNAL )    FOR REPLICA ON     N'<node1>' WITH (ENDPOINT_URL = N'tcp://<node1>:<5022>',AVAILABILITY_MODE = SYNCHRONOUS_COMMIT,        FAILOVER_MODE = EXTERNAL ,        SEEDING_MODE = AUTOMATIC),     N'<node2>' WITH (  ENDPOINT_URL = N'tcp://<node2>:<5022>',  AVAILABILITY_MODE = SYNCHRONOUS_COMMIT,        FAILOVER_MODE = EXTERNAL ,        SEEDING_MODE = AUTOMATIC),     N'<node3>' WITH (ENDPOINT_URL = N'tcp://<node3>:<5022>',AVAILABILITY_MODE = CONFIGURATION_ONLY          );ALTER AVAILABILITY GROUP [ag1] GRANT CREATE ANY DATABASE ;

*   Create AG with two synchronous replicas

Include two replicas with synchronous availability mode. For example, the following script creates an AG called ag1. node1 and node2 host replicas in synchronous mode, with automatic seeding and automatic failover.SQLCREATE AVAILABILITY GROUP [ag1]    WITH (CLUSTER_TYPE = EXTERNAL )    FOR REPLICA ON    N'node1' WITH (       ENDPOINT_URL = N'tcp://node1:5022',       AVAILABILITY_MODE = SYNCHRONOUS_COMMIT,       FAILOVER_MODE = EXTERNAL ,       SEEDING_MODE = AUTOMATIC    ),    N'node2' WITH (         ENDPOINT_URL = N'tcp://node2:5022',         AVAILABILITY_MODE = SYNCHRONOUS_COMMIT,       FAILOVER_MODE = EXTERNAL ,       SEEDING_MODE = AUTOMATIC    );ALTER AVAILABILITY GROUP [ag1] GRANT CREATE ANY DATABASE ;You can also configure an AG with CLUSTER_TYPE=EXTERNAL using SQL Server Management Studio or PowerShell.Join secondary replicas to the AGThe pacemaker user requires ALTER, CONTROL, and VIEW DEFINITION permissions on the availability group on all replicas. To grant permissions, run the following Transact-SQL script after the availability group is created on the primary replica and each secondary replica immediately after they are added to the availability group. Before you run the script, replace <pacemakerLogin> with the name of the pacemaker user account. If you do not have a login for pacemaker, create a sql server login for pacemaker.SQLGRANT ALTER , CONTROL, VIEW DEFINITION ON AVAILABILITY GROUP ::ag1 TO <pacemakerLogin>GRANT VIEW SERVER STATE TO <pacemakerLogin>The following Transact-SQL script joins a SQL Server instance to an AG named ag1\. Update the script for your environment. On each SQL Server instance that hosts a secondary replica, run the following Transact-SQL to join the AG.SQLALTER AVAILABILITY GROUP [ag1] JOIN WITH (CLUSTER_TYPE = EXTERNAL );ALTER AVAILABILITY GROUP [ag1] GRANT CREATE ANY DATABASE ;Add a database to the availability groupEnsure that the database you add to the availability group is in full recovery mode and has a valid log backup. If this is a test database or a newly created database, take a database backup. On the primary SQL Server, run the following Transact-SQL script to create and back up a database called db1:SQLCREATE DATABASE [db1];ALTER DATABASE [db1] SET RECOVERY FULL ;BACKUP DATABASE [db1]TO DISK = N'/var/opt/mssql/data/db1.bak';On the primary SQL Server replica, run the following Transact-SQL script to add a database called db1 to an availability group called ag1:SQLALTER AVAILABILITY GROUP [ag1] ADD DATABASE [db1];Verify that the database is created on the secondary serversOn each secondary SQL Server replica, run the following query to see if the db1 database was created and is synchronized:SQLSELECT * FROM sys.databases WHERE name = 'db1';GOSELECT DB_NAME(database_id) AS 'database', synchronization_state_desc FROM sys.dm_hadr_database_replica_states;Configure RHEL Cluster for SQL Server Availability GroupThis explains how to create a three-node availability group cluster for SQL Server on Red Hat Enterprise Linux. The clustering layer is based on Red Hat Enterprise Linux (RHEL) HA add-on built on top of Pacemaker.The following sections walk through the steps to set up a Pacemaker cluster and add an availability group as resource in the cluster for high availability.RoadmapThe steps to create an availability group on Linux servers for high availability are different from the steps on a Windows Server failover cluster. The following list describes the high-level steps:

1.  Configure SQL Server on the cluster nodes.
2.  Create the availability group.
3.  Configure a cluster resource manager, like Pacemaker. These instructions are in this document.

The way to configure a cluster resource manager depends on the specific Linux distribution.

4.  Add the availability group as a resource in the cluster.

Configure high availability for RHELTo configure high availability for RHEL, enable the high availability subscription and then configure Pacemaker.Enable the high availability subscription for RHELEach node in the cluster must have an appropriate subscription for RHEL and the High Availability Add on. Follow these steps to configure the subscription and repos:

1.  Register the system.

Bashsudo subscription-manager registerProvide your user name and password.

2.  List the available pools for registration.

Bashsudo subscription-manager list --availableFrom the list of available pools, note the pool ID for the high availability subscription.

3.  Update the following script. Replace <pool id> with the pool ID for high availability from the preceding step. Run the script to attach the subscription.

Bashsudo subscription-manager attach --pool=<pool id>

4.  Enable the repository.

RHEL 7Bashsudo subscription-manager repos --enable=rhel-ha-for-rhel-7-server-rpmsRHEL 8Bashsudo subscription-manager repos --enable=rhel-8-for-x86_64-highavailability-rpmsAfter you have configured the subscription, complete the following steps to configure Pacemaker:Configure PacemakerAfter you register the subscription, complete the following steps to configure Pacemaker:

1.  On all cluster nodes, open the Pacemaker firewall ports. To open these ports with firewalld, run the following command:

Bashsudo firewall-cmd --permanent --add-service=high-availabilitysudo firewall-cmd --reloadIf the firewall doesn't have a built-in high-availability configuration, open the following ports for Pacemaker.

*   TCP: Ports 2224, 3121, 21064
*   UDP: Port 5405

2.  Install Pacemaker packages on all nodes.

Bashsudo yum install pacemaker pcs fence-agents-all resource-agents

3.  Set the password for the default user that is created when installing Pacemaker and Corosync packages. Use the same password on all nodes.

Bashsudo passwd hacluster

4.  To allow nodes to rejoin the cluster after the reboot, enable and start pcsd service and Pacemaker. Run the following command on all nodes.

Bashsudo systemctl enable pcsdsudo systemctl start pcsdsudo systemctl enable pacemaker

5.  Create the Cluster. To create the cluster, run the following command:

RHEL 7Bashsudo pcs cluster auth <node1> <node2> <node3> -u hacluster -p <password for hacluster>sudo pcs cluster setup --name <clusterName> <node1> <node2> <node3>sudo pcs cluster start --allsudo pcs cluster enable --allRHEL8For RHEL 8, you will need to authenticate the nodes separately. Manually enter in the Username and Password for hacluster when prompted.Bashsudo pcs host auth <node1> <node2> <node3>sudo pcs cluster setup <clusterName> <node1> <node2> <node3>sudo pcs cluster start --allsudo pcs cluster enable --all

6.  Install SQL Server resource agent for SQL Server. Run the following commands on all nodes.

Bashsudo yum install mssql-server-haAfter Pacemaker is configured, use pcs to interact with the cluster. Execute all commands on one node from the cluster.Configure fencing (STONITH)Pacemaker cluster vendors require STONITH to be enabled and a fencing device configured for a supported cluster setup. STONITH stands for "shoot the other node in the head." When the cluster resource manager cannot determine the state of a node or of a resource on a node, fencing brings the cluster to a known state again.Resource level fencing ensures that there is no data corruption in case of an outage by configuring a resource. For example, you can use resource level fencing to mark the disk on a node as outdated when the communication link goes down.Node level fencing ensures that a node does not run any resources. This is done by resetting the node. Pacemaker supports a great variety of fencing devices. Examples include an uninterruptible power supply or management interface cards for servers.Because the node level fencing configuration depends heavily on your environment, disable it for this tutorial (it can be configured later). The following script disables node level fencing:Bashsudo pcs property set stonith-enabled=falseDisabling STONITH is just for testing purposes. If you plan to use Pacemaker in a production environment, you should plan a STONITH implementation depending on your environment and keep it enabled.Set cluster property cluster-recheck-intervalcluster-recheck-interval indicates the polling interval at which the cluster checks for changes in the resource parameters, constraints or other cluster options. If a replica goes down, the cluster tries to restart the replica at an interval that is bound by the failure-timeout value and the cluster-recheck-interval value. For example, if failure-timeout is set to 60 seconds and cluster-recheck-interval is set to 120 seconds, the restart is tried at an interval that is greater than 60 seconds but less than 120 seconds. We recommend that you set failure-timeout to 60s and cluster-recheck-interval to a value that is greater than 60 seconds. Setting cluster-recheck-interval to a small value is not recommended.To update the property value to 2 minutes run:Bashsudo pcs property set cluster-recheck-interval=2minTo update the property value to true run:Bashsudo pcs property set start-failure-is-fatal=trueTo update the ag_cluster resource property failure-timeout to 60s run:Bashpcs resource update ag_cluster meta failure-timeout=60sCreate a SQL Server login for Pacemaker

1.  On all SQL Servers, create a Server login for Pacemaker. The following Transact-SQL creates a login:

Transact-SQLUSE [master]GOCREATE LOGIN [pacemakerLogin] with PASSWORD= N'ComplexP@$$w0rd!'ALTER SERVER ROLE [sysadmin] ADD MEMBER [pacemakerLogin]At the time of availability group creation, the pacemaker user will require ALTER, CONTROL and VIEW DEFINITION permissions on the availability group, after it's created but before any nodes are added to it.

1.  On all SQL Servers, save the credentials for the SQL Server login.

Bashecho 'pacemakerLogin' >> ~/pacemaker-passwdecho 'ComplexP@$$w0rd!' >> ~/pacemaker-passwdsudo mv ~/pacemaker-passwd /var/opt/mssql/secrets/passwdsudo chown root:root /var/opt/mssql/secrets/passwdsudo chmod 400 /var/opt/mssql/secrets/passwd # Only readable by rootCreate availability group resourceTo create the availability group resource, use pcs resource create command and set the resource properties. The following command creates a ocf:mssql:ag master/subordinate type resource for availability group with name ag1.RHEL 7Bashsudo pcs resource create ag_cluster ocf:mssql:ag ag_name=ag1 meta failure-timeout=60s master notify=trueRHEL 8With the availability of RHEL 8, the create syntax has changed. If you are using RHEL 8, the terminology master has changed to promotable. Use the following create command instead of the above command:Bashsudo pcs resource create ag_cluster ocf:mssql:ag ag_name=ag1 meta failure-timeout=60s promotable notify=trueNoteWhen you create the resource, and periodically afterwards, the Pacemaker resource agent automatically sets the value of REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT on the availability group based on the availability group's configuration. For example, if the availability group has three synchronous replicas, the agent will set REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT to 1.Create virtual IP resourceTo create the virtual IP address resource, run the following command on one node. Use an available static IP address from the network. Replace the IP address between <10.128.16.240> with a valid IP address.Bashsudo pcs resource create virtualip ocf:heartbeat:IPaddr2 ip=<10.128.16.240>There is no virtual server name equivalent in Pacemaker. To use a connection string that points to a string server name instead of an IP address, register the virtual IP resource address and desired virtual server name in DNS. For DR configurations, register the desired virtual server name and IP address with the DNS servers on both primary and DR site.Add colocation constraintAlmost every decision in a Pacemaker cluster, like choosing where a resource should run, is done by comparing scores. Scores are calculated per resource. The cluster resource manager chooses the node with the highest score for a particular resource. If a node has a negative score for a resource, the resource cannot run on that node.On a pacemaker cluster, you can manipulate the decisions of the cluster with constraints. Constraints have a score. If a constraint has a score lower than INFINITY, Pacemaker regards it as recommendation. A score of INFINITY is mandatory.To ensure that primary replica and the virtual ip resources run on the same host, define a colocation constraint with a score of INFINITY. To add the colocation constraint, run the following command on one node.RHEL 7When you create the ag_cluster resource in RHEL 7, it creates the resource as ag_cluster-master. Use the following command for RHEL 7:Bashsudo pcs constraint colocation add virtualip ag_cluster-master INFINITY with-rsc-role=MasterRHEL 8When you create the ag_cluster resource in RHEL 8, it creates the resource as ag_cluster-clone. Use the following command for RHEL 8:Bashsudo pcs constraint colocation add virtualip with master ag_cluster-clone INFINITY with-rsc-role=MasterAdd ordering constraintThe colocation constraint has an implicit ordering constraint. It moves the virtual IP resource before it moves the availability group resource. By default the sequence of events is:

1.  User issues pcs resource move to the availability group primary from node1 to node2.
2.  The virtual IP resource stops on node 1.
3.  The virtual IP resource starts on node 2.
4.  The availability group primary on node 1 is demoted to secondary.
5.  The availability group secondary on node 2 is promoted to primary.

To prevent the IP address from temporarily pointing to the node with the pre-failover secondary, add an ordering constraint.To add an ordering constraint, run the following command on one node:RHEL 7Bashsudo pcs constraint order promote ag_cluster-master then start virtualipRHEL 8Bashsudo pcs constraint order promote ag_cluster-clone then start virtualipManually fail over the availability group with pcs. Do not initiate failover with Transact-SQL. For instructions, see Failover.Operate Always On Availability Groups on LinuxUpgrade availability groupThe following sections explain how to perform a rolling upgrade with SQL Server instances on Linux with availability groups.Upgrade steps on LinuxWhen availability group replicas are on instances of SQL Server in Linux, the cluster type of the availability group is either EXTERNAL or NONE. An availability group that is managed by a cluster manager besides Windows Server Failover Cluster (WSFC) is EXTERNAL. Pacemaker with Corosync is an example of an external cluster manager. An availability group with no cluster manager has cluster type NONE The upgrade steps outlined here are specific for availability groups of cluster type EXTERNAL or NONE.The order in which you upgrade instances depends on if their role is secondary and whether or not they host synchronous or asynchronous replicas. Upgrade instances of SQL Server that host asynchronous secondary replicas first. Then upgrade instances that host synchronous secondary replicas.Before you begin, back up each database.

1.  Stop the resource on the node hosting the secondary replica targeted for upgrade.

Before running the upgrade command, stop the resource so the cluster will not monitor it and fail it unnecessarily. The following example adds a location constraint on the node that will result on the resource to be stopped. Update ag_cluster-master with the resource name and nodeName1 with the node hosting the replica targeted for upgrade.Bashpcs constraint location ag_cluster-master avoids nodeName1

2.  Upgrade SQL Server on the secondary replica.

The following example upgrades mssql-server and mssql-server-ha packages.Bashsudo yum update mssql-serversudo yum update mssql-server-ha

3.  Remove the location constraint.

Before running the upgrade command, stop the resource so the cluster will not monitor it and fail it unnecessarily. The following example adds a location constraint on the node that will result on the resource to be stopped. Update ag_cluster-master with the resource name and nodeName1 with the node hosting the replica targeted for upgrade.Bashpcs constraint remove location-ag_cluster-master-rhel1--INFINITYAs a best practice, ensure the resource is started (using pcs status command) and the secondary replica is connected and synchronized state after upgrade.

4.  After all secondary replicas are upgraded, manually fail over to one of the synchronous secondary replicas.

For availability groups with EXTERNAL cluster type, use the cluster management tools to fail over; availability groups with NONE cluster type should use Transact-SQL to fail over. The following example fails over an availability group with the cluster management tools. Replace <targetReplicaName> with the name of the synchronous secondary replica that will become primary:Bashsudo pcs resource move ag_cluster-master <targetReplicaName> --master The following steps only apply to availability groups that do not have a cluster manager.If the availability group cluster type is NONE, manually fail over. Complete the following steps in order:a. The following command sets the primary replica to secondary. Replace AG1 with the name of your availability group. Run the Transact-SQL command on the instance of SQL Server that hosts the primary replica.transact-sqlALTER AVAILABILITY GROUP [ag1] SET (ROLE = SECONDARY);b. The following command sets a synchronous secondary replica to primary. Run the following Transact-SQL command on the target instance of SQL Server - the instance that hosts the synchronous secondary replica.transact-sqlALTER AVAILABILITY GROUP [ag1] FAILOVER;

5.  After failover, upgrade SQL Server on the old primary replica by repeating the preceding procedure.

The following example upgrades mssql-server and mssql-server-ha packages.Bash# add constraint for the resource to stop on the upgraded node# replace 'nodename2' with the name of the cluster node targeted for upgradepcs constraint location ag_cluster-master avoids nodeName2sudo yum update mssql-serversudo yum update mssql-server-haBash# upgrade mssql-server and mssql-server-ha packagessudo yum update mssql-serversudo yum update mssql-server-haBash# remove the constraint; make sure the resource is started and replica is connected and synchronizedpcs constraint remove location-ag_cluster-master-rhel1--INFINITY

6.  For an availability groups with an external cluster manager - where cluster type is EXTERNAL, clean up the location constraint that was caused by the manual failover.

Bashsudo pcs constraint remove cli-prefer-ag_cluster-master 

7.  Resume data movement for the newly upgraded secondary replica - the former primary replica. This step is required when a higher version instance of SQL Server is transferring log blocks to a lower version instance in an availability group. Run the following command on the new secondary replica (the previous primary replica).

transact-sqlALTER DATABASE database_name SET HADR RESUME;After upgrading all servers, you can fail back. Fail over back to the original primary - if necessary.Drop an availability groupTo delete an availability group, run DROP AVAILABILITY GROUP. If the cluster type is EXTERNAL or NONE run the command on every instance of SQL Server that hosts a replica. For example, to drop an availability group named group_name run the following command:transact-sqlDROP AVAILABILITY GROUP group_nameConfigure multiple-subnet Always On Availability Groups and failover cluster instancesWhen an Always On Availability Group (AG) or failover cluster instance (FCI) spans more than one site, each site usually has its own networking. This often means that each site has its own IP addressing. For example, Site A's addresses start with 192.168.1.x and Site B's addresses start with 192.168.2.x, where x is the part of the IP address that is unique to the server. Without some sort of routing in place at the networking layer, these servers will not be able to communicate with each other. There are two ways to handle this scenario: set up a network that bridges the two different subnets, known as a VLAN, or configure routing between the subnets.VLAN-based solutionPrerequisite: For a VLAN-based solution, each server participating in an AG or FCI needs two network cards (NICs) for proper availability (a dual port NIC would be a single point of failure on a physical server), so that it can be assigned IP addresses on its native subnet as well as one on the VLAN. This is in addition to any other network needs, such as iSCSI, which also needs its own network.The IP address creation for the AG or FCI is done on the VLAN. In the following example, the VLAN has a subnet of 192.168.3.x, so the IP address created for the AG or FCI is 192.168.3.104\. Nothing additional needs to be configured, since there is a single IP address assigned to the AG or FCI.![Configure multiple subnets 01](Image00035.jpg)Configuration with PacemakerIn the Windows world, a Windows Server Failover Cluster (WSFC) natively supports multiple subnets and handles multiple IP addresses via an OR dependency on the IP address. On Linux, there is no OR dependency, but there is a way to achieve a proper multi-subnet natively with Pacemaker, as shown by the following. You cannot do this by simply using the normal Pacemaker command line to modify a resource. You need to modify the cluster information base (CIB). The CIB is an XML file with the Pacemaker configuration.![Configure multiple subnets 02](Image00036.jpg)Update the CIB

1.  Export the CIB.

Red Hat Enterprise Linux (RHEL) and UbuntuBashsudo pcs cluster cib <filename>SUSE Linux Enterprise Server (SLES)Bashsudo cibadmin -Q > <filename>Where filename is the name you want to call the CIB.

2.  Edit the file that was generated. Look for the <resources> section. You will see the various resources that were created for the AG or FCI. Find the one associated with the IP address. Add a <instance attributes> section with the information for the second IP address either above or below the existing one, but before <operations>. It is similar to the following syntax:

XML<instance attributes id="<NameForAttribute>">    <nvpair id="<NameForIP>" name="ip" value="<IPAddress>"/></instance attributes>where NameForAttribute is the unique name for this attribute, NameForIP is the name associated with the IP address, IPAddress is the IP address for the second subnet.The following shows an example.XML<instance attributes id="virtualip-instance_attributes">    <nvpair id="virtualip-instance_attributes-ip" name="ip" value="192.168.1.102"/></instance attributes>By default, there is only one in the CIB XML file exported. Let's say there are two subnets, you need to have two entries. Here is an example of entries for two subnetsXML<instance attributes id="virtualip-instance_attributes1">    <rule id="Subnet1-IP" score="INFINITY" boolean-op="or">        <expression id="Subnet1-Node1" attribute="#uname" operation="eq" value="Node1" />        <expression id="Subnet1-Node2" attribute="#uname" operation="eq" value="Node2" />    </rule>    <nvpair id="IP-In-Subnet1" name="ip" value="192.168.1.102"/></instance attributes><instance attributes id="virtualip-instance_attributes2">    <rule id="Subnet2-IP" score="INFINITY">        <expression id="Subnet2-Node1" attribute="#uname" operation="eq" value="Node3" />    </rule>    <nvpair id="IP-In-Subnet2" name="ip" value="192.168.2.102"/></instance attributes>The 'boolean-op="or"' is used when the subnet has more than one server.

3.  Import the modified CIB and reconfigure Pacemaker.

RHEL/UbuntuBashsudo pcs cluster cib-push <filename>SLESBashsudo cibadmin -R -x <filename>where filename is the name of the CIB file with the modified IP address information.Check and verify failover

1.  After the CIB is successfully applied with the updated configuration, ping the DNS name associated with the IP address resource in Pacemaker. It should reflect the IP address associated with the subnet currently hosting the AG or FCI.
2.  Fail the AG or FCI to the other subnet.
3.  After the AG or FCI is fully online, ping the DNS name associated with the IP address. It should reflect the IP address in the second subnet.
4.  If desired, fail the AG or FCI back to the original subnet.

Here is a CSS post showing how to configure the CIB for three subnets, please review for detail: Configure multiple-subnet AlwaysOn Availability Group by modifying CIB.Performance best practices and configuration guidelines for SQL Server on LinuxFind the best practices and recommendations to maximize performance for database applications that connect to SQL Server on Linux. These recommendations are specific to running on the Linux platform. All normal SQL Server recommendations, such as index design, still apply.The following guidelines contain recommendations for configuring both SQL Server and the Linux operating system.SQL Server configurationIt is recommended to perform the following configuration tasks after you install SQL Server on Linux to achieve best performance for your application.Best practices

*   Use PROCESS AFFINITY for Node and/or CPUs

It is recommended to use ALTER SERVER CONFIGURATION to set PROCESS AFFINITY for all the NUMANODEs and/or CPUs you are using for SQL Server (which is typically for all NODEs and CPUs) on a Linux Operating System. Processor affinity helps maintain efficient Linux and SQL Scheduling behavior. Using the NUMANODE option is the simplest method. Note, you should use PROCESS AFFINITY even if you have only a single NUMA Node on your computer.

*   Configure multiple tempdb data files

Because a SQL Server on Linux installation does not offer an option to configure multiple tempdb files, we recommend that you consider creating multiple tempdb data files after installation.Advanced ConfigurationThe following recommendations are optional configuration settings that you may choose to perform after installation of SQL Server on Linux. These choices are based on the requirements of your workload and configuration of your Linux Operating System.

*   Set a memory limit with mssql-conf

In order to ensure there is enough free physical memory for the Linux Operating System, the SQL Server process uses only 80% of the physical RAM by default. For some systems which large amount of physical RAM, 20% might be a significant number. For example, on a system with 1 TB of RAM, the default setting would leave around 200 GB of RAM unused. In this situation, you might want to configure the memory limit to a higher value. See the documentation on the mssql-conf tool and the memory.memorylimitmb setting that controls the memory visible to SQL Server (in units of MB).When changing this setting, be careful not to set this value too high. If you do not leave enough memory, you could experience problems with the Linux Operating System and other Linux applications.Linux OS ConfigurationConsider using the following Linux Operating System configuration settings to experience the best performance for a SQL Server Installation.Kernel settings for high performanceThese are the recommended Linux Operating System settings related to high performance and throughput for a SQL Server installation. See your Linux Operating System documentation for the process to configure these settings.The following table provides recommendations for CPU settings:

| KERNEL SETTINGS FOR HIGH PERFORMANCE |
| --- |
| Setting | Value | More information |
| --- | --- | --- |
| CPU frequency governor | performance | See the cpupower command |
| ENERGY_PERF_BIAS | performance | See the x86_energy_perf_policy command |
| min_perf_pct | 100 | See your documentation on intel p-state |
| C-States | C1 only | See your Linux or system documentation on how to ensure C-States is set to C1 only |
|  |  |  |

The following table provides recommendations for disk settings:

| Setting | Value | More information |
| --- | --- | --- |
| disk readahead | 4096 | See the blockdev command |
| sysctl settings | kernel.sched_min_granularity_ns = 10000000 kernel.sched_wakeup_granularity_ns = 15000000
vm.dirty_ratio = 40
vm.dirty_background_ratio = 10
vm.swappiness = 10 | See the sysctl command |

Kernel setting auto numa balancing for multi-node NUMA systemsIf you install SQL Server on a multi-node NUMA systems, the following kernel.numa_balancing kernel setting is enabled by default. To allow SQL Server to operate at maximum efficiency on a NUMA system, disable auto numa balancing on a multi-node NUMA system:Bashsysctl -w kernel.numa_balancing=0Kernel settings for Virtual Address SpaceThe default setting of vm.max_map_count (which is 65536) may not be high enough for a SQL Server installation. For this reason, change the vm.max_map_count value to at least 262144 for a SQL Server deployment. The max value for vm.max_map_count is 2147483647.Bashsysctl -w vm.max_map_count=1600000Proposed Linux settings using a tuned mssql profileBash## A tuned configuration for SQL Server on Linux#[main]summary=Optimize for Microsoft SQL Serverinclude=throughput-performance[cpu]force_latency=5[sysctl]vm.swappiness = 1vm.dirty_background_ratio = 3vm.dirty_ratio = 80vm.dirty_expire_centisecs = 500vm.dirty_writeback_centisecs = 100vm.transparent_hugepages=always# For multi-instance SQL deployments, use# vm.transparent_hugepages=madvisevm.max_map_count=1600000net.core.rmem_default = 262144net.core.rmem_max = 4194304net.core.wmem_default = 262144net.core.wmem_max = 1048576kernel.numa_balancing=0kernel.sched_latency_ns = 60000000kernel.sched_migration_cost_ns = 500000kernel.sched_min_granularity_ns = 15000000kernel.sched_wakeup_granularity_ns = 2000000To enable this tuned profile, save these definitions in a tuned.conf file under a /usr/lib/tuned/mssql folder and enable the profile usingBashchmod +x /usr/lib/tuned/mssql/tuned.conftuned-adm profile mssqlVerify its enabling withBashtuned-adm activeorBashtuned-adm listDisable last accessed date/time on file systems for SQL Server data and log filesUse the noatime attribute with any file system that is used to store SQL Server data and log files. Refer to your Linux documentation on how to set this attribute.Leave Transparent Huge Pages (THP) enabledMost Linux installations should have this option on by default. We recommend for the most consistent performance experience to leave this configuration option enabled. However, in case of high memory paging activity in SQL Server deployments with multiple instances for example or SQL Server execution with other memory demanding applications on the server, we suggest testing your applications performance after executing the following commandBashecho madvise > /sys/kernel/mm/transparent_hugepage/enabledor modifying the mssql tuned profile with the lineBashvm.transparent_hugepages=madviseand make the mssql profile active after the modificationBashtuned-adm offtuned-adm profile mssqlswapfileEnsure you have a properly configured swapfile to avoid any out of memory issues. Consult your Linux documentation for how to create and properly size a swapfile.Virtual Machines and Dynamic MemoryIf you are running SQL Server on Linux in a virtual machine, ensure you select options to fix the amount of memory reserved for the virtual machine. Do not use features like Hyper-V Dynamic Memory.Performance features of SQL Server on LinuxIf you are a Linux user who is new to SQL Server, the following tasks walk you through some of the performance features. These are not unique or specific to Linux, but it helps to give you an idea of areas to investigate further. In each example, a link is provided to the depth documentation for that area.Create a Columnstore IndexA columnstore index is a technology for storing and querying large stores of data in a columnar data format, called a columnstore.

1.  Add a Columnstore index to the SalesOrderDetail table by executing the following Transact-SQL commands:

SQLCREATE NONCLUSTERED COLUMNSTORE INDEX [IX_SalesOrderDetail_ColumnStore]   ON Sales.SalesOrderDetail   (UnitPrice, OrderQty, ProductID)GO

2.  Execute the following query that uses the Columnstore Index to scan the table:

SQLSELECT ProductID, SUM (UnitPrice) SumUnitPrice, AVG (UnitPrice) AvgUnitPrice,   SUM (OrderQty) SumOrderQty, AVG (OrderQty) AvgOrderQtyFROM Sales.SalesOrderDetail   GROUP BY ProductID   ORDER BY ProductID

3.  Verify that the Columnstore Index was used by looking up the object_id for the Columnstore index and confirming that it appears in the usage stats for the SalesOrderDetail table:

SQLSELECT * FROM sys.indexes WHERE name = 'IX_SalesOrderDetail_ColumnStore'GOSELECT *FROM sys.dm_db_index_usage_stats   WHERE database_id = DB_ID('AdventureWorks')   AND object_id = OBJECT_ID('AdventureWorks.Sales.SalesOrderDetail');Use In-Memory OLTPSQL Server provides In-Memory OLTP features that can greatly improve the performance of application systems. This section of the Evaluation Guide will walk you through the steps to create a memory-optimized table stored in memory and a natively compiled stored procedure that can access the table without needing to be compiled or interpreted.Configure Database for In-Memory OLTP

1.  It's recommended to set the database to a compatibility level of at least 130 to use In-Memory OLTP. Use the following query to check the current compatibility level of AdventureWorks:

SQLUSE AdventureWorksGOSELECT d.compatibility_levelFROM sys.databases as d  WHERE d.name = Db_Name();GOIf necessary, update the level to 130:SQLALTER DATABASE CURRENTSET COMPATIBILITY_LEVEL = 130;GO

2.  When a transaction involves both a disk-based table and a memory-optimized table, it's essential that the memory-optimized portion of the transaction operate at the transaction isolation level named SNAPSHOT. To reliably enforce this level for memory-optimized tables in a cross-container transaction, execute the following:

SQLALTER DATABASE CURRENT SET MEMORY_OPTIMIZED_ELEVATE_TO_SNAPSHOT=ONGO

3.  Before you can create a memory-optimized table you must first create a Memory Optimized FILEGROUP and a container for data files:

SQLALTER DATABASE AdventureWorks ADD FILEGROUP AdventureWorks_mod CONTAINS memory_optimized_dataGO   ALTER DATABASE AdventureWorks ADD FILE (NAME ='AdventureWorks_mod', FILENAME='/var/opt/mssql/data/AdventureWorks_mod') TO FILEGROUP AdventureWorks_modGOCreate a Memory-Optimized TableThe primary store for memory-optimized tables is main memory and so unlike disk-based tables, data does not need to be read in from disk into memory buffers. To create a memory-optimized table, use the MEMORY_OPTIMIZED = ON clause.

1.  Execute the following query to create the memory-optimized table dbo.ShoppingCart. As a default, the data will be persisted on disk for durability purposes (Note that DURABILITY can also be set to persist the schema only).

SQLCREATE TABLE dbo.ShoppingCart (ShoppingCartId INT IDENTITY (1,1) PRIMARY KEY NONCLUSTERED,UserId INT NOT NULL INDEX ix_UserId NONCLUSTERED HASH WITH (BUCKET_COUNT=1000000),CreatedDate DATETIME2 NOT NULL,TotalPrice MONEY) WITH (MEMORY_OPTIMIZED=ON )GO

2.  Insert some records into the table:

SQLINSERT dbo.ShoppingCart VALUES (8798, SYSDATETIME(), NULL)INSERT dbo.ShoppingCart VALUES (23, SYSDATETIME(), 45.4)INSERT dbo.ShoppingCart VALUES (80, SYSDATETIME(), NULL)INSERT dbo.ShoppingCart VALUES (342, SYSDATETIME(), 65.4)Natively compiled Stored ProcedureSQL Server supports natively compiled stored procedures that access memory-optimized tables. The T-SQL statements are compiled to machine code and stored as native DLLs, enabling faster data access and more efficient query execution than traditional T-SQL. Stored procedures that are marked with NATIVE_COMPILATION are natively compiled.

1.  Execute the following script to create a natively compiled stored procedure that inserts a large number of records into the ShoppingCart table:

SQLCREATE PROCEDURE dbo.usp_InsertSampleCarts @InsertCount int WITH NATIVE_COMPILATION, SCHEMABINDING ASBEGIN ATOMICWITH (TRANSACTION ISOLATION LEVEL = SNAPSHOT , LANGUAGE = N'us_english')DECLARE @i int = 0WHILE @i < @InsertCount BEGIN  INSERT INTO dbo.ShoppingCart VALUES (1, SYSDATETIME() , NULL)  SET @i += 1 ENDEND

2.  Insert 1,000,000 rows:

SQLEXEC usp_InsertSampleCarts 1000000

3.  Verify the rows have been inserted:

SQLSELECT COUNT (*) FROM dbo.ShoppingCartLearn More About In-Memory OLTPUse Query StoreQuery Store collects detailed performance information about queries, execution plans, and runtime statistics.Query Store is not active by default and can be enabled with ALTER DATABASE:SQLALTER DATABASE AdventureWorks SET QUERY_STORE = ON ;Run the following query to return information about queries and plans in the query store:SQLSELECT Txt.query_text_id, Txt.query_sql_text, Pl.plan_id, Qry.*FROM sys.query_store_plan AS PlJOIN sys.query_store_query AS QryON Pl.query_id = Qry.query_idJOIN sys.query_store_query_text AS TxtON Qry.query_text_id = Txt.query_text_id ;Query Dynamic Management ViewsDynamic management views return server state information that can be used to monitor the health of a server instance, diagnose problems, and tune performance.To query the dm_os_wait stats dynamic management view:SQLSELECT wait_type, wait_time_msSQL Server Replication on LinuxSQL Server 2017 (14.x) (CU18) and later support SQL Server Replication for instances of SQL Server on Linux.Configure replication on Linux with SQL Server Management Studio (SSMS) replication stored procedures.An instance of SQL Server can participate in any replication role:

*   Publisher
*   Distributor
*   Subscriber

A replication schema can mix and match operating system platforms. For example, a replication schema may include an instance of SQL Server on Linux for publisher and distributor, and the subscribers include instances of SQL Server on Windows as well as Linux.SQL Server instances on Linux can participate in any type of replication.

*   Transactional
*   Snapshot

For detailed information about replication, see SQL Server replication documentation.Supported featuresThe following replication features are supported:

*   Snapshot replication
*   Transactional replication
*   Replication with non-default ports
*   Replication with AD authentication
*   Replication configurations across Windows and Linux
*   Immediate updates for transactional replication

LimitationsThe following features are not supported:

*   Merge replication
*   Peer-to-Peer replication
*   Oracle publishing

Configure SQL Server Replication on LinuxSQL Server 2019 (15.x) introduces SQL Server Replication for instances of SQL Server on Linux.Configure replication on Linux with either SQL Server Management Studio (SSMS) or Transact-SQL stored procedures.

*   To use SSMS, follow the instructions in this article.

Use SSMS on a Windows operating system to connect to instances of SQL Server.PrerequisitesBefore configuring publishers, distributors, and subscribers, you need to complete a couple configuration steps for the SQL Server instance.

1.  Enable SQL Server Agent to use replication agents. On all Linux servers, run the following commands in the terminal.

Bashsudo /opt/mssql/bin/mssql-conf set sqlagent.enabled truesudo systemctl restart mssql-server

2.  Configure the SQL Server instance for replication. To configure the SQL Server instance for replication, run sys.sp_MSrepl_createdatatypemappings on all instances participating in replication.

SQLUSE msdbGOexec sys.sp_MSrepl_createdatatypemappings;GO

3.  Create a snapshot folder. The SQL Server agents require a snapshot folder to read/write to. Create the snapshot folder on the distributor.

To create the snapshot folder, and grant access to mssql user, run the following command:Bashsudo mkdir /var/opt/mssql/data/ReplData/sudo chown mssql /var/opt/mssql/data/ReplData/sudo chgrp mssql /var/opt/mssql/data/ReplData/Configure and monitor replication with SQL Server Management Studio (SSMS)Configure the distributorTo configure the distributor:

1.  On SSMS connect to your instance of SQL Server in Object Explorer.
2.  Right-click Replication, and click Configure Distribution....
3.  Follow the instructions on the Configure Distribution Wizard.

Create publication and articlesTo create a publication and articles:

1.  In Object Explorer, click Replication > Local Publications> New Publication....
2.  Follow the instruction on the New Publication Wizard to configure the type of replication, and the articles that belong to the publication.

Configure the subscriptionTo configure the subscription in Object Explorer, click Replication > Local Subscriptions> New subscriptions....Monitor replication jobsUse Replication Monitor to monitor replication jobs.In Object Explorer, right-click Replication, and click Launch Replication Monitor.Configure replication snapshot folder with sharesThe snapshot folder is a directory that you have designated as a share; agents that read from and write to this folder must have enough permissions to access it.![replication diagram](Image00037.jpg)Replication Snapshot Folder Share ExplainedBefore the examples, let's walk through how SQL Server uses samba shares in replication. Below is a basic example of how this works.

1.  Samba shares are configured that files written to /local/path1 by the replication agents on publisher can be seen by the subscriber
2.  SQL Server is configured to use share paths when setting up the publisher on the distribution server such that all instances would look at the //share/path
3.  SQL Server finds the local path from the //share/path to know where to look for the files
4.  SQL Server reads/writes to local paths backed by a samba share

Configure a samba share for the snapshot folderReplication agents will need a shared directory between replication hosts to access snapshot folders on other machines. For example, in transactional pull replication, the distribution agent resides on the subscriber, which requires access to the distributor to get articles. In this section, we'll go through an example of how to configure a samba share on two replication hosts.StepsAs an example, we will configure a snapshot folder on Host 1 (the distributor) to be shared with Host 2 (the subscriber) using Samba.Install and start Samba on both machinesOn Ubuntu:Bashsudo apt-get -y install sambasudo service smbd restartOn RHEL:Bashsudo yum install sambasudo service smb startsudo service smb statusOn Host 1 (Distributor) Set-up the Samba share

1.  Set-up user and password for samba:

Bashsudo smbpasswd -a mssql

2.  Edit the /etc/samba/smb.conf to include the following entry and fill in the share_name and path fields

Bash<[share_name]>path = </local/path/on/host/1>writable = yescreate mask = 770directory maskvalid users = mssqlExampleBash[mssql_data]   <- Name of the shared directorypath = /var/opt/mssql/repldata <- location of directory we wish to sharewritable = yes  <- determines if the share is writable from other hostscreate mask = 770  <- Linux permissions for files createddirectory mask = 770 <- Linux permissions for directories createdvalid users = mssql   <- list of users who can login to this shareOn Host 2 (Subscriber) Mount the Samba ShareEdit the command with the correct paths and run the following command on machine2:Bashsudo mount //<name_of_host_1>/<share_name> </local/path/on/host/2> -o user=mssql,uid=mssql,gid=mssqlExampleBashmount //host1/mssql_data /var/opt/mssql/repldata_shared -o user=mssql,uid=mssql,gid=mssqluser=mssql <- sets the login name for sambauid=mssql   <- makes the mssql user as the owner of the mounted directorygid=mssql   <- sets the mssql group as the owner of the mounted directoryOn Both Hosts Configure SQL Server on Linux Instances to use Snapshot ShareAdd the following section to mssql.conf on both machines. Use wherever the samba share for the //share/path. In this example, it would be //host1/mssql_dataBash[uncmapping]//share/path = /local/path/on/hosts/ExampleOn host1:Bash[uncmapping]//host1/mssql_data = /local/path/on/hosts/1On host2:Bash[uncmapping]//host1/mssql_data = /local/path/on/hosts/2Configuring Publisher with Shared paths

*   When setting up replication, use the shares path (example //host1/mssql_data
*   Map //host1/mssql_data to a local directory and the mapping added to mssql.conf.

Configure replication with non-default ports (SQL Server Linux)You can configure replication with SQL Server on Linux instances listening on any port configured with the network.tcpport mssql-conf setting. The port needs to be appended to the server name during configuration if the following conditions are true:

1.  Replication set-up involves an instance of SQL Server on Linux
2.  Any instance (Windows or Linux) is listening on a non-default port.

The server name of an instance can be found by running @@servername on the instance. Do not use the IP address instead of the server name. Using the IP address for the publisher, distributor, or subscriber may result in an error.Examples'Server1' listens on port 1500 on Linux. To configure 'Server1' for distribution, run sp_adddistributor with @distributor. For example:SQLexec sp_adddistributor @distributor = 'Server1,1500''Server1' listens on port 1500 on Linux. To configure a publisher for the distributor, run sp_adddistpublisher with @publisher. For example:SQLexec sp_adddistpublisher @publisher = 'Server1,1500' ,  , 'Server2' listens on port 6549 on Linux. To configure 'Server2' as a subscriber, run sp_addsubscription with @subscriber. For example:SQLexec sp_addsubscription @subscriber = 'Server2,6549' ,  , 'Server3' listens on port 6549 on Windows with server name of Server3 and instance name of MSSQL2017\. To configure 'Server3' as a subscriber, run the sp_addsubscription with @subscriber. For example:SQLexec sp_addsubscription @subscriber = 'Server3/MSSQL2017,6549',  , Troubleshoot SQL Server on LinuxThis defines how to troubleshoot Microsoft SQL Server running on Linux or in a Docker container. When troubleshooting SQL Server on Linux, remember to review the supported features and known limitations.Troubleshoot connection failuresIf you are having difficulty connecting to your Linux SQL Server, there are a few things to check.

*   If you are unable to connect locally using localhost, try using the IP address 127.0.0.1 instead. It is possible that localhost is not properly mapped to this address.
*   Verify that the server name or IP address is reachable from your client machine.

Bashsudo ifconfig eth0 | grep 'inet addr'For Red Hat, you can use the ip addr as in the following example:Bashsudo ip addr show eth0 | grep "inet"One exception to this technique relates to Azure VMs. For Azure VMs, find the public IP for the VM in the Azure portal .

*   If applicable, check that you have opened the SQL Server port (default 1433) on the firewall.
*   For Azure VMs, check that you have a network security group rule for the default SQL Server port.
*   Verify that the user name and password do not contain any typos or extra spaces or incorrect casing.
*   Try to explicitly set the protocol and port number with the server name like the following example: tcp:servername,1433.
*   Network connectivity issues can also cause connection errors and timeouts. After verifying your connection information and network connectivity, try the connection again.

Manage the SQL Server serviceThe following sections show how to start, stop, restart, and check the status of the SQL Server service.Manage the mssql-server service in Red Hat Enterprise Linux (RHEL) and UbuntuCheck the status of the SQL Server service using this command:Bashsudo systemctl status mssql-serverYou can stop, start, or restart the SQL Server service as needed using the following commands:Bashsudo systemctl stop mssql-serversudo systemctl start mssql-serversudo systemctl restart mssql-serverManage the execution of the mssql Docker containerYou can get the status and container ID of the latest created SQL Server Docker container by running the following command (The ID is under the CONTAINER ID column):Bashsudo docker ps -lYou can stop or restart the SQL Server service as needed using the following commands:Bashsudo docker stop <container ID>sudo docker restart <container ID>Access the log filesThe SQL Server engine logs to the /var/opt/mssql/log/errorlog file in both the Linux and Docker installations. You need to be in 'superuser' mode to browse this directory.The installer logs here: /var/opt/mssql/setup-< time stamp representing time of install> You can browse the errorlog files with any UTF-16 compatible tool like 'vim' or 'cat' like this:Bashsudo cat errorlogIf you prefer, you can also convert the files to UTF-8 to read them with 'more' or 'less' with the following command:Bashsudo iconv -f UTF-16LE -t UTF-8 <errorlog> -o <output errorlog file>Crash dumpsLook for dumps in the log directory in Linux. Check under the /var/opt/mssql/log directory for Linux Core dumps (.tar.gz2 extension) or SQL minidumps (.mdmp extension)For Core dumpsBashsudo ls /var/opt/mssql/log | grep .tar.gz2For SQL dumpsBashsudo ls /var/opt/mssql/log | grep .mdmpStart SQL Server in Minimal Configuration or in Single User ModeStart SQL Server in Minimal Configuration ModeThis is useful if the setting of a configuration value (for example, over-committing memory) has prevented the server from starting.Bashsudo -u mssql /opt/mssql/bin/sqlservr -fStart SQL Server in Single User ModeUnder certain circumstances, you may have to start an instance of SQL Server in single-user mode by using the startup option -m. For example, you may want to change server configuration options or recover a damaged master database or other system database. For example, you may want to change server configuration options or recover a damaged master database or other system databaseStart SQL Server in Single User ModeBashsudo -u mssql /opt/mssql/bin/sqlservr -mStart SQL Server in Single User Mode with SQLCMDBashsudo -u mssql /opt/mssql/bin/sqlservr -m SQLCMDIf you have accidentally started SQL Server with another user, you must change ownership of SQL Server database files back to the 'mssql' user prior to starting SQL Server with systemd. For example, to change ownership of all database files under /var/opt/mssql to the 'mssql' user, run the following commandBashchown -R mssql:mssql /var/opt/mssql/Rebuild system databasesAs a last resort, you can choose to rebuild the master and model databases back to default versions.

1.  Stop SQL Server.

Bashsudo systemctl stop mssql-server

2.  Run sqlservr with the force-setup parameter.

Bashsudo -u mssql /opt/mssql/bin/sqlservr --force-setup WarningSee the previous warning! Also, you must run this as the mssql user as shown here.

3.  After you see the message "Recovery is complete", press CTRL+C. This will shut down SQL Server
4.  Reconfigure the SA password.

Bashsudo /opt/mssql/bin/mssql-conf set-sa-password

5.  Start SQL Server and reconfigure the server. This includes restoring or re-attaching any user databases.

Bashsudo systemctl start mssql-serverImprove performanceThere are many factors that affect performance, including database design, hardware, and workload demands. Then explore some of the available tools for troubleshooting performance problems.Common issues

1.  You cannot connect to your remote SQL Server instance.
2.  ERROR: Hostname must be 15 characters or less.

This is a known-issue that happens whenever the name of the machine that is trying to install the SQL Server Debian package is longer than 15 characters. There are currently no workarounds other than changing the name of the machine. One way to achieve this is by editing the hostname file and rebooting the machine.

3.  Resetting the system administration (SA) password.

If you have forgotten the system administrator (SA) password or need to reset it for some other reason, follow these steps.Bashsudo systemctl stop mssql-serversudo /opt/mssql/bin/mssql-conf setup

4.  Using special characters in password.

If you use some characters in the SQL Server login password, you might need to escape them with a backslash when you use them in a Linux command in the terminal. For example, you must escape the dollar sign ($) anytime you use it in a terminal command/shell script:Does not work:Bashsudo sqlcmd -S myserver -U sa -P Test$$Works:Bashsqlcmd -S myserver -U sa -P Test\$\$Configure a SQL Server Availability Group for read-scale on LinuxYou can configure a SQL Server Always On Availability Group (AG) for read-scale workloads on Linux. There are two types of architectures for AGs. A architecture for high availability uses a cluster manager to provide improved business continuity. This architecture also can include read-scale replicas. The other architecture supports only read-scale workloads. This article explains how to create an AG without a cluster manager for read-scale workloads. This architecture provides read-scale only. It doesn't provide high availability.Before you create the availability group, you need to:

*   Set your environment so that all the servers that will host availability replicas can communicate.
*   Install SQL Server.

On Linux, you must create an availability group before you add it as a cluster resource to be managed by the cluster. This document provides an example that creates the availability group. For distribution-specific instructions to create the cluster and add the availability group as a cluster resource, see the links under "Next steps."

1.  Update the computer name for each host.

Each SQL Server name must be:

*   15 characters or less.
*   Unique within the network.

To set the computer name, edit /etc/hostname. The following script lets you edit /etc/hostname with vi:Bashsudo vi /etc/hostname

2.  Configure the hosts file.

The hosts file on every server contains the IP addresses and names of all servers that will participate in the availability group.The following command returns the IP address of the current server:Bashsudo ip addr showUpdate /etc/hosts. The following script lets you edit /etc/hosts with vi:Bashsudo vi /etc/hostsThe following example shows /etc/hosts on node1 with additions for node1, node2, and node3\. In this document, node1 refers to the server that hosts the primary replica. And node2 and node3 refer to servers that host the secondary replicas.127.0.0.1   localhost localhost4 localhost4.localdomain4::1       localhost localhost6 localhost6.localdomain610.128.18.12 node110.128.16.77 node210.128.15.33 node3Enable AlwaysOn availability groups and restart mssql-serverEnable AlwaysOn availability groups on each node that hosts a SQL Server instance. Then restart mssql-server. Run the following script:Bashsudo /opt/mssql/bin/mssql-conf set hadr.hadrenabled  1sudo systemctl restart mssql-serverEnable an AlwaysOn_health event sessionYou can optionally enable AlwaysOn availability groups extended events to help with root-cause diagnosis when you troubleshoot an availability group. Run the following command on each instance of SQL Server:SQLALTER EVENT SESSION   AlwaysOn_health ON SERVER WITH (STARTUP_STATE=ON );GOFor more information about this XE session, see Always On extended events.Create a certificateThe SQL Server service on Linux uses certificates to authenticate communication between the mirroring endpoints.The following Transact-SQL script creates a master key and a certificate. It then backs up the certificate and secures the file with a private key. Update the script with strong passwords. Connect to the primary SQL Server instance. To create the certificate, run the following Transact-SQL script:SQLCREATE MASTER KEY ENCRYPTION BY PASSWORD = '**<Master_Key_Password>**';CREATE CERTIFICATE dbm_certificate WITH SUBJECT = 'dbm';BACKUP CERTIFICATE dbm_certificateTO FILE = '/var/opt/mssql/data/dbm_certificate.cer'WITH PRIVATE KEY (FILE = '/var/opt/mssql/data/dbm_certificate.pvk',ENCRYPTION BY PASSWORD = '**<Private_Key_Password>**');At this point, your primary SQL Server replica has a certificate at /var/opt/mssql/data/dbm_certificate.cer and a private key at var/opt/mssql/data/dbm_certificate.pvk. Copy these two files to the same location on all servers that will host availability replicas. Use the mssql user, or give permission to the mssql user to access these files.For example, on the source server, the following command copies the files to the target machine. Replace the **<node2>** values with the names of the SQL Server instances that will host the replicas.Bashcd /var/opt/mssql/datascp dbm_certificate.* root@**<node2>**:/var/opt/mssql/data/On each target server, give permission to the mssql user to access the certificate.Bashcd /var/opt/mssql/datachown mssql:mssql dbm_certificate.*Create the certificate on secondary serversThe following Transact-SQL script creates a master key and a certificate from the backup that you created on the primary SQL Server replica. Update the script with strong passwords. The decryption password is the same password that you used to create the .pvk file in a previous step. To create the certificate, run the following script on all secondary servers:SQLCREATE MASTER KEY ENCRYPTION BY PASSWORD = '**<Master_Key_Password>**';CREATE CERTIFICATE dbm_certificateFROM FILE = '/var/opt/mssql/data/dbm_certificate.cer'WITH PRIVATE KEY (FILE = '/var/opt/mssql/data/dbm_certificate.pvk',DECRYPTION BY PASSWORD = '**<Private_Key_Password>**');Create the database mirroring endpoints on all replicasDatabase mirroring endpoints use the Transmission Control Protocol (TCP) to send and receive messages between the server instances that participate in database mirroring sessions or host availability replicas. The database mirroring endpoint listens on a unique TCP port number.The following Transact-SQL script creates a listening endpoint named Hadr_endpoint for the availability group. It starts the endpoint and gives connection permission to the certificate that you created. Before you run the script, replace the values between **< ... >**. Optionally you can include an IP address LISTENER_IP = (0.0.0.0). The listener IP address must be an IPv4 address. You can also use 0.0.0.0.Update the following Transact-SQL script for your environment on all SQL Server instances:SQLCREATE ENDPOINT [Hadr_endpoint]AS TCP (LISTENER_PORT = **<5022>**)FOR DATABASE_MIRRORING (​     ROLE = ALL ,​     AUTHENTICATION = CERTIFICATE dbm_certificate,​ ENCRYPTION = REQUIRED ALGORITHM AES​ );ALTER ENDPOINT [Hadr_endpoint] STATE = STARTED;SQLCREATE ENDPOINT [Hadr_endpoint]AS TCP (LISTENER_PORT = **<5022>**)FOR DATABASE_MIRRORING (​     ROLE = WITNESS,​     AUTHENTICATION = CERTIFICATE dbm_certificate,​ ENCRYPTION = REQUIRED ALGORITHM AES​ );ALTER ENDPOINT [Hadr_endpoint] STATE = STARTED;The TCP port on the firewall must be open for the listener port.Create the AGCreate the AG. Set CLUSTER_TYPE = NONE. In addition, set each replica with FAILOVER_MODE = MANUAL. Client applications running analytics or reporting workloads can directly connect to the secondary databases. You also can create a read-only routing list. Connections to the primary replica forward read connection requests to each of the secondary replicas from the routing list in a round-robin fashion.The following Transact-SQL script creates an AG named ag1\. The script configures the AG replicas with SEEDING_MODE = AUTOMATIC. This setting causes SQL Server to automatically create the database on each secondary server after it is added to the AG. Update the following script for your environment. Replace the <node1> and <node2> values with the names of the SQL Server instances that host the replicas. Replace the <5022> value with the port you set for the endpoint. Run the following Transact-SQL script on the primary SQL Server replica:SQLCREATE AVAILABILITY GROUP [ag1]WITH (CLUSTER_TYPE = NONE )FOR REPLICA ONN'<node1>' WITH (ENDPOINT_URL = N'tcp://<node1>:<5022>',​     AVAILABILITY_MODE = ASYNCHRONOUS_COMMIT,​     FAILOVER_MODE = MANUAL ,​     SEEDING_MODE = AUTOMATIC ,SECONDARY_ROLE (ALLOW_CONNECTIONS = ALL )​     ),N'<node2>' WITH (​     ENDPOINT_URL = N'tcp://<node2>:<5022>',​     AVAILABILITY_MODE = ASYNCHRONOUS_COMMIT,​     FAILOVER_MODE = MANUAL ,​     SEEDING_MODE = AUTOMATIC ,​     SECONDARY_ROLE (ALLOW_CONNECTIONS = ALL )​     );ALTER AVAILABILITY GROUP [ag1] GRANT CREATE ANY DATABASE ;Join secondary SQL Servers to the AGThe following Transact-SQL script joins a server to an AG named ag1. Update the script for your environment. On each secondary SQL Server replica, run the following Transact-SQL script to join the AG:SQLALTER AVAILABILITY GROUP [ag1] JOIN WITH (CLUSTER_TYPE = NONE );ALTER AVAILABILITY GROUP [ag1] GRANT CREATE ANY DATABASE ;Add a database to the availability groupEnsure that the database you add to the availability group is in full recovery mode and has a valid log backup. If this is a test database or a newly created database, take a database backup. On the primary SQL Server, run the following Transact-SQL script to create and back up a database called db1:SQLCREATE DATABASE [db1];ALTER DATABASE [db1] SET RECOVERY FULL ;BACKUP DATABASE [db1]TO DISK = N'/var/opt/mssql/data/db1.bak';On the primary SQL Server replica, run the following Transact-SQL script to add a database called db1 to an availability group called ag1:SQLALTER AVAILABILITY GROUP [ag1] ADD DATABASE [db1];Verify that the database is created on the secondary serversOn each secondary SQL Server replica, run the following query to see if the db1 database was created and is synchronized:SQLSELECT * FROM sys.databases WHERE name = 'db1';GOSELECT DB_NAME(database_id) AS 'database', synchronization_state_desc FROM sys.dm_hadr_database_replica_states;This AG isn't a high-availability configuration. If you need high availability, follow the instructions at Configure an Always On Availability Group for SQL Server on Linux. Specifically, create the AG with CLUSTER_TYPE=WSFC (in Windows) or CLUSTER_TYPE=EXTERNAL (in Linux). Then integrate with a cluster manager by using either Windows Server failover clustering on Windows or Pacemaker on Linux.Fail over the primary replica on a read-scale Availability GroupEach availability group has only one primary replica. The primary replica allows reads and writes. To change which replica is primary, you can fail over. In an availability group for high availability, the cluster manager automates the failover process. In an availability group with cluster type NONE, the failover process is manual.There are two ways to fail over the primary replica in an availability group with cluster type NONE:

*   Forced manual failover with data loss
*   Manual failover without data loss

Forced manual failover with data lossUse this method when the primary replica isn't available and can't be recovered.To force failover with data loss, connect to the SQL Server instance that hosts the target secondary replica and then run the following command:SQLALTER AVAILABILITY GROUP [ag1] FORCE_FAILOVER_ALLOW_DATA_LOSS;When the previous primary replica recovers, it will also assume the primary role. To ensure that the previous primary replica transitions into a secondary role run the following command on the previous primary replica.SQLALTER AVAILABILITY GROUP [ag1]  SET (ROLE = SECONDARY);Manual failover without data lossUse this method when the primary replica is available, but you need to temporarily or permanently change the configuration and change the SQL Server instance that hosts the primary replica. To avoid potential data loss, before you issue the manual failover, ensure that the target secondary replica is up to date.To manually fail over without data loss:

1.  Make the current primary and target secondary replica SYNCHRONOUS_COMMIT.

SQLALTER AVAILABILITY GROUP [ag1]     MODIFY REPLICA ON N'<node2>'     WITH (AVAILABILITY_MODE = SYNCHRONOUS_COMMIT);

2.  To identify that active transactions are committed to the primary replica and at least one synchronous secondary replica, run the following query:

SQLSELECT ag.name,drs.database_id,drs.group_id,drs.replica_id,drs.synchronization_state_desc,   ag.sequence_numberFROM sys.dm_hadr_database_replica_states drs, sys.availability_groups agWHERE drs.group_id = ag.group_id;The secondary replica is synchronized when synchronization_state_desc is SYNCHRONIZED.

3.  Update REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT to 1.

The following script sets REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT to 1 on an availability group named ag1\. Before you run the following script, replace ag1 with the name of your availability group:SQLALTER AVAILABILITY GROUP [ag1]     SET (REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT = 1);This setting ensures that every active transaction is committed to the primary replica and at least one synchronous secondary replica.

4.  Offline the primary replica in preparation for role changes.

SQLALTER AVAILABILITY GROUP [ag1] OFFLINE

5.  Promote the target secondary replica to primary.

SQLALTER AVAILABILITY GROUP ag1 FORCE_FAILOVER_ALLOW_DATA_LOSS;

6.  Update the role of the old primary to SECONDARY, run the following command on the SQL Server instance that hosts the old primary replica:

SQLALTER AVAILABILITY GROUP [ag1]     SET (ROLE = SECONDARY);

7.  Resume data movement, run the following command for every database in the availability group on the SQL Server instance that hosts the primary replica:

SQLALTER DATABASE [db1]     SET HADR RESUME

8.  Re-create any listener you created for read-scale purposes and that isn't managed by a cluster manager. If the original listener points to the old primary, drop it and re-create it to point to the new primary.

Configure SQL Server Always On Availability Group on Windows and Linux (cross-platform)This explains the steps to create an Always On Availability Group (AG) with one replica on a Windows server and the other replica on a Linux server. This configuration is cross-platform because the replicas are on different operating systems. Use this configuration for migration from one platform to the other or disaster recovery (DR). This configuration does not support high-availability because there is no cluster solution to manage a cross-platform configuration.![Hybrid None](Image00030.jpg)Before proceeding, you should be familiar with installation and configuration for SQL Server instances on Windows and Linux.ScenarioIn this scenario, two servers are on different operating systems. A Windows Server 2016 named WinSQLInstance hosts the primary replica. A Linux server named LinuxSQLInstance host the secondary replica.Configure the AGThe steps to create the AG are the same as the steps to create an AG for read-scale workloads. The AG cluster type is NONE, because there is no cluster manager.For the scripts in this article, angle brackets < and > identify values that you need to replace for your environment. The angle brackets themselves are not required for the scripts.

1.  Install SQL Server 2017 on Windows Server 2016, enable Always On Availability Groups from SQL Server Configuration Manager, and set mixed mode authentication.

  Enable Availability Groups![Enable Availability Groups](Image00038.jpg)SQL Server Configuration Manager notes that the computer is not a node in a failover cluster.After you enable Availability Groups, restart SQL Server.Set mixed mode authentication

2.  Install SQL Server 2017 on Linux. For instructions.

To enable hadr via mssql-conf from a shell prompt, issue the following command:Bashsudo /opt/mssql/bin/mssql-conf set hadr.hadrenabled 1After you enable hadr, restart the SQL Server instance.The following image shows this complete step.![Screenshot of a Git Bash window showing the command.](Image00039.jpg)

3.  Configure hosts file on both servers or register the server names with DNS.
4.  Open up firewall ports for TPC 1433 and 5022 on both Windows and Linux.
5.  On the primary replica, create a database login and password.

SQLCREATE LOGIN dbm_login WITH PASSWORD = '<C0m9L3xP@55w0rd!>';CREATE USER dbm_user FOR LOGIN dbm_login;GO

6.  On the primary replica, create a master key and certificate, then back up the certificate with a private key.

SQLCREATE MASTER KEY ENCRYPTION BY PASSWORD = '<C0m9L3xP@55w0rd!>';CREATE CERTIFICATE dbm_certificate WITH SUBJECT = 'dbm';BACKUP CERTIFICATE dbm_certificateTO FILE = 'C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\MSSQL\DATA\dbm_certificate.cer'WITH PRIVATE KEY (        FILE = 'C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\MSSQL\DATA\dbm_certificate.pvk',        ENCRYPTION BY PASSWORD = '<C0m9L3xP@55w0rd!>'    );GO

7.  Copy the certificate and private key to the Linux server (secondary replica) at /var/opt/mssql/data. You can use pscp to copy the files to the Linux server.
8.  Set the group and ownership of the private key and the certificate to mssql:mssql.

The following script sets the group and ownership of the files.Bashsudo chown mssql:mssql /var/opt/mssql/data/dbm_certificate.pvksudo chown mssql:mssql /var/opt/mssql/data/dbm_certificate.cerIn the following diagram, ownership and group are set correctly for the certificate and key.![Screenshot of a Git Bash window showing the .cer and the .pvk in the /var/opt/mssql/data folder.](Image00040.jpg)

9.  On the secondary replica, create a database login and password and create a master key.

SQLCREATE LOGIN dbm_login WITH PASSWORD = '<C0m9L3xP@55w0rd!>';CREATE USER dbm_user FOR LOGIN dbm_login;GOCREATE MASTER KEY ENCRYPTION BY PASSWORD = '<M@st3rKeyP@55w0rD!>'GO

10.  On the secondary replica, restore the certificate you copied to /var/opt/mssql/data.

SQLCREATE CERTIFICATE dbm_certificate       AUTHORIZATION dbm_user    FROM FILE = '/var/opt/mssql/data/dbm_certificate.cer'    WITH PRIVATE KEY (    FILE = '/var/opt/mssql/data/dbm_certificate.pvk',    DECRYPTION BY PASSWORD = '<C0m9L3xP@55w0rd!>')GO

11.  On the primary replica, create an endpoint.

SQLCREATE ENDPOINT [Hadr_endpoint]    AS TCP (LISTENER_IP = (0.0.0.0), LISTENER_PORT = 5022)    FOR DATA_MIRRORING (        ROLE = ALL ,        AUTHENTICATION = CERTIFICATE dbm_certificate,        ENCRYPTION = REQUIRED ALGORITHM AES        );ALTER ENDPOINT [Hadr_endpoint] STATE = STARTED;GRANT CONNECT ON ENDPOINT::[Hadr_endpoint] TO [dbm_login]GO ImportantThe firewall must be open for the listener TCP port. In the preceding script, the port is 5022\. Use any available TCP port.

12.  On the secondary replica, create the endpoint. Repeat the preceding script on the secondary replica to create the endpoint.
13.  On the primary replica, create the AG with CLUSTER_TYPE = NONE. The example script uses SEEDING_MODE = AUTOMATIC to create the AG.

Before you run the script, update the values for your AGs.

*   Replace <WinSQLInstance> with the server name of the primary replica SQL Server instance.
*   Replace <LinuxSQLInstance> with the server name of the secondary replica SQL Server instance.

To create the AG, update the values and run the script on the primary replica.SQLCREATE AVAILABILITY GROUP [ag1]    WITH (CLUSTER_TYPE = NONE )    FOR REPLICA ONN'<WinSQLInstance>'   ​ WITH (        ENDPOINT_URL = N'tcp://<WinSQLInstance>:5022',        AVAILABILITY_MODE = ASYNCHRONOUS_COMMIT,   ​     SEEDING_MODE = AUTOMATIC ,       ​ FAILOVER_MODE = MANUAL , ​    SECONDARY_ROLE (ALLOW_CONNECTIONS = ALL )   ​ ​ ),N'<LinuxSQLInstance>'    WITH (   ​     ENDPOINT_URL = N'tcp://<LinuxSQLInstance>:5022',        AVAILABILITY_MODE = ASYNCHRONOUS_COMMIT,        SEEDING_MODE = AUTOMATIC , ​    FAILOVER_MODE = MANUAL , ​    SECONDARY_ROLE (ALLOW_CONNECTIONS = ALL )        )GO

14.  On the secondary replica, join the AG.

SQLALTER AVAILABILITY GROUP [ag1] JOIN WITH (CLUSTER_TYPE = NONE )ALTER AVAILABILITY GROUP [ag1] GRANT CREATE ANY DATABASEGO

15.  Create a database for the AG. The example steps use a database named <TestDB>. If you are using automatic seeding, set the same path for both the data and the log files.

Before you run the script, update the values for your database.

*   Replace <TestDB> with the name of your database.
*   Replace <F:\Path> with the path for your database and log files. Use the same path for the database and log files.

You can also use the default paths.To create your database, run the script.SQLCREATE DATABASE [<TestDB>]   CONTAINMENT = NONE  ON   PRIMARY ( NAME = N'<TestDB>', FILENAME = N'<F:\Path>\<TestDB>.mdf')  LOG ON ( NAME = N'<TestDB>_log', FILENAME = N'<F:\Path>\<TestDB>_log.ldf')GO

16.  Take a full backup of the database.
17.  If you are not using automatic seeding, restore the database on the secondary replica (Linux) server. Migrate a SQL Server database from Windows to Linux using backup and restore. Restore the database WITH NORECOVERY on the secondary replica.
18.  Add the database to the AG. Update the example script. Replace <TestDB> with the name of your database. On the primary replica, run the SQL query to add the database to the AG.

SQLALTER AG [ag1] ADD DATABASE <TestDB>GO

19.  Verify that the database is getting populated on the secondary replica.

Fail over the primary replicaEach availability group has only one primary replica. The primary replica allows reads and writes. To change which replica is primary, you can fail over. In an availability group for high availability, the cluster manager automates the failover process. In an availability group with cluster type NONE, the failover process is manual.There are two ways to fail over the primary replica in an availability group with cluster type NONE:

*   Forced manual failover with data loss
*   Manual failover without data loss

Forced manual failover with data lossUse this method when the primary replica isn't available and can't be recovered.To force failover with data loss, connect to the SQL Server instance that hosts the target secondary replica and then run the following command:SQLALTER AVAILABILITY GROUP [ag1] FORCE_FAILOVER_ALLOW_DATA_LOSS;When the previous primary replica recovers, it will also assume the primary role. To ensure that the previous primary replica transitions into a secondary role run the following command on the previous primary replica.SQLALTER AVAILABILITY GROUP [ag1]  SET (ROLE = SECONDARY);Manual failover without data lossUse this method when the primary replica is available, but you need to temporarily or permanently change the configuration and change the SQL Server instance that hosts the primary replica. To avoid potential data loss, before you issue the manual failover, ensure that the target secondary replica is up to date.To manually fail over without data loss:

1.  Make the current primary and target secondary replica SYNCHRONOUS_COMMIT.

SQLALTER AVAILABILITY GROUP [ag1]     MODIFY REPLICA ON N'<node2>'     WITH (AVAILABILITY_MODE = SYNCHRONOUS_COMMIT);

2.  To identify that active transactions are committed to the primary replica and at least one synchronous secondary replica, run the following query:

SQLSELECT ag.name,drs.database_id,drs.group_id,drs.replica_id,drs.synchronization_state_desc,   ag.sequence_numberFROM sys.dm_hadr_database_replica_states drs, sys.availability_groups agWHERE drs.group_id = ag.group_id;The secondary replica is synchronized when synchronization_state_desc is SYNCHRONIZED.

3.  Update REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT to 1.

The following script sets REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT to 1 on an availability group named ag1\. Before you run the following script, replace ag1 with the name of your availability group:SQLALTER AVAILABILITY GROUP [ag1]     SET (REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT = 1);This setting ensures that every active transaction is committed to the primary replica and at least one synchronous secondary replica.

4.  Offline the primary replica in preparation for role changes.

SQLALTER AVAILABILITY GROUP [ag1] OFFLINE

5.  Promote the target secondary replica to primary.

SQLALTER AVAILABILITY GROUP ag1 FORCE_FAILOVER_ALLOW_DATA_LOSS;

6.  Update the role of the old primary to SECONDARY, run the following command on the SQL Server instance that hosts the old primary replica:

SQLALTER AVAILABILITY GROUP [ag1]     SET (ROLE = SECONDARY);

7.  Resume data movement, run the following command for every database in the availability group on the SQL Server instance that hosts the primary replica:

SQLALTER DATABASE [db1]     SET HADR RESUME

8.  Re-create any listener you created for read-scale purposes and that isn't managed by a cluster manager. If the original listener points to the old primary, drop it and re-create it to point to the new primary.

This article reviewed the steps to create a cross-platform AG to support migration or read-scale workloads. It can be used for manual disaster recovery. It also explained how to fail over the AG. A cross-platform AG uses cluster type NONE and does not support high availability because there is no cluster tool across-platforms.High availability for SQL Server containersCreate and manage your SQL Server instances natively in Kubernetes.Deploy SQL Server to docker containers managed by Kubernetes. In Kubernetes, a container with a SQL Server instance can automatically recover in case a cluster node fails.SQL Server 2017 introduces a Docker image that can deploy on Kubernetes. You can configure the image with a Kubernetes persistent volume claim (PVC). Kubernetes monitors the SQL Server process in the container. If the process, pod, container, or node fail, Kubernetes automatically bootstraps another instance and reconnects to the storage.Container with SQL Server instance on KubernetesKubernetes 1.6 and later has support for storage classes, persistent volume claims, and the Azure disk volume type.In this configuration, Kubernetes plays the role of the container orchestrator.![Diagram of Kubernetes SQL Server cluster](Image00041.jpg)In the preceding diagram, mssql-server is a SQL Server instance (container) in a pod. A replica set ensures that the pod is automatically recovered after a node failure. Applications connect to the service. In this case, the service represents a load balancer that hosts an IP address that stays the same after failure of the mssql-server.Kubernetes orchestrates the resources in the cluster. When a node hosting a SQL Server instance container fails, it bootstraps a new container with a SQL Server instance and attaches it to the same persistent storage.SQL Server 2017 and later support containers on Kubernetes.Deploy a SQL Server container in Kubernetes with Azure Kubernetes Services (AKS)Learn how to configure a SQL Server instance on Kubernetes in Azure Kubernetes Service (AKS), with persistent storage for high availability (HA). The solution provides resiliency. If the SQL Server instance fails, Kubernetes automatically re-creates it in a new pod. Kubernetes also provides resiliency against a node failure.This tutorial demonstrates how to configure a highly available SQL Server instance in a container on AKS.

*   Create an SA password
*   Create storage
*   Create the deployment
*   Connect with SQL Server Management Studio (SSMS)
*   Verify failure and recovery

HA solution on Kubernetes running in Azure Kubernetes ServiceKubernetes 1.6 and later has support for storage classes, persistent volume claims, and the Azure disk volume type. You can create and manage your SQL Server instances natively in Kubernetes. The example in this article shows how to create a deployment to achieve a high availability configuration similar to a shared disk failover cluster instance. In this configuration, Kubernetes plays the role of the cluster orchestrator. When a SQL Server instance in a container fails, the orchestrator bootstraps another instance of the container that attaches to the same persistent storage.![SQL Server container on Kubernetes cluster](Image00041.jpg)In the preceding diagram, mssql-server is a container in a pod. Kubernetes orchestrates the resources in the cluster. A replica set ensures that the pod is automatically recovered after a node failure. Applications connect to the service. In this case, the service represents a load balancer that hosts an IP address that stays the same after failure of the mssql-server.In the following diagram, the mssql-server container has failed. As the orchestrator, Kubernetes guarantees the correct count of healthy instances in the replica set, and starts a new container according to the configuration. The orchestrator starts a new pod on the same node, and mssql-server reconnects to the same persistent storage. The service connects to the re-created mssql-server.![SQL Server pod fail on Kubernetes cluster](Image00042.jpg)In the following diagram, the node hosting the mssql-server container has failed. The orchestrator starts the new pod on a different node, and mssql-server reconnects to the same persistent storage. The service connects to the re-created mssql-server.![SQL Server pod recover on Kubernetes cluster](Image00043.jpg)Prerequisites

*   Kubernetes cluster
    *   The tutorial requires a Kubernetes cluster. The steps use kubectl to manage the cluster.
*   Azure CLI 2.0.23
    *   The instructions in this tutorial have been validated against Azure CLI 2.0.23.

Create an SA passwordCreate an SA password in the Kubernetes cluster. Kubernetes can manage sensitive configuration information, like passwords as secrets.The following command creates a password for the SA account:Azure CLIkubectl create secret generic mssql --from-literal =SA_PASSWORD="MyC0m9l&xP@ssw0rd"Replace MyC0m9l&xP@ssw0rd with a complex password.To create a secret in Kubernetes named mssql that holds the value MyC0m9l&xP@ssw0rd for the SA_PASSWORD, run the command.Create storageConfigure a persistent volume and persistent volume claim in the Kubernetes cluster. Complete the following steps:

1.  Create a manifest to define the storage class and the persistent volume claim. The manifest specifies the storage provisioner, parameters, and reclaim policy. The Kubernetes cluster uses this manifest to create the persistent storage.

The following yaml example defines a storage class and persistent volume claim. The storage class provisioner is azure-disk, because this Kubernetes cluster is in Azure. The storage account type is Standard_LRS. The persistent volume claim is named mssql-data. The persistent volume claim metadata includes an annotation connecting it back to the storage class.YAMLkind: StorageClassapiVersion: storage.k8s.io/v1metadata:     name: azure-diskprovisioner: kubernetes.io/azure-diskparameters:  storageaccounttype: Standard_LRS  kind: Managed---kind: PersistentVolumeClaimapiVersion: v1metadata:  name: mssql-data  annotations:    volume.beta.kubernetes.io/storage-class: azure-diskspec:  accessModes:  - ReadWriteOnce  resources:    requests:      storage: 8GiSave the file (for example, pvc.yaml).

2.  Create the persistent volume claim in Kubernetes.

Azure CLIkubectl apply -f <Path to pvc.yaml file><Path to pvc.yaml file> is the location where you saved the file.The persistent volume is automatically created as an Azure storage account, and bound to the persistent volume claim.![Screenshot of persistent volume claim command](Image00044.jpg)

3.  Verify the persistent volume claim.

Azure CLIkubectl describe pvc <PersistentVolumeClaim><PersistentVolumeClaim> is the name of the persistent volume claim.In the preceding step, the persistent volume claim is named mssql-data. To see the metadata about the persistent volume claim, run the following command:Azure CLIkubectl describe pvc mssql-dataThe returned metadata includes a value called Volume. This value maps to the name of the blob.![Screenshot of returned metadata, including Volume](Image00045.jpg)The value for volume matches part of the name of the blob in the following image from the Azure portal:![Screenshot of Azure portal blob name](Image00046.jpg)

4.  Verify the persistent volume.

Azure CLIkubectl describe pvkubectl returns metadata about the persistent volume that was automatically created and bound to the persistent volume claim.Create the deploymentIn this example, the container hosting the SQL Server instance is described as a Kubernetes deployment object. The deployment creates a replica set. The replica set creates the pod.In this step, create a manifest to describe the container based on the SQL Server mssql-server-linux Docker image. The manifest references the mssql-server persistent volume claim, and the mssql secret that you already applied to the Kubernetes cluster. The manifest also describes a service. This service is a load balancer. The load balancer guarantees that the IP address persists after SQL Server instance is recovered.

1.  Create a manifest (a YAML file) to describe the deployment. The following example describes a deployment, including a container based on the SQL Server container image.

YAMLapiVersion: apps/v1kind: Deploymentmetadata:  name: mssql-deploymentspec:  replicas: 1  selector:     matchLabels:       app: mssql  template:    metadata:      labels:        app: mssql    spec:      terminationGracePeriodSeconds: 30      hostname: mssqlinst      securityContext:        fsGroup: 10001      containers:      - name: mssql        image: mcr.microsoft.com/mssql/server:2019-latest        ports:        - containerPort: 1433        env:        - name: MSSQL_PID          value: "Developer"        - name: ACCEPT_EULA          value: "Y"        - name: SA_PASSWORD          valueFrom:            secretKeyRef:              name: mssqlkey: SA_PASSWORD        volumeMounts:        - name: mssqldb          mountPath: /var/opt/mssql      volumes:      - name: mssqldb        persistentVolumeClaim:          claimName: mssql-data---apiVersion: v1kind: Servicemetadata:  name: mssql-deploymentspec:  selector:    app: mssql  ports:    - protocol: TCP      port: 1433      targetPort: 1433  type: LoadBalancerCopy the preceding code into a new file, named sqldeployment.yaml. Update the following values:

*   MSSQL_PID value: "Developer": Sets the container to run SQL Server Developer edition. Developer edition is not licensed for production data. If the deployment is for production use, set the appropriate edition (Enterprise, Standard, or Express).
*   persistentVolumeClaim: This value requires an entry for claimName: that maps to the name used for the persistent volume claim. This tutorial uses mssql-data.
*   name: SA_PASSWORD: Configures the container image to set the SA password, as defined in this section.

YAMLvalueFrom:  secretKeyRef:    name: mssql    key: SA_PASSWORDWhen Kubernetes deploys the container, it refers to the secret named mssql to get the value for the password.

*   securityContext : A securityContext defines privilege and access control settings for a Pod or Container, in this case it is specified at the pod level, so all containers ( in this case only one) adhere to that security context. In the security context we define the fsGroup with the value 10001 ( which is the GID for mssql group) means, all processes of the container are also part of the supplementary group ID 10001(mssql). The owner for volume /var/opt/mssql and any files created in that volume will be Group ID 10001(mssql group).

2.  Create the deployment.

Azure CLIkubectl apply -f <Path to sqldeployment.yaml file><Path to sqldeployment.yaml file> is the location where you saved the file.![Screenshot of deployment command](Image00047.jpg)The deployment and service are created. The SQL Server instance is in a container, connected to persistent storage.To view the status of the pod, type kubectl get pod.![Screenshot of get pod command](Image00048.jpg)In the preceding image, the pod has a status of Running. This status indicates that the container is ready. This may take several minutes.

3.  Verify the services are running. Run the following command:

Azure CLIkubectl get servicesThis command returns services that are running, as well as the internal and external IP addresses for the services. Note the external IP address for the mssql-deployment service. Use this IP address to connect to SQL Server.![Screenshot of get service command](Image00049.jpg)For more information about the status of the objects in the Kubernetes cluster, run:Azure CLIaz aks browse --resource-group <MyResourceGroup> --name <MyKubernetesClustername>

4.  You can also verify the container is running as non-root by running the following command:

Azure CLIkubectl.exe exec <name of SQL POD> -it -- /bin/bashand then run 'whoami' you should see the username as mssql. Which is a non-root user.Azure CLIwhoamiConnect to the SQL Server instanceIf you configured the container as described, you can connect with an application from outside the Azure virtual network. Use the sa account and the external IP address for the service. Use the password that you configured as the Kubernetes secret.You can use the following applications to connect to the SQL Server instance.

*   SSMS
*   SSDT
*   sqlcmd

To connect with sqlcmd, run the following command:cmdsqlcmd -S <External IP Address> -U sa -P "MyC0m9l&xP@ssw0rd"Replace the following values:

*   <External IP Address> with the IP address for the mssql-deployment service
*   MyC0m9l&xP@ssw0rd with your password

Verify failure and recoveryTo verify failure and recovery, you can delete the pod. Do the following steps:

1.  List the pod running SQL Server.

Azure CLIkubectl get podsNote the name of the pod running SQL Server.

2.  Delete the pod.

Azure CLIkubectl delete pod mssql-deployment- 0mssql-deployment-0 is the value returned from the previous step for pod name.Kubernetes automatically re-creates the pod to recover a SQL Server instance, and connect to the persistent storage. Use kubectl get pods to verify that a new pod is deployed. Use kubectl get services to verify that the IP address for the new container is the same.Security limitations for SQL Server on LinuxSQL Server on Linux currently has the following limitations:

*   A standard password policy is provided. MUST_CHANGE is the only option you may configure. CHECK_POLICY option is not supported.
*   Extensible Key Management is not supported.
*   Using keys stored in the Azure Key Vault is not supported.
*   SQL Server generates its own self-signed certificate for encrypting connections. SQL Server can be configured to use a user provided certificate for TLS.

Security features of SQL Server on LinuxIf you are a Linux user who is new to SQL Server, the following tasks walk you through some of the security tasks. These are not unique or specific to Linux, but it helps to give you an idea of areas to investigate further. In each example, a link is provided to the in-depth documentation for that area.Create a login and a database userGrant others access to SQL Server by creating a login in the master database using the CREATE LOGIN statement. For example:CREATE LOGIN Larry WITH PASSWORD = '************'; Logins can connect to SQL Server and have access (with limited permissions) to the master database. To connect to a user-database, a login needs a corresponding identity at the database level, called a database user. Users are specific to each database and must be separately created in each database to grant them access. The following example moves you into the AdventureWorks2014 database, and then uses the CREATE USER statement to create a user named Larry that is associated with the login named Larry. Though the login and the user are related (mapped to each other), they are different objects. The login is a server-level principle. The user is a database-level principal.USE AdventureWorks2014;GOCREATE USER Larry;GO

*   A SQL Server administrator account can connect to any database and can create more logins and users in any database.
*   When someone creates a database they become the database owner, which can connect to that database. Database owners can create more users.

Later you can authorize other logins to create a more logins by granting them the ALTER ANY LOGIN permission. Inside a database, you can authorize other users to create more users by granting them the ALTER ANY USER permission. For example:GRANT ALTER ANY LOGIN TO Larry;  GO  USE AdventureWorks2014;  GO  GRANT ALTER ANY USER TO Jerry;   GO  Now the login Larry can create more logins, and the user Jerry can create more users.Granting access with least privilegesThe first people to connect to a user-database will be the administrator and database owner accounts. However these users have all the permissions available on the database. This is more permission than most users should have.When you are just getting started, you can assign some general categories of permissions by using the built-in fixed database roles. For example, the db_datareader fixed database role can read all tables in the database, but make no changes. Grant membership in a fixed database role by using the ALTER ROLE statement. The following example add the user Jerry to the db_datareader fixed database role.USE AdventureWorks2014;  GO  ALTER ROLE db_datareader ADD MEMBER Jerry;  For a list of the fixed database roles, see Database-Level Roles.Later, when you are ready to configure more precise access to your data (highly recommended), create your own user-defined database roles using CREATE ROLE statement. Then assign specific granular permissions to you custom roles.For example, the following statements create a database role named Sales, grants the Sales group the ability to see, update, and delete rows from the Orders table, and then adds the user Jerry to the Sales role.CREATE ROLE Sales;  GRANT SELECT ON Object::Sales TO Orders;  GRANT UPDATE ON Object::Sales TO Orders;  GRANT DELETE ON Object::Sales TO Orders;  ALTER ROLE Sales ADD MEMBER Jerry;  Configure row-level securityRow-Level Security enables you to restrict access to rows in a database based on the user executing a query. This feature is useful for scenarios like ensuring that customers can only access their own data or that workers can only access data that is pertinent to their department.The following steps walk through setting up two Users with different row-level access to the Sales.SalesOrderHeader table.Create two user accounts to test the row level security:    USE AdventureWorks2014;  GO  CREATE USER Manager WITHOUT LOGIN;    CREATE USER SalesPerson280 WITHOUT LOGIN;   Grant read access on the Sales.SalesOrderHeader table to both users:    GRANT SELECT ON Sales.SalesOrderHeader TO Manager;     GRANT SELECT ON Sales.SalesOrderHeader TO SalesPerson280;Create a new schema and inline table-valued function. The function returns 1 when a row in the SalesPersonID column matches the ID of a SalesPerson login or if the user executing the query is the Manager user.CREATE SCHEMA Security;  GO  CREATE FUNCTION Security.fn_securitypredicate(@SalesPersonID AS int)    RETURNS TABLE  WITH SCHEMABINDING  AS    RETURN SELECT 1 AS fn_securitypredicate_result   WHERE ('SalesPerson' + CAST(@SalesPersonId as VARCHAR(16)) = USER_NAME())    OR (USER_NAME() = 'Manager');   Create a security policy adding the function as both a filter and a block predicate on the table:CREATE SECURITY POLICY SalesFilter  ADD FILTER PREDICATE Security.fn_securitypredicate(SalesPersonID)   ON Sales.SalesOrderHeader,  ADD BLOCK PREDICATE Security.fn_securitypredicate(SalesPersonID)   ON Sales.SalesOrderHeader  WITH (STATE = ON);  Execute the following to query the SalesOrderHeader table as each user. Verify that SalesPerson280 only sees the 95 rows from their own sales and that the Manager can see all the rows in the table.EXECUTE AS USER = 'SalesPerson280';  SELECT * FROM Sales.SalesOrderHeader;   REVERT;EXECUTE AS USER = 'Manager';  SELECT * FROM Sales.SalesOrderHeader;  REVERT;  Alter the security policy to disable the policy. Now both users can access all rows.ALTER SECURITY POLICY SalesFilter  WITH (STATE = OFF);   Enable dynamic data maskingDynamic Data Masking enables you to limit the exposure of sensitive data to users of an application by fully or partially masking certain columns.Use an ALTER TABLE statement to add a masking function to the EmailAddress column in the Person.EmailAddress table:USE AdventureWorks2014;GOALTER TABLE Person.EmailAddress    ALTER COLUMN EmailAddress   ADD MASKED WITH (FUNCTION = 'email()');Create a new user TestUser with SELECT permission on the table, then execute a query as TestUser to view the masked data:CREATE USER TestUser WITHOUT LOGIN;  GRANT SELECT ON Person.EmailAddress TO TestUser;   EXECUTE AS USER = 'TestUser';  SELECT EmailAddressID, EmailAddress FROM Person.EmailAddress;      REVERT;   Enable Transparent Data EncryptionOne threat to your database is the risk that someone will steal the database files off of your hard-drive. This could happen with an intrusion that gets elevated access to your system, through the actions of a problem employee, or by theft of the computer containing the files (such as a laptop).Transparent Data Encryption (TDE) encrypts the data files as they are stored on the hard drive. The master database of the SQL Server database engine has the encryption key, so that the database engine can manipulate the data. The database files cannot be read without access to the key. High-level administrators can manage, backup, and recreate the key, so the database can be moved, but only by selected people. When TDE is configured, the tempdb database is also automatically encrypted.Since the Database Engine can read the data, Transparent Data Encryption does not protect against unauthorized access by administrators of the computer who can directly read memory, or access SQL Server through an administrator account.Configure TDE

*   Create a master key
*   Create or obtain a certificate protected by the master key
*   Create a database encryption key and protect it by the certificate
*   Set the database to use encryption

Configuring TDE requires CONTROL permission on the master database and CONTROL permission on the user database. Typically an administrator configures TDE.The following example illustrates encrypting and decrypting the AdventureWorks2014 database using a certificate installed on the server named MyServerCert.USE master;GOCREATE MASTER KEY ENCRYPTION BY PASSWORD = '**********'; GOCREATE CERTIFICATE MyServerCert WITH SUBJECT = 'My Database Encryption Key Certificate'; GOUSE AdventureWorks2014;  GOCREATE DATABASE ENCRYPTION KEY WITH ALGORITHM = AES_256 ENCRYPTION BY SERVER CERTIFICATE MyServerCert; GOALTER DATABASE AdventureWorks2014SET ENCRYPTION ON;  To remove TDE, execute ALTER DATABASE AdventureWorks2014 SET ENCRYPTION OFF;The encryption and decryption operations are scheduled on background threads by SQL Server. You can view the status of these operations using the catalog views and dynamic management views in the list that appears later in this topic.Configure backup encryptionSQL Server has the ability to encrypt the data while creating a backup. By specifying the encryption algorithm and the encryptor (a certificate or asymmetric key) when creating a backup, you can create an encrypted backup file.     The following example creates a certificate, and then creates a backup protected by the certificate.USE master;  GO  CREATE CERTIFICATE BackupEncryptCert  WITH SUBJECT = 'Database backups';  GOBACKUP DATABASE [AdventureWorks2014]  TO DISK = N'/var/opt/mssql/backups/AdventureWorks2014.bak' WITHCOMPRESSION,ENCRYPTION  (ALGORITHM = AES_256,SERVER CERTIFICATE = BackupEncryptCert),STATS = 10GOActive Directory authentication for SQL Server on LinuxThis provides an overview of Active Directory (AD) authentication for SQL Server on Linux. AD authentication is also known as Integrated authentication in SQL Server.AD authentication overviewAD authentication enables domain-joined clients on either Windows or Linux to authenticate to SQL Server using their domain credentials and the Kerberos protocol.AD Authentication has the following advantages over SQL Server Authentication:

*   Users authenticate via single sign-on, without being prompted for a password.
*   By creating logins for AD groups, you can manage access and permissions in SQL Server using AD group memberships.
*   Each user has a single identity across your organization, so you don't have to keep track of which SQL Server logins correspond to which people.
*   AD enables you to enforce a centralized password policy across your organization.

Configuration stepsIn order to use Active Directory authentication, you must have an AD Domain Controller (Windows) on your network.Known issues

*   At this time, the only authentication method supported for database mirroring endpoint is CERTIFICATE. WINDOWS authentication method will be enabled in a future release.
*   SQL Server on Linux does not support NTLM protocol for remote connections. Local connection may work using NTLM.

Join SQL Server on a Linux host to an Active Directory domainThis provides general guidance on how to join a SQL Server Linux host machine to an Active Directory (AD) domain. There are two methods: use a built-in SSSD package or use third-party Active Directory providers. Examples of third-party domain join products are PowerBroker Identity Services (PBIS), One Identity, and Centrify. This guide includes steps to check your Active Directory configuration. However, it is not intended to provide instructions on how to join a machine to a domain when using third-party utilities.Before you configure Active Directory authentication, you need to set up an Active Directory domain controller, Windows, on your network. Then join your SQL Server on Linux host to an Active Directory domain.Check the connection to a domain controllerCheck that you can contact the domain controller with both the short and fully qualified names of the domain:Bashping contosoping contoso.comIf either of these name checks fail, update your domain search list. The following sections provide instructions for Ubuntu, Red Hat Enterprise Linux (RHEL), and SUSE Linux Enterprise Server (SLES) respectively.Ubuntu 16.04

1.  Edit the /etc/network/interfaces file, so that your Active Directory domain is in the domain search list:

/etc/network/interfaces Copy# The primary network interfaceauto eth0iface eth0 inet dhcpdns-nameservers **<AD domain controller IP address>**dns-search **<AD domain name>**

2.  After editing this file, restart the network service:

Bashsudo ifdown eth0 && sudo ifup eth0

3.  Next, check that your /etc/resolv.conf file contains a line like the following example:

/etc/resolv.confsearch contoso.com com nameserver **<AD domain controller IP address>**RHEL 7.x

1.  Edit the /etc/sysconfig/network-scripts/ifcfg-eth0 file, so that your Active Directory domain is in the domain search list. Or edit another interface config file as appropriate:

/etc/sysconfig/network-scripts/ifcfg-eth0PEERDNS=noDNS1=**<AD domain controller IP address>**DOMAIN="contoso.com com"

2.  After editing this file, restart the network service:

Bashsudo systemctl restart network

3.  Now check that your /etc/resolv.conf file contains a line like the following example:

/etc/resolv.confsearch contoso.com com nameserver **<AD domain controller IP address>**

4.  If you still cannot ping the domain controller, find the fully qualified domain name and IP address of the domain controller. An example domain name is DC1.CONTOSO.COM. Add the following entry to /etc/hosts:

/etc/hosts**<IP address>** DC1.CONTOSO.COM CONTOSO.COM CONTOSOSLES 12

1.  Edit the /etc/sysconfig/network/config file, so that your Active Directory domain controller IP is used for DNS queries and your Active Directory domain is in the domain search list:

/etc/sysconfig/network/configNETCONFIG_DNS_STATIC_SEARCHLIST=""NETCONFIG_DNS_STATIC_SERVERS="**<AD domain controller IP address>**"

2.  After editing this file, restart the network service:

Bashsudo systemctl restart network

3.  Next, check that your /etc/resolv.conf file contains a line like the following example:

/etc/resolv.confsearch contoso.com comnameserver **<AD domain controller IP address>**Join to the AD domainAfter the basic configuration and connectivity with domain controller is verified, there are two options for joining a SQL Server Linux host machine with Active Directory domain controller:Option 1: Use SSSD package to join AD domainThis method joins the SQL Server host to an AD domain using realmd and sssd packages.Use the following steps to join a SQL Server host to an Active Directory domain:

1.  Use realmd to join your host machine to your AD Domain. You must first install both the realmd and Kerberos client packages on the SQL Server host machine using your Linux distribution's package manager:

RHEL:basesudo yum install realmd krb5-workstationSUSE:Bashsudo zypper install realmd krb5-clientUbuntu:Bashsudo apt-get install realmd krb5-user software-properties-common python-software-properties packagekit

2.  If the Kerberos client package installation prompts you for a realm name, enter your domain name in uppercase.
3.  After you confirm that your DNS is configured properly, join the domain by running the following command. You must authenticate using an AD account that has sufficient privileges in AD to join a new machine to the domain. This command creates a new computer account in AD, creates the /etc/krb5.keytab host keytab file, configures the domain in /etc/sssd/sssd.conf, and updates /etc/krb5.conf.

Bashsudo realm join contoso.com -U 'user@CONTOSO.COM' -vYou should see the message, Successfully enrolled machine in realm.The following table lists some error messages that you could receive and suggestions on resolving them:

| Error message | Recommendation |
| --- | --- |
| Necessary packages are not installed | Install those packages using your Linux distribution's package manager before running the realm join command again. |
| Insufficient permissions to join the domain | Check with a domain administrator that you have sufficient permissions to join Linux machines to your domain. |
| KDC reply did not match expectations | You may not have specified the correct realm name for the user. Realm names are case-sensitive, usually uppercase, and can be identified with the command realm discover contoso.com. |

SQL Server uses SSSD and NSS for mapping user accounts and groups to security identifiers (SIDs). SSSD must be configured and running for SQL Server to create AD logins successfully. realmd usually does this automatically as part of joining the domain, but in some cases, you must do this separately.

4.  Verify that you can now gather information about a user from the domain, and that you can acquire a Kerberos ticket as that user. The following example uses id, kinit, and klist commands for this.

Bashid user@contoso.comuid=1348601103(user@contoso.com) gid=1348600513(domain group@contoso.com) groups=1348600513(domain group@contoso.com)kinit user@CONTOSO.COMPassword for user@CONTOSO.COM:klistTicket cache: FILE:/tmp/krb5cc_1000Default principal: user@CONTOSO.COMOption 2: Use third-party openldap provider utilitiesYou can use third-party utilities such as PBIS, VAS, or Centrify. This article does not cover steps for each individual utility. You must first use one of these utilities to join the Linux host for SQL Server to the domain before continuing forward.SQL Server does not use third-party integrator's code or library for any AD-related queries. SQL Server always queries AD using openldap library calls directly in this setup. The third-party integrators are only used to join the Linux host to AD domain, and SQL Server does not have any direct communication with these utilities.Verify that your /etc/krb5.conf is configured correctly. For most third-party Active Directory providers, this configuration is done automatically. However, check /etc/krb5.conf for the following values to prevent any future issues:/etc/krb5.conf[libdefaults]default_realm = CONTOSO.COM[realms]CONTOSO.COM = {}[domain_realm]contoso.com = CONTOSO.COM.contoso.com = CONTOSO.COMCheck that the reverse DNS is properly configuredThe following command should return the fully qualified domain name (FQDN) of the host that runs SQL Server. An example is SqlHost.contoso.com.Bashhost **<IP address of SQL Server host>**The output of this command should be similar to **<reversed IP address>**.in-addr.arpa domain name pointer SqlHost.contoso.com. If this command does not return your host's FQDN, or if the FQDN is incorrect, add a reverse DNS entry for your SQL Server on Linux host to your DNS server.Encrypting Connections to SQL Server on LinuxSQL Server on Linux can use Transport Layer Security (TLS) to encrypt data that is transmitted across a network between a client application and an instance of SQL Server. SQL Server supports the same TLS protocols on both Windows and Linux: TLS 1.2, 1.1, and 1.0\. However, the steps to configure TLS are specific to the operating system on which SQL Server is running.Requirements for CertificatesBefore getting started, you need to make sure your certificates follow these requirements:

*   The current system time must be after the Valid from property of the certificate and before the Valid to property of the certificate.
*   The certificate must be meant for server authentication. This requires the Enhanced Key Usage property of the certificate to specify Server Authentication (1.3.6.1.5.5.7.3.1).
*   The certificate must be created by using the KeySpec option of AT_KEYEXCHANGE. Usually, the certificate's key usage property (KEY_USAGE) also includes key encipherment (CERT_KEY_ENCIPHERMENT_KEY_USAGE).
*   The Subject property of the certificate must indicate that the common name (CN) is the same as the host name or fully qualified domain name (FQDN) of the server computer. Note: Wild Card Certificates are supported.

Configuring the OpenSSL Libraries for Use (Optional)You can create symbolic links in the /opt/mssql/lib/ directory that reference which libcrypto.so and libssl.so libraries should be used for encryption. This is useful if you want to force SQL Server to use a specific version of OpenSSL other than the default provided by the system. If these symbolic links are not present, SQL Server will load the default configured OpenSSL libraries on the system.These symbolic links should be named libcrypto.so and libssl.so and placed in the /opt/mssql/lib/ directory.OverviewTLS is used to encrypt connections from a client application to SQL Server. When configured correctly, TLS provides both privacy and data integrity for communications between the client and the server. TLS connections can either be client initiated or server initiated.Client Initiated Encryption

*   Generate certificate (/CN should match your SQL Server host fully qualified domain name)

Bashopenssl req -x509 -nodes -newkey rsa:2048 -subj '/CN=mssql.contoso.com' -keyout mssql.key -out mssql.pem -days 365sudo chown mssql:mssql mssql.pem mssql.keysudo chmod 600 mssql.pem mssql.key  sudo mv mssql.pem /etc/ssl/certs/sudo mv mssql.key /etc/ssl/private/

*   Configure SQL Server

Bashsystemctl stop mssql-servercat /var/opt/mssql/mssql.confsudo /opt/mssql/bin/mssql-conf set network.tlscert /etc/ssl/certs/mssql.pemsudo /opt/mssql/bin/mssql-conf set network.tlskey /etc/ssl/private/mssql.keysudo /opt/mssql/bin/mssql-conf set network.tlsprotocols 1.2sudo /opt/mssql/bin/mssql-conf set network.forceencryption 0

*   Register the certificate on your client machine (Windows, Linux, or macOS)
    *   If you are using CA signed certificate, you have to copy the Certificate Authority (CA) certificate instead of the user certificate to the client machine.
    *   If you are using the self-signed certificate, just copy the .pem file to the following folders respective to distribution and execute the commands to enable them
        *   Ubuntu: Copy cert to /usr/share/ca-certificates/, rename its extension to .crt, and use dpkg-reconfigure ca-certificates to enable it as system CA certificate.
        *   RHEL: Copy cert to /etc/pki/ca-trust/source/anchors/ and use update-ca-trust to enable it as system CA certificate.
        *   SUSE: Copy cert to /usr/share/pki/trust/anchors/ and use update-ca-certificates to enable it as system CA certificate.
        *   Windows: Import the .pem file as a certificate under current user -> trusted root certification authorities -> certificates
        *   macOS:
            *   Copy the cert to /usr/local/etc/openssl/certs
            *   Run the following command to get the hash value: /usr/local/Cellar/openssl/1.0.2l/openssl x509 -hash -in mssql.pem -noout
            *   Rename the cert to value. For example: mv mssql.pem dc2dd900.0\. Make sure dc2dd900.0 is in /usr/local/etc/openssl/certs
*   Example connection strings
    *   SQL Server Management Studio

![SSMS connection dialog](Image00050.jpg)   

*   SQLCMD

sqlcmd -S <sqlhostname> -N -U sa -P '<YourPassword>'

*   ADO.NET

"Encrypt=True; TrustServerCertificate=False;"

*   ODBC

"Encrypt=Yes; TrustServerCertificate=no;"

*   JDBC

"encrypt=true; trustServerCertificate=false;"Server Initiated Encryption

*   Generate certificate (/CN should match your SQL Server host fully-qualified domain name)

Bashopenssl req -x509 -nodes -newkey rsa:2048 -subj '/CN=mssql.contoso.com' -keyout mssql.key -out mssql.pem -days 365sudo chown mssql:mssql mssql.pem mssql.keysudo chmod 600 mssql.pem mssql.key  sudo mv mssql.pem /etc/ssl/certs/sudo mv mssql.key /etc/ssl/private/

*   Configure SQL Server

Bashsystemctl stop mssql-servercat /var/opt/mssql/mssql.confsudo /opt/mssql/bin/mssql-conf set network.tlscert /etc/ssl/certs/mssql.pemsudo /opt/mssql/bin/mssql-conf set network.tlskey /etc/ssl/private/mssql.keysudo /opt/mssql/bin/mssql-conf set network.tlsprotocols 1.2sudo /opt/mssql/bin/mssql-conf set network.forceencryption 1

*   Example connection strings
    *   SQLCMD

sqlcmd -S <sqlhostname> -U sa -P '<YourPassword>'

*   ADO.NET

"Encrypt=False; TrustServerCertificate=False;"

*   ODBC

"Encrypt=no; TrustServerCertificate=no;"

*   JDBC

"encrypt=false; trustServerCertificate=false;"Common connection errors

| COMMON CONNECTION ERRORS |
| --- |
| Error message | Fix |
| --- | --- |
| The certificate chain was issued by an authority that is not trusted. | This error occurs when clients are unable to verify the signature on the certificate presented by SQL Server during the TLS handshake. Make sure the client trusts either the SQL Server certificate directly, or the CA which signed the SQL Server certificate. |
| The target principal name is incorrect. | Make sure that Common Name field on SQL Server's certificate matches the server name specified in the client's connection string. |
| An existing connection was forcibly closed by the remote host. | This error can occur when the client doesn't support the TLS protocol version required by SQL Server. For example, if SQL Server is configured to require TLS 1.2, make sure your clients also support the TLS 1.2 protocol. |
|  |  |