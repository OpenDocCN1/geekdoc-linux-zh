
## Listing 5.24 — Disconnecting from the database

In the above listing:

- 1. Disconnect from the database using **SQLDisconnect** API. Pass connection handle variable as an argument.
```c
/* disconnect from the database */
(1) rc = SQLDisconnect(*pHdbc);
(2) if (rc != SQL_SUCCESS)
{
    printf("\n\nERROR while disconnecting from database.\n");
    funcRc = 1;
    exit(1);
}
printf("\n\nDisconnect from %s database successfully.", dbAlias);
```
- 2. Check whether the disconnection was successful.

### 5.5.3.6 Freeing the handles

The last step in a CLI application is to free all the allocated handles. To free the allocated handles, DB2 CLI provides the **SQLFreeHandle** API which takes the handle type and the handle variable as arguments. Before calling **SQLFreeHandle**() an application must call **SQLDisconnect**(). Calling **SQLFreeHandle**() before the **SQLDisconnect**() returns SQL_ERROR and the connection remains valid. *Listing 5.25* shows how to free the handles.

## Listing 5.25 – Free allocated environment and connection handles

In the above listing:

- 1. Frees allocated connection handle using `SQLFreeHandle`.
```c
/* free connection handle */
(1) rc = SQLFreeHandle(SQL_HANDLE_DBC, *pHdbc);
    if (rc != SQL_SUCCESS)
    {
        printf("\n\nERROR while freeing connection handle.\n");
        funcRc = 1;
        exit(1);
    }
    printf("\n\nFree connection handle successfully.");

/* free environment handle */
(2) rc = SQLFreeHandle(SQL_HANDLE_ENV, *pHenv);
    if (rc != SQL_SUCCESS)
    {
        printf("\n\nERROR while freeing environment handle.\n");
        funcRc = 1;
        exit(1);
    }
    printf("\n\nFree environment handle successfully.\n");
```
- 2. Frees allocated environment handle using `SQLFreeHandle`.

*Figure 5.33* shows the output of the above code snippets in *Listing 5.24* and *5.25*.

![](img/5f6ba170efa3a607142589708531bef8_211_0.png)

**Figure 5.33** - Freeing allocated handles

> **Note:**
> All the code snippets shown in this section are extracted from the program `cli_odbc.c` which is included in the `Exercise_Files_DB2_Application_Development.zip` file with this book. Before building the application ensure to change the userid and password at lines # 52 and 53 in the program.

## 5.5.4 Building ODBC/CLI applications

You can build ODBC/CLI application either manually from the command line or by using the DB2 provided scripts.

### 5.5.4.1 Building an ODBC or CLI application from the command line

Building ODBC application from the command line involves the following steps:

1) Compile the application on windows using below command

```c
cl -Zi -Od -cC -W2 -DWIN32 cli_odbc.c
```

*Figure 5.34* shows the output of above command

![](img/5f6ba170efa3a607142589708531bef8_212_0.png)

**Figure 5.34 – Compile application**

2) Link the application with the CLI library (db2cli.lib) for a CLI application or the odbc library (odbc32.lib) for an ODBC application. For example, the command below would create the CLI application cli_odbc:

```
link -debug -out:cli_odbc.exe cli_odbc.obj db2cli.lib db2api.lib
```

Figure 5.35 shows the output of the above command

![](img/5f6ba170efa3a607142589708531bef8_212_1.png)

**Figure 5.35 – Linking the application with the CLI library**

On the other hand this command would create an ODBC application:

```
link -debug -out:cli_odbc.exe cli_odbc.obj odbc32.lib
```

Figure 5.36 shows the output of the above command:

![](img/5f6ba170efa3a607142589708531bef8_212_2.png)

**Figure 5.36 – Link the application with the ODBC library**

You can run the executable file by entering the executable name cli_odbc.

### 5.5.4.2 Building an ODBC or CLI application using the sample build script

To build an application using the sample script bldapp that comes with DB2, follow the same recommendations provided earlier in section 5.4.2. By default bldapp script uses db2cli.lib library to build CLI applications. If you want to build ODBC applications using bldapp replace db2cli.lib with odbc32.lib in the script.

To build the sample program cli_odbc described earlier, enter:

```
bldapp cli_odbc
```

The result is an executable file, `cli_odbc`. You can run the executable file by entering the executable name:

```
cli_odbc
```

## 5.6 Working with XML in C/C++ applications with DB2

As discussed in *Chapter 2, DB2 pureXML*, DB2 provides the XML data type to store XML data natively. To exchange XML data between the database server and an embedded SQL C/C++ application, you need to declare host variables in your application source code. Columns with the XML data type are described as an SQL_TYP_XML column SQLTYPE. XML columns can be accessed directly using SQL, XQuery or SQL/XML.

Sample program `xmlinsert.sqc`, `xmlread.sqc` demonstrates different ways to insert and read the data from an XML column. You can find these sample programs under `<DB2 install path>/samples/xml/c` directory.

## 5.7 Exercises

- 1. Write a program to read database log files asynchronously with a database connection
    - Solution: To review the solution check the `dblogconn.sqc` sample under `<DB2 install path>/samples/c` directory
- 2. Write a program to read and write LOB data
    - Solution: To review the solution check the `dtlob.sqc` sample under `<DB2 install path>/samples/c` directory
- 3. Write a program to use a trigger on a table.
    - Solution: To review the solution check the `btrig.sqc` sample under `<DB2 install path>/samples/c` directory
- 4. Write a program to insert data using the CLI LOAD utility
    - Solution: To review the solution check the `tload.c` sample under `<DB2 install path>/samples/cli` directory

## 5.8 Summary

In this chapter you learned the basics of developing C/C++ applications with DB2. The chapter showed you how to set up the environment for building C/C++ applications and how to connect to a DB2 database and issue different kinds of SQL statements using an embedded SQL application and also a CLI/ODBC application. CLI/ODBC applications use procedure calls at run time to connect to databases, issue SQL statements, and retrieve data and status information.

## 5.9 Review questions

1. What is the difference between an embedded SQL C/C++ application and a CLI/ODBC application?

2. What is a cursor?

3. What is a parameter marker?

4. What are handles?

5. What are different return codes returned by CLI APIs?

6. What is the file extension of an embedded SQL C++ program on Windows?
    A. .sqc
    B. .c
    C. .sqs
    D. .sqC
    E. None of the above

7. What is the command that can dump the SQL statements from a bind file?
    A. db2bffd -b
    B. db2bffd -s
    C. db2bffd -h
    D. db2bffd -v
    E. None of the above

8. What is the command to list current data sources?
    A. db2 list odbc data sources
    B. db2 system odbc data sources
    C. db2 list system odbc data sources
    D. db2 system odbc data source
    E. None of the above

9. Which of the following API is used for allocating all the handles?
    A. SQLAllocHandle ( )
    B. SQLAllocConnect()
    C. SQLAllocEnv()
    D. SQLAllocStmt()
    E. None of the above

10. Which of the following shows the correct flow of handle allocations in CLI application?
    
    A. Allocate environment handle -> allocate connection handle -> allocate statement handle -> free statement handle-> free connection handle -> free environment handle
    
    B. Allocate connection handle -> allocate environment handle -> allocate statement handle -> free statement handle-> free environment handle -> free connection handle
    
    C. Allocate connection handle -> allocate environment handle -> free environment handle -> free connection handle
    
    D. Allocate environment handle -> allocate statement handle -> free statement handle -> free environment handle
    
    E. None of the above
