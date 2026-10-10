A C/C++ application works in a client-server architecture where the C/C++ application works as the client and DB2 as the server. The client sends the request to the server and the server performs the operation. A C/C++ application can be an embedded SQL application or a CLI/ODBC application. *Figure 5.2* illustrates the client-server architecture where a C/C++ application interacts with a DB2 server.

![](bbox=[0.15, 0.23, 0.85, 0.41])

# **Figure 5.2 – C/C++ application accessing a DB2 server**

*Figure 5.2* shows how C/C++ applications are built and can access a DB2 database. Embedded SQL applications containing SQL statements must be precompiled by a DB2 precompiler. To facilitate this preprocessing, each SQL statement embedded in an application must be prefixed with the keywords EXEC SQL and terminated with a semicolon (;).

On the other hand CLI or ODBC is an alternative to embedded dynamic SQL, but unlike embedded SQL, it does not require host variables or a precompiler. Applications can be run against a variety of databases from different vendors which would provide their own ODBC drivers. There is no need for the application to be compiled against each of these databases. Processing of ODBC/CLI applications is handled by the ODBC/CLI driver. Applications use procedure calls at run time to connect to databases, issue SQL statements, and retrieve data and status information.

We will discuss each of the above methods in more detail in the coming sections.

# 5.2 Setting up the environment

Before you start building an embedded SQL C/C++ application or an ODBC/CLI application, you need to install a supported C/C++ compiler. For embedded SQL C/C++ programs, you also need a precompiler; fortunately, this is included with DB2.

# 5.2.1 Supported compilers

*Table 5.1* lists C/C++ compilers that are supported for DB2 database application development on both, 32-bit and 64-bit platforms.