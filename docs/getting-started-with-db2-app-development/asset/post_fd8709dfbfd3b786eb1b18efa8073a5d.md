
| Name | Description |
|---|---|
| **connection** | A valid database connection object as returned from `ibm_db.connect()` |
| **Statement** | An SQL statement in string format. The statement cannot contain any parameter markers, i.e the statement should be known at the time it is written. |
| **options** | Optional: A dictionary containing statement options. You can use this parameter to request a scrollable cursor for database servers that support this type of cursor. By default, a forward-only cursor is returned. |

## Table 10.2 - Parameters for function ibm_db.exec_immediate

For example, you can call `ibm_db.exec_immediate` function to run a SELECT statement passed in as a string argument as shown below:

```
stmt = ibm_db.exec_immediate(conn, 'SELECT firstname, lastname FROM
employee fetch first 2 rows only')
```

Where the function takes the connection object `conn` returned in step 1 as the first function argument, and returns a statement object `stmt` which is associated with the query's result set if the execution is successful.

3. Fetch rows from the result set by calling `ibm_db.fetch_tuple()`, which returns a tuple representing the next or requested row in the result set. Each column value is indexed by the 0-indexed column position in the tuple.

The syntax of function `ibm_db.fetch_tuple` is shown as follows:

```
array ibm_db.fetch_tuple(IBM_DBStatement stmt, [, int row_number])
```

Table 10.3 explains the different parameters of `ibm_db.fetch_tuple`

| Name | Description |
|---|---|
| **Stmt** | A valid statement object containing a result set. |
| **row_number** | Optional: 1-indexed row number for a specific row that you want to fetch from the result set. Passing this parameter results in a warning if the result set uses a forward-only cursor |

## Table 10.3 - Parameters for function ibm_db.fetch_tuple

The function returns `False` if there are no more rows left in the result set, or if the row requested by `row_number` does not exist in the result set.

For example, you can fetch and print all the rows from the result set as shown in Listing 10.6.

```
(1) mytuple = ibm_db.fetch_tuple(stmt)
(2) while mytuple != False:
    (3) print "First Name: %s, Last Name: %s" % (mytuple[0], mytuple[1])
    (4) mytuple = ibm_db.fetch_tuple (stmt)
```

### Listing 10.6 – Fetch rows from the result set

Items in *Listing 10.6* are explained as follows:

- (1) The function **ibm_db.fetch_tuple** returns each row from the result set as a tuple and assigns it to the variable *mytuple*;
- (2) Loop until the function returns **False** if there are no rows left in the result set;
- (3) Print each columns' value from the returned row by using the 0-indexed column position, such as *mytuple[0], mytuple[1]*;
- (4) Fetch the next row into the variable *mytuple*.

> **Note:**
> 
> In addition to **ibm_db.fetch_tuple**, the ibm_db driver also provides 3 other data fetching functions that support flexible ways of fetching result sets: **ibm_db.fetch_assoc**, **ibm_db.fetch_both** and **ibm_db.fetch_row**. For more information review [http://code.google.com/p/ibm-db/wiki/APIs](http://code.google.com/p/ibm-db/wiki/APIs).

If you would like to test all the above code snippets, edit the Python script `select.py` included in the exercise files accompanying this book and replace the user ID and password with your own. Then run the script as follows:

```
python select.py
```

The result of executing the above script is illustrated in *Figure 10.5*.

![](img/5f6ba170efa3a607142589708531bef8_349_0.png)

Figure 10.5 Executing the script select.py

> **Note:**
> 
> All the scripts used in this chapter are included in the directory *samples/chapter10* in the zip file *Exercise_Files_DB2_Application_Development.zip* that accompanies this book.
> To run the scripts, you may need to first create the *SAMPLE* database using the *db2samp1* utility. Also replace the user name and password in the scripts with your own ones.

## 10.3.3 Inserting, updating and deleting data

Similar to the **SELECT** statement, an **INSERT**, **UPDATE** or **DELETE** SQL statement that is already known at the time the application is written can be executed directly by calling the function `ibm_db.exec_immediate`. For a SQL statement that contains variable inputs or parameter markers, refer to section **10.3.4**.

After successful execution of the SQL statements, you can use the `ibm_db.num_rows` function to return the number of rows that the SQL statement affected.

Let's take a look at the example in **Listing 10.7**.

```
(1) stmt = ibm_db.exec_immediate (conn, "CREATE TABLE PRODUCT(product_id char(6), name char(30))")
(2) stmt = ibm_db.exec_immediate (conn, "Insert into PRODUCT values ('000001','Computer'), ('000002','TV')")
(3) print "Returns for insert: ", ibm_db.num_rows(stmt)
(4) stmt = ibm_db.exec_immediate (conn, "update PRODUCT set name = 'notebook' where product_id='000001'")
(5) print "Returns for update: ", ibm_db.num_rows(stmt)
(6) stmt = ibm_db.exec_immediate (conn, "delete from PRODUCT where product_id='000003'")
(7) print "Returns for delete: ", ibm_db.num_rows(stmt)
(8) stmt = ibm_db.exec_immediate (conn, "drop table PRODUCT")
```

### Listing 10.7 - the script ins_upd_del.py

Items in **Listing 10.7** are explained as follows:

- 1. Calls the function `ibm_db.exec_immediate` to create the table **PRODUCT**
- 2. Calls the function `ibm_db.exec_immediate` to insert rows into the **PRODUCT** table
- 3. Prints the number of rows that were inserted
- 4. Updates some rows in the table
- 5. Prints the number of rows that were updated
- 6. Deletes some rows in the table
- 7. Prints the number of rows deleted
- 8. Drops the table.

The above code snippets are part of the script `ins_upd_del.py` included in the exercise files accompanying the book. You can test the code by modifying the user ID and password in the script appropriately and run it as:

```
python ins_upd_del.py
```

The result of executing the script is illustrated in **Figure 10.6**.

![](img/5f6ba170efa3a607142589708531bef8_351_0.png)

Figure 10.6 - Executing the script ins_upd_del.py

## 10.3.4 Execute a SQL statement with parameter markers

In previous two sections, you have learned how to use function `ibm_db.exec_immediate` to execute SQL statements which is known at application written time. Now let's examine how to run a SQL statement which might contain variable inputs whose values are not known until at the run time.

The question mark (?) character will be used as the parameter marker for each variable input in the SQL statement string. The procedure to prepare and execute such SQL statements is explained below:

- 1. Connect to the database with the `ibm_db.connect` function, which returns a database connection object if connection is successful.
- 2. Prepare the SQL string with the parameter markers using the `ibm_db.prepare` function, which returns a IBM_DBStatement statement object if the prepare attempt is successful.

The syntax of function `ibm_db.prepare` is:

```
IBM_DBStatement ibm_db.prepare( IBM_DBConnection connection, string statement [, array options])
```

Table 10.4 describes the parameters of the function `ibm_db.prepare`

| Name | Description |
| :--- | :--- |
| connection | A valid database connection object returned from `ibm_db.connect()` |
| Statement | An SQL statement in string format, which may optionally contain input/output parameter markers, whose values are not known until the SQL is run. |
| options | Optional: A dictionary containing statement options. You can use this parameter to request a scrollable cursor for database servers that support this type of cursor. By default, a forward-only cursor is returned. |

### Table 10.4 - Parameters of the function ibm_db.prepare

The function returns a statement object if the SQL is successfully prepared, otherwise it raises an exception.

For example, you can prepare a **SELECT** statement containing a parameter marker as follows:

```
stmt = ibm_db.prepare(conn, "SELECT empno, lastname, job, salary FROM employee WHERE workdept = ?")
```

As shown above, the connection object **conn** is passed in as the first function argument, while the second argument is a **SELECT** string which contains a parameter marker in the predicate "workdept = ?", where the parameter marker "?" represents a variable input for a department number that is not known until the SQL is run. If the function **ibm_db.prepare** successfully prepares the SQL statement, it returns a statement object and assigns it to the variable *stmt*.

- 3. Bind input values to parameter markers in the SQL by calling the **ibm_db.bind_param** function for each parameter marker.

The syntax of function **ibm_db.bind_param** is:

```
Py_True/Py_None ibm_db.bind_param(IBM_DBStatement stmt, int
parameter-number, string variable [, int parameter-type [, int data-
type [, int precision [, int scale [, int size()]]]]]])
```

*Table 10.5* describes the parameters of function **ibm_db.bind_param**

| Name | Description |
| --- | --- |
| stmt | A prepared statement returned from **ibm_db.prepare()** |
| Parameter-number | Specifies the 1-indexed position of the parameter in the prepared statement. |
| variable | A Python variable to be bound to the parameter specified by parameter-number |
| Parameter-type | Optional: The type of the parameter marker. It can be an input parameter (SQL_PARAM_INPUT), an output parameter (SQL_PARAM_OUTPUT), or as a parameter that accepts input and returns output (SQL_PARAM_INPUT_OUTPUT). To avoid memory overhead, you can also specify PARAM_FILE to bind the Python variable to the name of a file that contains large object (BLOB, CLOB, or DB2_DBCLOB) data. By default, it’s SQL_PARAM_INPUT. |
| data-type | Optional: A constant specifying the SQL data type that the Python variable should be bound as: one of SQL_BINARY, DB2_CHAR, DB2_DOUBLE, or DB2_LONG |
| precision | Optional: Specifies the precision that the variable should be bound to the database. |
