*Listing 6.2* shows the C# code snippet to connect to a database using the OLE DB .NET Data Provider

```
OleDbConnection con = new OleDbConnection("Provider=IBMADDB2;" +
"Data Source=sample;UID=userID;PWD=password;") ;
con.Open()
```

**Listing 6.2 - C# code snippet to connect to a database using the OLE DB .NET Data Provider**

*Listing 6.3* shows the C# code snippet to connect to a database using the ODBC.NET Data Provider

```
OdbcConnection con = new
OdbcConnection ("DSN=sample;UID=userID;PWD=password;") ;
con.Open()
```

**Listing 6.3 - C# code snippet to connect to a database using the ODBC.NET Data Provider**

The code samples can be compiled using the following command:

```
csc NETSamp.cs /r:<DB2 Install Path>\bin\netf20\IBM.Data.DB2.dll
```

where *<DB2 Install Path>* is the path where DB2 is installed.

In C#, all errors are treated as instances of an exception. Error handling in ADO.NET is performed using a *try/catch/finally* block or using the **On Error** construct.

# ## 6.3 Setting up the environment

The set up required to start developing .NET applications to access DB2 is fairly straight forward. You only need to install either a DB2 client, or a DB2 server which include a .NET data provider. *Table 6.1* shows the the .NET data providers that are shipped with DB2 Version 9.7 clients and servers, and their 32-bit and 64-bit support levels.

| .Net data provider framework | 32-bit support | 64-bit support |
|---|---|---|
| IBM Data Server Provider for .NET Framework Version 1.1 | Yes | No |
| IBM Data Server Provider for .NET Framework Version 2.0, Version 3.0, and Version 3.5 | Yes | Yes |


**Table 6.1 - 32-bit and 64-bit support in IBM Data Server data providers for .NET**

During the installation of the DB2 client or server software, one of these two IBM Data Server Providers for .NET editions will be installed:

+   - For Windows on 32-bit AMD and Intel systems (x86)