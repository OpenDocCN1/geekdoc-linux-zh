
## OPTIONS

This section describes some of the options you can use on the *mysql* command line. The options preceded by a single hyphen and those preceded by a double hyphen are equivalent.

-   **--disable-reconnect**
    Does not attempt to connect to the server again if the connection is dropped. See **--reconnect**.

-   **--host=***hostname*  **-h** *hostname*
    Specifies the address of the MySQL server as *hostname*. Without this option MySQL connects to the server on the local system (127.0.0.1).

-   **--password[=***passwd***]**
    **-p[***passwd***]**
    Specifies the MySQL password as *passwd*. For improved security, do not specify the password on the command line; MySQL will prompt for it. By default, MySQL does not use a password. In the short form of this option, do not put a SPACE between the **-p** and *passwd*.

-   **--reconnect**
    Attempts to connect to the server again if the connection is dropped (default). Disable this behavior using **--disable-reconnect**.

-   **--user=***usr*  **-u** *usr*
    Specifies the MySQL user as *usr*. When you first install MySQL, there is one user, **root**, and that user does not have a password.

-   **--verbose**  **-v**
    Increases the amount of information MySQL displays. Use this option multiple times to further increase verbosity.

## THE .MY.CNF CONFIGURATION FILE

You can use the *~/.my.cnf* file to set MySQL options. The following example shows Max's *~/.my.cnf* file. The [**mysql**] specifies the MySQL group. The next line sets Max's password to **mpassword**. With this setup, Max does not have to use **-p** on the command line; MySQL logs him in automatically.

```
$ cat /home/max/\.my.cnf
[mysql]
password="mpassword"
```

## WORKING WITH MYSQL

### Adding a user

Before starting to work with the database, create a user so you do not have to work as the MySQL **root** user. If the MySQL username you add is the same as your Linux username, you will not have to specify a username on the MySQL command line. In the following example, Max works as the MySQL **root** (**-u** **root**) user to create a database named **maxdb** and add the MySQL user named **max** with a password of **mpassword**. In response to the *Enter password* prompt, Max supplies the password for the MySQL user named **root**. The **GRANT** statement gives Max the permissions he needs to work with the **maxdb** database. You must work as the MySQL **root** user to set up a MySQL user. The **-p** option causes MySQL to prompt for the password.

When using the MySQL interpreter, **Query OK** indicates that the preceding statement was syntactically correct. You must enclose all character and date data within single quotation marks.

```
$ mysql -u root -p
Enter password:
Welcome to the MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 12
Server version: 5.1.40 Source distribution

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

mysql> CREATE DATABASE maxdb;
Query OK, 1 row affected (0.00 sec)

mysql> GRANT ALL PRIVILEGES
    -> ON maxdb.* to 'max'
    -> IDENTIFIED BY 'password'
    -> WITH GRANT OPTION;
Query OK, 0 rows affected (0.00 sec)

mysql> SELECT user, password
    -> FROM mysql.user;

+--------------------+-------------------------------------------+
| user               | password                                  |
+--------------------+-------------------------------------------+
| root               | *96D4C5B9348F896B0B593E4ADC1B653156799FDD |
| max                | *34432555D06C778C7C4B40EE4551425CE3AC0E16 |
| debian-sys-maint   | *E41C0008AE5D3C42D15447ABC53308E62505ADF1 |
+--------------------+-------------------------------------------+
3 rows in set (0.00 sec)

mysql> quit
Bye
$
```

In the preceding example, after creating the database and setting up the new user, Max queries the user table of the **mysql** database to display the **user** and **password** columns. Two users now exist: **root** and **max**. Max gives the command **quit** to exit from the MySQL interpreter.

Working as the MySQL user **max**, Max can now set up a simple database to keep track of users. He does not need to use the **-u** option on the command line because his Linux username and his MySQL username are the same.

### Specifying the default database

For subsequent commands, if you do not tell MySQL which database you are working with, you must prefix the names of tables with the name of the database. For example, you would need to specify the **people** table in the **maxdb** database as **maxdb.people**. When you specify the **maxdb** database with a USE statement, you can refer to the same table as **people**. In the following example, Max specifies **maxdb** as the database he is working with:

```
mysql> USE maxdb;
Database changed
```

Next Max creates a table named **people** in the **maxdb** database. This table has six columns of various types. After creating the table, Max uses a DESCRIBE statement to display a description of the table.

```
mysql> CREATE TABLE people ( person VARCHAR(20), password CHAR(41),
-> created DATE, readperm BOOL, writeperm BOOL, executeperm BOOL );
Query OK, 0 rows affected (0.01 sec)
```

```
mysql> DESCRIBE people;

+-------------+-----------+------+-----+---------+-------+
| Field | Type | Null | Key | Default | Extra |
+-------------+-----------+------+-----+---------+-------+
| person | varchar(20) | YES | | NULL | |
| password | char(41) | YES | | NULL | |
| created | date | YES | | NULL | |
| readperm | tinyint(1) | YES | | NULL | |
| writeperm | tinyint(1) | YES | | NULL | |
| executeperm | tinyint(1) | YES | | NULL | |
+-------------+-----------+------+-----+---------+-------+
6 rows in set (0.00 sec)
```

MySQL changed the columns Max specified as BOOL (Boolean) to type tinyint(1), an 8-bit integer, because MySQL does not have native (bit) Boolean support. With tinyint(1), 0 evaluates as **FALSE** and 1–255 evaluate as **TRUE**. **Figure 16-6** shows part of the **people** table after data has been entered in it.

Max decides that the **readperm**, **writeperm**, and **executeperm** columns should default to 0. He uses an ALTER TABLE statement to modify the table so he does not have to delete it and start over. He then checks his work using a DESCRIBE statement.

![](img/2344fc4a798f29dca9e8b5ed7288171a_682_0.png)

```
mysql> ALTER TABLE people
-> MODIFY readperm BOOL DEFAULT 0,
-> MODIFY writeperm BOOL DEFAULT 0,
-> MODIFY executeperm BOOL DEFAULT 0 ;
Query OK, 0 rows affected (0.01 sec)
Records: 0 Duplicates: 0 Warnings: 0
```

```
mysql> DESCRIBE people;
```

| Field | Type | Null | Key | Default | Extra |
|---|---|---|---|---|---|
| `person` | `varchar(20)` | `YES` | | `NULL` | |
| `password` | `char(41)` | `YES` | | `NULL` | |
| `created` | `date` | `YES` | | `NULL` | |
| `readperm` | `tinyint(1)` | `YES` | | `0` | |
| `writeperm` | `tinyint(1)` | `YES` | | `0` | |
| `executeperm` | `tinyint(1)` | `YES` | | `0` | |

### Entering data

You can enter information into a database using several techniques. The following command adds three rows to **maxdb** from a Linux text file. In the file, each row is on a separate line, a TAB separates each column from the next, and \VN specifies a null character. The file is not terminated with a NEWLINE.

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
