```
mysql> LOAD DATA LOCAL INFILE "/tmp/name.txt" INTO TABLE name;
Query OK, 3 rows affected (0.02 sec)
Records: 3 Deleted: 0 Skipped: 0 Warnings: 0
```

Type the following at the mysql> prompt to make sure that the records have been added correctly:

```
mysql> SELECT * FROM name;
\+-----------\+-----------\+-------------\+------------\+-------\+--------\+
| firstname | lastname  | streetaddr  | city       | state | zipcode |
\+-----------\+-----------\+-------------\+------------\+-------\+--------\+
| Jerry     | Wignut    | 167 E Street| Roy        | UT    | 84103  |
| Chris     | Smith     | 175 Harrison Street| Gig Harbor| WA    | 98999  |
| John      | Jones     | 18 Talbot Road Newes| Coventry   | NJ    | 08759  |
| Howard    | Manty     | 1515 Broadway | New York   | NY    | 10028  |
\+-----------\+-----------\+-------------\+------------\+-------\+--------\+
```

At this point, you have a database that includes some data that you can begin working with. If something went wrong, refer to the “Updating and Deleting MySQL Records” section later in this chapter. If you find you need more information than is provided in this chapter, refer to the MySQL documentation at http://dev.mysql.com/doc.

> NOTE: Because some text editors (not including vi) don't use a hard tab character by default, it can be difficult to create a correctly formatted file. As an alternative, you can import a CSV-formatted text file (many spreadsheet programs can export to such a file). To include such a file that has comma-separated fields and text enclosed in quotes (for example, named /tmp/name.csv), you could use the following (all on one line):

```
mysql> LOAD DATA LOCAL INFILE '/tmp/name.csv' INTO TABLE
allusers.name
FIELDS TERMINATED BY ',' ENCLOSED BY '"' LINES
TERMINATED BY '\n';
```

Although MySQL doesn't support all of SQL, it does contain enough features for most users. If you find that MySQL doesn't meet your needs, try the PostgreSQL object-relational database management system (which also comes with Fedora systems). For further information on PostgreSQL, refer to http://www.postgresql.org. Firebird (http://www.firebirdsql.org) is another open source relational database that might interest you.

# # Understanding MySQL Tables

You have a lot of flexibility when it comes to setting up MySQL tables. To have your MySQL database operate as efficiently as possible, you want to have the columns assigned to the most appropriate size and data type to hold the data you need to store.