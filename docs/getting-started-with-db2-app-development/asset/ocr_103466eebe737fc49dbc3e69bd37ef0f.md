```
$sth->closeCursor();
} catch (PDOException $exp) {
    echo 'Exception: ' . $exp->getMessage();
}
?>
```

# Listing 8.18—Exception handling using PDO::ERRMODE_EXCEPTION

When the exception is generated, the getMessage() method produces an output that looks like this:

```
Exception : SQLSTATE[42S22]: Column not found: -206 [IBM][CLI
Driver][DB2/LINUX] SQL0206N "NONEXISTINGCOL" is not valid in the context
where it is used. SQLSTATE=42703 (SQLExecute[-206] at /root/Desktop/php-
5.1.2/ext/pdo_odbc/odbc_stmt.c:133)
```

The methods called **errorCode()** and **errorInfo()** could be used to get more information about the error:
PDO::errorCode() gives the information about the SQLSTATE of the error.
PDO::errorInfo() gives all the information about the error, such as SQLSTATE, SQLCODE, and error message from the database server.

# 8.3.3.3.3 Isolation level to use

Considerations of which isolation level to use in PHP with PDO_IBM/PDO_ODBC are the same as the ones described for the ibm_db2 extension earlier.

# 8.3.3.3.4 Preparing and executing SQL statements

PDO provides mechanisms by which you can prepare and execute SQL statements in a single step, and also in separate steps.

# Preparing and executing SQL statements in a single step

Normally, we use this method for execution of SQL statements which are not executed repeatedly in the same program. We have two kinds of SQL statements:

+   * SQL statements returning result sets

The function PDO::query is used for preparing and executing the SQL statement which returns a result set indexed by both column position and column name. Listing 8.19 is an example for the query function. You see that each row in the result set returned by the query is fetched into an array named $row and the value is printed.

```
<?php
/* Use one of the following connection string */
/* The connection below is for pdo_ibm */
```