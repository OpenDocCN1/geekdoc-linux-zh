```
)
/* End of error handling */
```

```
(4) /* Execute SQL statements
EXECSQL SELECT <coll>, <col2> INTO :varl :var2
FROM <table name> WHERE <condition> ;
/* Error handling to check SQL statement executed successfully */
```

```
(5)
if (SQLCODE < 0)
{
printf ("\n Error while executing SQL statement");
printf ("\n Returned SQLCODE = ");
exit;
}
```

```
(6) /* Commit the transaction */
EXECSQL COMMIT;
/* Error handling to check SQL statement executed successfully */
if (SQLCODE < 0)
{
printf ("\n Error while Committing data");
printf ("\n Returned SQLCODE = ");
exit;
}
```

```
(7) /* Disconnect from the database */
EXECSQL DISCONNECT FROM <database name>;
```

```
/* Error handling to check whether disconnection is successful */
if (SQLCODE < 0)
{
printf ("\n Error while disconnecting from database");
printf ("\n Returned SQLCODE = ");
exit;
}
else
{
printf ("\n Disconnect from database successfully");
}
)
```

**Listing 5.1 – Embedded SQL C program template**

Each of the items numbered in *Listing 5.1* are discussed in detail in the following subsections.