```
```sql
mysql> SELECT * FROM name ORDER BY lastname;
+-------------+------------+------------------------+--------------+-------+---------+
| firstname   | lastname   | streetaddr             | city         | state | zipcode |
+-------------+------------+------------------------+--------------+-------+---------+
| John        | Jones      | 18 Talbot Road NW      | Coventry     | NJ    | 08759   |
| Howard      | Manty      | 1515 Broadway          | New York     | NY    | 10028   |
| Chris       | Smith      | 167 Small Road         | Gig Harbor   | WA    | 98399   |
+-------------+------------+------------------------+--------------+-------+---------+
```
```

To sort records based on city name, use the following command:

```
```sql
mysql> SELECT * FROM name ORDER BY city;
+-------------+------------+------------------------+--------------+-------+---------+
| firstname   | lastname   | streetaddr             | city         | state | zipcode |
+-------------+------------+------------------------+--------------+-------+---------+
| John        | Jones      | 18 Talbot Road NW      | Coventry     | NJ    | 08759   |
| Chris       | Smith      | 167 Small Road         | Gig Harbor   | WA    | 98399   |
| Howard      | Manty      | 1515 Broadway          | New York     | NY    | 10028   |
+-------------+------------+------------------------+--------------+-------+---------+
```
```

You can also add `ASC` or `DESC` to indicate the sorting order, because MySQL doesn’t otherwise guarantee the order in which data are displayed. Now that you have entered and displayed the database records, you may find that you need to change some of them. The following section describes how to update database records during a `mysql` session.

# ## Making Changes to Tables and Records

As you begin to use your MySQL database, you will find that you need to make changes to both the structure and content of the database tables. The following section describes how you can alter the structure of your MySQL tables and change the content of MySQL records. If you are not already connected to a `mysql` session, type the following command (assuming the `mysql` user name of root):

```
```
$ mysql -u root -P
Enter password: ******
mysql> 
```
```

To use the examples shown in the following sections, identify the database (`allusers` in this example) as the current database by typing the following:

```
```
mysql> USE allusers;
Database changed
```
```

# ### Altering the structure of MySQL tables

After you have created your database tables, you will inevitably want to make changes to them. This section describes how to use the `ALTER` command during a `mysql` session for the following tasks: adding a column, deleting a column, renaming a column, and changing the data type for a column.