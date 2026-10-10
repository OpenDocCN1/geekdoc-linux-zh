From the above figure, you can see the IBM Data Server Runtime client has all the components you need (driver and network support) to connect and work with a DB2 Data Server. The IBM Data Server client has this same support and also includes GUI Tools and libraries for application development.

In addition to these clients, provided are these other clients and drivers:

+   - DB2 Runtime Client Merge Modules for Windows: mainly used to embed a DB2
+   runtime client as part of a Windows application installation
+   - IBM Data Server Driver for JDBC and SQLJ: allows Java applications to connect to
+   DB2 servers without having to install a client
+   - IBM Data Server Driver for ODBC and CLI: allows ODBC and CLI applications to
+   connect to a DB2 server without having to install a client
+   - IBM Data Server Driver Package: includes a Windows-specific driver with support
+   for .NET environments in addition to ODBC, CLI and open source. This driver was
+   previously known as the IBM Data Server Driver for ODBC, CLI and .NET.

There is no charge to use DB2 clients or drivers.

# ## B.3 Installing DB2

In this section we explain how to install DB2 using the DB2 setup wizard.

# ### B.3.1 Installation on Windows

DB2 installation on Windows is straight-forward and requires the following basic steps:

+   1. Ensure you are using a local or domain user that is part of the Administrator group
+   on the server where you are installing DB2.
+   2. After downloading and unzipping DB2 Express-C for Windows from
+   ibm.com/db2/express, look for the file setup.exe, and double-click on it.
+   3. Follow the self- explanatory instructions from the wizard. Choosing default values is
+   normally sufficient.
+   4. The following is performed by default during the installation:
+   
+   - DB2 is installed in `C:\Program Files\IBM\SQLLIB`
+   - The **DB2ADMNS** and **DB2USERS** Windows operating system groups are
+   created.
+   - The instance **DB2** is created under `C:\Program Files\IBM\SQLLIB\DB2`
+   - The DB2 Administration Server (DAS) is created
+   - Installation logs are stored in:
+   
+   `My Documents\DB2LOG\db2.log`
+   `My Documents\DB2LOG\db2wi.log`