The default fetch mode determines how the rows are returned.

# 9.1.5 Testing for NULL Values in Query Results

PHP represents the SQL NULL value in result sets using the PHP NULL value. One way to check for NULL in a column value returned from a SELECT query is to use the is_null() function. The following example selects and prints names and email addresses from the member table, printing“ No email address available” if the address is NULL.

```
```
$stmt = "SELECT last_name, first_name, email FROM member";
$sth = $dbh->query ($stmt);
while (list ($last_name, $first_name, $email) = $sth->fetch (PDO::FETCH_NUM)) {
    printf ('Name: %s %s, Email: ', $first_name, $last_name);
    if (is_null ($email))
        print ('No email address available');
    else
        print ($email);
    print ('\n');
}
```
```

You can also test for SQL NULL values by comparing a value to the PHP NULL constant using the === identically-equal-to operator:

```
```
if ($email === NULL)
    print ('No email address available');
else
    print ($email);
```
```

PHP NULL is the same as an unset value, so isset() provides another way to test for NULL values:

```
```
if (!isset ($email))
    print ('No email address available');
else
    print ($email);
```
```

# 9.1.6 Using Prepared Statements

The exec() and query() methods described earlier execute SQL statements and return their results immediately. PDO can also prepare and execute statements in separate steps. Use the database handle with prepare() to obtain a statement handle, and use the statement handle to execute the statement:

```
```
$sth = $dbh->prepare ($stmt);
$sth->execute ();
```
```