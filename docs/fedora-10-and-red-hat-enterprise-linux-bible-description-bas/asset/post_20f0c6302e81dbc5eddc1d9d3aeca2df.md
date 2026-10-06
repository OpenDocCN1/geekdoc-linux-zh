
## Part IV: Fedora RHEL Network and Server Setup

| Data Type | Description | Space Needed |
|---|---|---|
| MEDIUMBLOB | Contains a binary large object (BLOB) that varies in size, based on the actual value of data, rather than on the maximum allowable size. MEDIUMBLOB allows larger values than BLOB. Searches on a MEDIUMBLOB column are case-sensitive. | Uses up to L-3 bytes, where L is less than or equal to 16777215. |
| MEDIUMTEXT | Same as BLOB, except that searching is done on these columns in case-insensitive style. | Uses up to L+3 bytes, where L is less than or equal to 16777215. |
| SET(val1,val2,...) | Contains a set of values. A SET column can display zero or more values from the list of values contained in the SET column definition. Up to 64 members are allowed. | Uses 1, 2, 3, 4, or 8 bytes, varying based on how many members are used. |
| TEXT | Same as BLOB, except that searching is done on these columns in case-insensitive style. | Uses up to L+2 bytes, where L is less than or equal to 65535. |
| TINYBLOB | Contains a binary large object (BLOB) that varies in size, based on the actual value of the data, rather than on the maximum allowable size. TINYBLOB allows smaller values than BLOB. Searches on a TINYBLOB column are case-sensitive. | Uses up to L+1 bytes, where L is less than or equal to 255. |
| TINYTEXT | Same as BLOB, except that searching is done on these columns in case-insensitive style. | Uses up to L+1 bytes, where L is less than or equal to 255. |
| [NATIONAL] VARCHAR(M) ([BINARY]) | Contains a character string of variable length, with no padded spaces added. The value of (M) determines the number of characters (from 1 to 255). If the BINARY keyword is used, sorting of values is case-sensitive (it is case-insensitive by default). The NATIONAL keyword indicates that the default character set should be used. | Uses L+1 bytes, where L is less than or equal to M and M is from 1 to 255 characters. |

## Chapter 24: Setting Up a MySQL Server

### Displaying Databases

There are many different ways of sorting and displaying database records during a mysql session. If you are not already connected to a mysql session, type the following command (assuming the mysql user name of root):

```
$ mysql -u root -
Enter password: ********
mysql>
```

When you are in your mysql session (and have chosen a database), you can display all selected records, choose which columns are displayed, or how records are sorted.

### Displaying all or selected records

Assuming that the current database is allusers (in the previous examples), type the following command to SELECT (*) from the name table and display them in the order in which they were entered into the database.

```
mysql> SELECT * FROM name;
+----------------------+----------------------+----------+
| firstname | lastname | streetaddr | city | state | zipcode |
+----------------------+----------------------+----------+
| Chris | Smith | 175 Harrison Street | Gig Harbor | WA | 98999 |
| John | Jones | 18 Talbot Road NW | Coventry | NJ | 54889 |
| Howard | Manty | 1515 Broadway | New York | NY | 10028 |
+----------------------+----------------------+----------+
```

The following command displays all records from the name table that have the lastname set to Jones. Instead of using lastname, you could search for a value from any column used in the table.

```
mysql> SELECT * FROM name WHERE lastname = "Jones";
+----------------------+----------------------+----------+
| firstname | lastname | streetaddr | city | state | zipcode |
+----------------------+----------------------+----------+
| John | Jones | 18 Talbot Road NW | Coventry | NJ | 54889 |
```

Using the OR operator, you can select records that have different values. In the following command, records that have either Chris or Howard as the firstname are matched and displayed.

```
mysql> SELECT * FROM name WHERE firstname = "Chris" OR firstname = "Howard";
+----------------------+----------------------+----------+
| firstname | lastname | streetaddr | city | state | zipcode |
+----------------------+----------------------+------++
| Chris | Smith | 175 Harrison Street | Gig Harbor | WA | 98999 |
| Howard | Manty | 1515 Broadway | New York | NY | 10028 |
+----------------------+----------------------+----------+
```

To match and display a record based on the value of two columns, you can use the AND operator. In the following command, any record that has Chris as the firstname and Smith as the lastname is matched.

```
mysql> SELECT * FROM name WHERE firstname = "Chris" AND lastname = "Smith";
+-------------+-----------+----------+
| firstname | streetaddr | city | state | zipcode |
+-------------+-----------+----------+
| Chris | Smith | 175 Harrison Street | Gig Harbor | WA | 98999 |
+-------------+-----------+----------+
```

### Displaying selected columns

You don't need to display every column of data. Instead of using the asterisk (*) shown in the previous examples to match all columns, you can use a comma-separated list of columns. The following command displays the firstname, lastname, and zipcode records for all of the records in the name table:

```
mysql> SELECT firstname, lastname, zipcode FROM name;
+-------------+-------------+----------+
| firstname | lastname | zipcode |
+-------------+-------------+----------+
| Chris | Smith | 98999 |
| John | Jones | 54889 |
| Howard | Manty | 10028 |
+-------------+-------------+----------+
```

Likewise, you can sort columns in any order you choose. Type the following command to show the same three columns with the zipcode displayed first:

```
mysql> SELECT zipcode, firstname, lastname FROM name;
+----------+-------------+-------------+
| zipcode | firstname | lastname |
+----------+-------------+-------------+
| 98999 | Chris | Smith |
| 54889 | John | Jones |
| 10028 | Howard | Manty |
+----------+-------------+-------------+
```

You can also mix selection with selection record as shown in the following example:

```
mysql> SELECT firstname, lastname,city FROM name WHERE firstname = "Chris";
+-------------+-------------+----------+
| firstname | lastname | city |
+-------------+-------------+----------+
| Chris | Smith | Gig Harbor |
+-------------+-------------+----------+
```

### Sorting data

You can sort records based on the values in any column you choose. For example, using the ORDER BY operator, you can display the records based on the lastname column:

```
mysql> SELECT * FROM name ORDER BY lastname;
+----------------------+-------------+-------+--------+
```

| firstname | lastname | streetaddr | city | state | zipcode |
|---|---|---|---|---|---|
| John | Jones | 18 Talbot Road NW | Coventry | NJ | 54889 |
| Howard | Manty | 1515 Broadway | New York | NY | 10028 |
| Chris | Smith | 175 Harrison Street | Gig Harbor | WA | 98999 |

To sort by city name, you can use the following command:

```
mysql> SELECT * FROM name ORDER BY city;
+----------------------+-------------+-------+--------+
```

| firstname | lastname | streetaddr | city | state | zipcode |
|---|---|---|---|---|---|
| John | Jones | 18 Talbot Road NW | Coventry | NJ | 54889 |
| Chris | Smith | 175 Harrison Street | Gig Harbor | WA | 98999 |
| Howard | Manty | 1515 Broadway | New York | NY | 10028 |
