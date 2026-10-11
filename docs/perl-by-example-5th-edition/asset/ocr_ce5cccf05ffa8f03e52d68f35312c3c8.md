# 15.3  Getting Started with MySQL

**EXAMPLE 15.7**

```
1  mysql> CREATE TABLE teams (
     ->  name VARCHAR(100) not null,
     ->  wins INT unsigned,
     ->  losses INT unsigned);
Query OK, 0 rows affected (0.09 sec)
```

```
2  mysql> SHOW TABLES;
+--------------------+
| Tables_in_sample_db |
+--------------------+
| teams              |
+--------------------+
1 row in set (0.00 sec);
```

```
3  mysql> DESCRIBE teams;
+--------+---------------+------+-----+---------+-------+
| Field  | Type          | Null | Key | Default | Extra |
+--------+---------------+------+-----+---------+-------+
| name   | varchar(100)  | NO   |     |         |       |
| wins   | int(10) unsigned| YES |     | NULL    |       |
| losses | int(10) unsigned| YES |     | NULL    |       |
+--------+---------------+------+-----+---------+-------+
1 row in set (0.00 sec)
```

**EXPLANATION**

+   1.  The `CREATE TABLE` statement creates a table in the database. This table is named `teams`. It consists of three fields: `name`, `wins`, and `losses`. The `name` field will consist of a varying string of up to 100 characters; the `wins` and `losses` fields will hold unsigned integers.

+   2.  The `SHOW` command lists the tables in a database. (The `SHOW` command has many forms that provide information about databases, tables, columns, or status information about the server.)

+   3.  The `DESCRIBE` command describes the structure of the table, meaning, the names of the fields and the type of data that can be stored in each field. Note that the `name` field cannot be `NULL`, and the default value for the `wins` and `losses` is `NULL` if a value isn't supplied; for example, if a team hasn't played any games, the `wins` and `losses` will be assigned `NULL`.

**Adding Another Table with a Primary Key**  In the next example, we will create another table and add a primary key. A primary key is used to uniquely identify the records in the database. A user's login name, UID, account number, or license plate are examples of unique IDs. A primary key is a unique index where all key columns must be defined as `NOT NULL`. If they are not explicitly declared as `NOT NULL`, MySQL declares them so implicitly (and silently). A table can have only one primary key.