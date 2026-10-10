```
SQLSMALLINT AuthenticationLength); /* cbAuthStr */
```

# Listing 5.16 – Syntax of SQLConnect function

```
/* allocate a database connection handle */
(1) rc = SQLAllocHandle(SQL_HANDLE_DBC, *pHenv, pHdbc);
if (rc != SQL_SUCCESS)
{
	printf("\n\nERROR while allocating connection handle.\n");
	funcRc = 1;
	exit (1);
}
printf("\n\nAllocate Connection handle successfully.");

/* connect to the database */
(2) rc = SQLConnect (*pRdbc, (SQLCHAR *)dbAlias, SQL_NTS,(SQLCHAR *)user,SQL_NTS,(SQLCHAR *)pswd, SQL_NTS);
if (rc != SQL_SUCCESS)
{
	printf("\n\nERROR while connecting to database.\n");
	funcRc = 1;
	exit (1);
}
printf("\n\nConnected to %s database successfully\n", dbAlias);
```

# Listing 5.17 – Allocate connection handle and connect to the database

In the above listing:

+   1.  This statement allocates the connection handle using SQLAllocHandle function.
+   2.  This statement connects to the database using SQLConnect. Database name will be passed as an argument.

If you would like to test the above code snippet, copy the **AppInit** function from `cli_odbc.c` program (accompanying this book) and change the userid, and password in the program. The program includes the handle allocation and connection statements shown in *Listing 5.15* and *Listing 5.17*. *Figure 5.28* provides the output of above code snippet of *Listing 5.15* and *5.17*.