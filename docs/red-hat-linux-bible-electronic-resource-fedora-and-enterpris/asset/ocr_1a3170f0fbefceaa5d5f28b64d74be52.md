```
+----------+-------+--------------------+-----------+------+--------+
| Chris    | Smith | 175 Harrison Street | Gig Harbor | WA   | 98999  |
+----------+-------+--------------------+-----------+------+--------+
```

# ## Displaying selected columns

You don't need to display every column of data. Instead of using the asterisk (*) shown in previous examples to match all columns, you can enter a comma-separated list of column names. The following command displays the firstname, lastname, and zipcode records for all of the records in the "names" table:

```
mysql> SELECT firstname,lastname,zipcode FROM names;
+-----------+----------+--------+
| firstname | lastname | zipcode |
+-----------+----------+--------+
| Chris     | Smith    |  98999  |
| John      | Jones    |  54889  |
| Howard    | Manty    |  10028  |
+-----------+----------+--------+
```

Likewise, you can sort columns in any order you choose. Type the following command to show the same three columns with the zipcode column displayed first:

```
mysql> SELECT zipcode,firstname,lastname FROM names;
+---------+-----------+----------+
| zipcode | firstname | lastname |
+---------+-----------+----------+
|  98999  | Chris     |  Smith    |
|  54889  | John      |  Jones    |
|  10028  | Howard    |  Manty    |
+---------+-----------+----------+
```