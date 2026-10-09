| Field | Type | Null | Key | Default | Extra |
|---|---|---|---|---|---|
| `person` | `varchar(20)` | `YES` | | `NULL` | |
| `password` | `char(41)` | `YES` | | `NULL` | |
| `created` | `date` | `YES` | | `NULL` | |
| `readperm` | `tinyint(1)` | `YES` | | `0` | |
| `writeperm` | `tinyint(1)` | `YES` | | `0` | |
| `executeperm` | `tinyint(1)` | `YES` | | `0` | |

**Entering data** You can enter information into a database using several techniques. The following command adds three rows to **maxdb** from a Linux text file. In the file, each row is on a separate line, a TAB separates each column from the next, and \VN specifies a null character. The file is not terminated with a NEWLINE.

```
$ cat /home/max/people_to_add$
max     \V        2008-02-17        1         1         1
zach    \V        2009-03-24        1         1         0
sam     \V        2009-01-28        1         0         0

mysql> LOAD DATA LOCAL INFILE '/home/max/people_to_add'
    -> INTO TABLE people;
Query OK, 3 rows affected (0.00 sec)
Records: 3  Deleted: 0  Skipped: 0  Warnings: 0
```

The next command adds a row using an INSERT statement:

```
mysql> INSERT INTO people
    -> VALUES ('topsy', NULL, CURDATE(),1,1,1);
Query OK, 1 row affected (0.01 sec)
```

Within an INSERT statement you can specify which columns you want to enter data into:

```
mysql> INSERT INTO people (person,created,readperm)
    -> VALUES ('bailey',CURDATE(),1), ('percy',CURDATE(),0);
Query OK, 2 rows affected (0.01 sec)
Records: 2  Duplicates: 0  Warnings: 0

mysql> SELECT * FROM people;
```

| person | password | created | readperm | writeperm | executeperm |
|---|---|---|---|---|---|
| `max` | `NULL` | `2008-02-17` | `1` | `1` | `1` |
| `zach` | `NULL` | `2009-03-24` | `1` | `1` | `0` |
| `sam` | `NULL` | `2009-01-28` | `1` | `0` | `0` |
| `topsy` | `NULL` | `2010-03-05` | `1` | `1` | `1` |
| `bailey` | `NULL` | `2010-03-05` | `1` | `0` | `0` |
| `percy` | `NULL` | `2010-03-05` | `0` | `0` | `0` |