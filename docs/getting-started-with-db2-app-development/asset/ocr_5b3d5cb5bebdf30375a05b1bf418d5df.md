an embedded SQL C/C++ application is that an ODBC application can run against a variety of databases from different vendors without having to compile the code against each of these databases. To run a compiled ODBC/CLI application, you only need to install the ODBC/CLI driver that the vendor provides on the machine where you are running the application, and their client. Applications use procedure calls at run time to connect to databases, issue SQL statements, and retrieve data and status information.

# 5.5.1 Additional environment setup for CLI/ODBC applications

In addition to what was discussed in section 5.2, for an ODBC/CLI application to access a DB2 database you also need to follow these steps:

# 5.5.1.1 Linux

+   1. Install an ODBC driver manager.
+   2. Register the DB2 database as an ODBC data source in the `.odbc.ini` file. For example, to register the SAMPLE database, the `.odbc.ini` file must contain the following line  
+   `SAMPLE=IBM DB2 ODBC DRIVER`
+   3. Set the `LD_LIBRARY_PATH` environment variable to `libodbc.so`.
+   4. Set the `ODBCINI` environment variable as follows:  
+   `ODBCINI=/opt/odbc/system_odbc.ini; export ODBCINI`

# 5.5.1.2 Windows

+   1. Make sure that the Microsoft ODBC Driver Manager and the DB2 CLI/ODBC driver are installed. To verify that both exist on the machine follow the steps below:
+   
+   - Double click on the Microsoft ODBC Data Sources icon in the Control Panel, or run the `odbcad32.exe` command from the command line.
+   
+   - Click on the Drivers tab and check IBM DB2 ODBC DRIVER - `<DB2_Copy_Name>` is shown in the list. *Figure 5.24* shows the output. If ODBC Driver Manager or the IBM DB2 CLI/ODBC driver is not in the list, you need to download the IBM Data Server driver for ODBC and CLI from [http://www-01.ibm.com/support/docview.wss?rs=4020&uid=swg2i385217](http://www-01.ibm.com/support/docview.wss?rs=4020&uid=swg2i385217) and install it by copying the `clidriver` folder to `<DB2 install directory>\sqllib`