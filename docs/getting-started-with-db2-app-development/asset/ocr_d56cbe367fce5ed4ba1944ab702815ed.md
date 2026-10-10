```
			)
			while ($row = db2_fetch_assoc($stmt)) {
				printf("%d %s %s ", $row['C_ID'], $row['C_NAME'], $row['C_EMAIL']);
			}
		```

# **Listing 8.8 – Using db2_fetch_assoc function**

Since the columns are indexed by the column names, the case of the column names does matter. The default case of the column can be overridden using the DB2_ATTR_CASE statement option which can have one of these values:

+   - **DB2_CASE_NATURAL**: Column names as returned by DB2.
+   - **DB2_CASE_LOWER**: Column names are forced to lower case.
+   - **DB2_CASE_UPPER**: Column names are forced to uppercase.

For example, if you would like to force column names to lower case, use:

```
```php
$stmt = db2_prepare($conn_resource, $sql, array('DB2_ATTR_CASE' =>
DB2_CASE_LOWER));
```
```

# **8.3.2.4.3 Using db2_fetch_both**

This function returns an array which is indexed by both the column number and the column name. *Listing 8.9* provides an example.

```
```php
while ($row = db2_fetch_both($stmt)) {
  printf("%d %s %s", $row[0], $row['C_NAME'], $row['C_EMAIL']);
}
```
```

# **Listing 8.9 – Using db2_fetch_both function**

# **8.3.2.4.4 Using db2_fetch_object**

This function can be used to return an object for each row fetched. Each property of the object will be the column returned. *Listing 8.10* provides an example.

```
```php
while ($row = db2_fetch_object($stmt)) {
  printf("%d %s %s", $row->C_ID, $row->C_NAME, $row->C_EMAIL);
}
```
```

# **Listing 8.10 – Using db2_fetch_object function**

# **8.3.2.4.5 Using db2_fetch_row**

This function can be used to iterate through the result set or go to the specified row number when using scrollable cursor. *Listing 8.11* shows how to fetch all the rows in the result set using **db2_fetch_row** function.