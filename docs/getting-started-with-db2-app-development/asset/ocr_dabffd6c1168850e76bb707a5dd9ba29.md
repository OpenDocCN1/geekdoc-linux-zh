```
(1) EXEC SQL CONNECT TO sample; /* Database name is SAMPLE*/
(2) if (SQLCODE < 0)
{
    printf ("\n ERROR WHILE DATABASE CONNECTION\n");
    printf ("\n SQLCODE = %d", SQLCODE);
    rc = 1;
    exit (1);
}
else
{
    printf ("\n CONNECT TO DATABASE SUCCESSFULLY\n");
}
```

# Listing 5.4 – Connect to the database

Let’s review each of the items shown in *Listing 5.4*:

+   1. This statement establishes the connection to the **sample** database.
+   2. This statement checks if the connection is successful or not. SQLCODE is a special variable in DB2 that is set after a statement is executed. When SQLCODE is less than zero, the statement completed with an error. If SQLCODE is equal to zero, the statement completed successfully; and if it was greater than zero, the statement completed with a warning.

*Figure 5.9* provides the output of above code snippet.

![](bbox=[0.17, 0.52, 0.85, 0.61])

# Figure 5.9 – Output of the connect statement

If you include the **utilemb.h** header file, you can also use the **Dbconn** utility function that comes with DB2 sample programs to connect to the database. *Listing 5.5* shows how to use Dbconn utility function.

```
(1) rc = DbConn(dbAlias, user, pwd);
(2) if (rc != 0)
{
    printf("\n Error while connecting to database");
    return rc;
})
```

# Listing 5.5 – Connect to the database using DbConn utility function

Let’s review each of the items shown in *Listing 5.5*: