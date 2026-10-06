# Chapter 24: Setting Up a MySQL Database Server 945

# Displaying MySQL Databases

There are many different ways of sorting and displaying database records during a mysql session. If you are not already connected to a mysql session, type the following command (assuming the mysql user name of root):

```
$ mysql -u root -p
Enter password: ********
mysql>
```

When you are in your mysql session (and have chosen a database), you can display all selected table records, choose which columns are displayed, or how few records are sorted.

# Displaying all or selected records

Assuming that the current database is allusers (in the previous examples), type the following command to (SELECT *) from the name table and display them in the order in which they were entered into the database.

```
mysql> SELECT * FROM name;
+----------------------+----------------------+------+----------+
| firstname | lastname | streetaddr | city | state | zipcode |
+----------------------+--------------------+------+------+----------+
| Chris | Smith | 175 Harrison Street | Gig Harbor | WA | 98999 |
| John | Jones | 18 Talbot Road NW | Coventry | NJ | 54889 |
| Howard | Manty | 1515 Broadway | New York | NY | 10028 |
+----------------------+--------------------+------+------+----------+
```

The following command displays all records from the name table that have the lastname column set to Jones. Instead of using lastname, you could search for a value from any name column used in the table.

```
mysql> SELECT * FROM name WHERE lastname = "Jones";
+----------------------+--------------------+------+------+----------+
| firstname | lastname | streetaddr | city | state | zipcode |
+----------------------+--------------------+------+------+----------+
| John | Jones | 18 Talbot Road NW | Coventry | NJ | 54889 |
+----------------------+--------------------+------+------+----------+
```

Using the OR operator, can select records that have different values. In the following command, records that have either Chris or Howard as the firstname are matched and displayed.

```
mysql> SELECT * FROM name WHERE firstname = "Chris" OR firstname = "Howard";
+----------------------+--------------------+------+------+----------+
| firstname | lastname | streetaddr | city | state | zipcode |
+----------------------+--------------------+------+------+----------+
| Chris | Smith | 175 Harrison Street | Gig Harbor | WA | 98999 |
| Howard | Manty | 1515 Broadway | New York | NY | 10028 |
+----------------------+--------------------+------+------+----------+
```