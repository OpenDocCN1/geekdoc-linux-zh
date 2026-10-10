create an instance of PDO using the DSN, user name, and password as shown in *Listing 8.17* below.

```
<?php
/* Use one of the following connection strings */
/* The connection below is for pdo_ibm */
$constring = 'ibm:sample';
/* The connection below is for pdo_odbc */
$constring = 'odbc:sample';
try {
    
    $dbh = new PDO($constring, 'db2inst1', '123');
    echo 'Connected';
} catch (PDOException $exp) {
    echo 'Exception: ' . $exp->getMessage();
}
?>
```

# Listing 8.17 — Making a Non-persistent connection

To make a persistent connection use the following `new PDO` format:
`$dbh = new PDO($constring, 'db2inst1', '123',
array(PDO::ATTR_PERSISTENT=> true));`

# 8.3.3.3 Preparing and executing the statement

Before you prepare and execute SQL statements, you need to decide the following characteristics about the transaction:

+   * Type of cursor used
+   * How to catch the error
+   * Isolation level to use

# 8.3.3.1 Type of cursor to be used

Like the ibm_db2 extension, PDO also supports two kinds of cursors:

# **Forward-only cursor**
This cursor is the default cursor in the PDO driver. It is the fastest cursor available. Make sure that the cursor is closed using the method `PDOStatement::closeCursor` after fetching all the rows and before launching another query. The Forward-only cursor can be set using `PDO::ATTR_CURSOR` with the value of `PDO::CURSOR_FWDONLY` in the `PDOStatement::prepare`. *Listing 8.20* provides an example.

```
$sql = "SELECT c_id, c_name, c_email FROM customer WHERE c_name = 
```