
an embedded SQL C/C++ application is that an ODBC application can run against a variety of databases from different vendors without having to compile the code against each of these databases. To run a compiled ODBC/CLI application, you only need to install the ODBC/CLI driver that the vendor provides on the machine where you are running the application, and their client. Applications use procedure calls at run time to connect to databases, issue SQL statements, and retrieve data and status information.

## 5.5.1 Additional environment setup for CLI/ODBC applications

In addition to what was discussed in section 5.2, for an ODBC/CLI application to access a DB2 database you also need to follow these steps:

### 5.5.1.1 Linux

- Install an ODBC driver manager.
- Register the DB2 database as an ODBC data source in the `.odbc.ini` file. For example, to register the SAMPLE database, the `.odbc.ini` file must contain the following line
  `SAMPLE=IBM DB2 ODBC DRIVER`
- Set the `LD_LIBRARY_PATH` environment variable to `libodbc.so`.
- Set the `ODBCINI` environment variable as follows:
  `ODBCINI=/opt/odbc/system_odbc.ini; export ODBCINI`

### 5.5.1.2 Windows

- Make sure that the Microsoft ODBC Driver Manager and the DB2 CLI/ODBC driver are installed. To verify that both exist on the machine follow the steps below:
  - Double click on the Microsoft ODBC Data Sources icon in the Control Panel, or run the `odbcad32.exe` command from the command line.
  - Click on the Drivers tab and check IBM DB2 ODBC DRIVER - `<DB2_Copy_Name>` is shown in the list. *Figure 5.24* shows the output. If ODBC Driver Manager or the IBM DB2 CLI/ODBC driver is not in the list, you need to download the IBM Data Server driver for ODBC and CLI from [http://www-01.ibm.com/support/docview.wss?rs=4020&uid=swg2i385217](http://www-01.ibm.com/support/docview.wss?rs=4020&uid=swg2i385217) and install it by copying the `clidriver` folder to `<DB2 install directory>\sqllib`

![](img/5f6ba170efa3a607142589708531bef8_192_0.png)

**Figure 5.24 – Add ODBC data source**

- The next step is to configure the ODBC Data Source. Follow below steps to set up the Data Source.
  - In the ODBC Data Source Administrator panel (as shown in Figure 5.24 above), click on the System DSN tab.
  - Click on Add, select IBM DB2 ODBC driver and click finish to create new data source.
  - In the window that pops up, enter any name for the data source name, in this example we will use sample, then choose the database SAMPLE and click on add button to register this database.
- You can also check if the DB2 database is registered by listing your current data sources with the following command from the DB2 command window or Linux shell:

```bash
db2 list system odbc data sources
```

Figure 5.25 shows the output of above command. You can see the data source SAMPLE is added in the list.

![](img/5f6ba170efa3a607142589708531bef8_193_0.png)

**Figure 5.25 – Add ODBC data source**

- An alternative to using the ODBC Data Source Administrator is to register the database using the command below:

```bash
db2 catalog system odbc data source sample
```

## 5.5.2 Handles

An ODBC/CLI handle is a variable that refers to a data object allocated and managed by ODBC/CLI. In simpler terms, a handle is a pointer to a variable which is used for passing references to the variable between parts of the program. There are four types of handles in ODBC/CLI:

- **Environment handle (SQL_HANDLE_ENV)**
  An environment handle refers to an object that holds information about the global state of the application, attributes or connections. An environment handle must be allocated before a connection handle can be allocated.

- **Connection handle (SQL_HANDLE_DBC)**
  A connection handle refers to an object that holds information about the connection to a particular database. For each database, a separate connection handle must be allocated. A connection handle must be allocated before a statement handle can be allocated.

- **Statement handle (SQL_HANDLE_STMT)**
  A statement handle refers to an object that holds information about the execution of a single SQL statement. Before the execution of a SQL statement, a statement handle must be allocated and associated with a connection handle.

- **Descriptor handle (SQL_HANDLE_DESC)**
  A descriptor handle refers to an object that contains information about the columns in a result set and dynamic parameters in an SQL statement.

*Figure 5.26 taken from the IBM redbook DB2 Express-C: The Developer Handbook for XML, PHP, C/C++, Java, and .NET [5] illustrates the relationship between the different handles.*

![](img/5f6ba170efa3a607142589708531bef8_194_0.png)

**Figure 5.26 – CLI Handles**

## 5.5.3 Steps to develop an ODBC/CLI application

Figure 5.27 shows the steps required to develop an ODBC/CLI application.

![](img/5f6ba170efa3a607142589708531bef8_194_1.png)

**Figure 5.27 – Steps required in an ODBC/CLI application**

The steps shown in *Figure 5.27* are described in more detail in the following sections.

### 5.5.3.1 Include header files

To start application development with CLI, you need to include `sqlecli.h` header file which contains CLI constants, function prototypes, data structures required for developing CLI application. Listing 5.13 lists the header files required for a CLI/ODBC application.

```c
/* Include header files */
#include <stdio.h>
#include <string.h>
#include <stdlib.h>
#include <sqlecli.h>
```
*Listing 5.13 - Header files required for CLI application*

### 5.5.3.2 Allocate environment handle

Allocation of different handles can be done using `SQLAllocHandle` API. `SQLAllocHandle()` is a generic function that allocates environment, connection, statement, or descriptor handles.

> **Note:**
> This function replaces the deprecated functions `SQLAllocConnect()`, `SQLAllocEnv()`, and `SQLAllocStmt()`. For a complete list of CLI and ODBC functions, review this link http://public.boulder.ibm.com/infocenter/db2luw/v9r7/topic/com.ibm.db2.luw.apdv.cli.doc/doc/r0000553.html

Listing 5.14 shows the syntax of `SQLAllocHandle` API

```c
SQLRETURN SQLAllocHandle(
             SQLSMALLINT    HandleType,
             SQLHANDLE      InputHandle,
             SQLHANDLE      *OutputHandlePtr);
```
*Listing 5.14 - Syntax of `SQLAllocHandle` function*

Function `SQLAllocHandle` takes as arguments the type of handle (environment, connection, statement, or descriptor), the input handle and the output handle. To allocate an environment handle the value of `HandleType` must be `SQL_HANDLE_ENV`. If the handle type is `SQL_HANDLE_ENV` the value of `InputHandle` will be `SQL_NULL_HANDLE`. `OutputHandlePtr` will be a pointer to a buffer in which to return the handle to the newly allocated data structure. After the handle is allocated, `SQLAllocHandle` returns any one of the following return codes, which are self-explanatory:

- `SQL_SUCCESS`
- `SQL_SUCCESS_WITH_INFO`
- `SQL_INVALID_HANDLE`
- `SQL_ERROR`

Let's take a look at an example. *Listing 5.15* shows the allocation of an environment handle.

```c
/* allocate an environment handle */
(1) rc = SQLAllocHandle(SQL_HANDLE_ENV, SQL_NULL_HANDLE, pHenv);
(2) if (rc != SQL_SUCCESS)
    {
        printf("\n\nERROR while allocating environment handle.\n");
        funcRc = 1;
        exit (1);
    }
    printf("\n\nAllocate environment handle successfully.");
```
*Listing 5.15 – Allocate Environment handle using SQLAllocHandle function*

In the above listing:

- 1. This statement allocates the environment handle using `SQLAllocHandle` API and returns the pointer to `pHenv`.
- 2. This statement checks whether allocation is successful or not.

### 5.5.3.3 Connect to the database

After the successful allocation of the environment handle, the next step is to connect to the database using `SQLConnect()` . Before connecting to the database you need to allocate a connection handle. Allocation of a connection handle can be done by the `SQLAllocHandle` API using `SQL_HANDLE_DBC` as the type of handle. The value of `InputHandle` will be the pointer to the environment handle variable. *Listing 5.16* shows the syntax of `SQLConnect` , and *Listing 5.17* provides an example of allocating a connection handle using `SQLAllocHandle` and connecting to a database using `SQLConnect` .

```c
SQLRETURN SQLConnect ( ConnectionHandle, /* hdbc */
                    SQLCHAR *ServerName, /* szDSN */
                    SQLSMALLINT ServerNameLength,
                    SQLCHAR *UserName, /* szUID */
                    SQLSMALLINT UserNameLength,
                    SQLCHAR *Authentication, /* szAuthStr */
                    SQLSMALLINT AuthLength,
                    SQLCHAR *Output = NULL,
                    SQLSMALLINT *OutputLength = NULL);
```
*Listing 5.16 – Syntax of `SQLConnect` function*

```c
(1) rc = SQLAllocHandle(SQL_HANDLE_DBC, pHenv, &pHdbc);
(2) rc = SQLConnect(pHdbc, "SAMPLE", SQL_NTS, "user", SQL_NTS, "password", SQL_NTS);
(3) if (rc != SQL_SUCCESS && rc != SQL_SUCCESS_WITH_INFO)
    {
        printf("\n\nERROR while connecting to database.\n");
        funcRc = 1;
        exit (1);
    }
    printf("\n\nConnect to database successfully.");
```
*Listing 5.17 – Allocate connection handle and connect to database*

In the above listing:

- 1. This statement allocates the connection handle using `SQLAllocHandle` API and returns the pointer to `pHdbc`.
- 2. This statement connects to the database using `SQLConnect` API.
- 3. This statement checks whether connection is successful or not.

