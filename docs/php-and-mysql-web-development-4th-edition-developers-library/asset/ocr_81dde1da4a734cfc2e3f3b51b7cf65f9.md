2.5 Selecting, Creating, Dropping, and Altering Databases

113

# 2.5.2 Creating Databases

To create a database, use a CREATE DATABASE statement:

```
CREATE DATABASE db_name;
```

The conditions on database creation are that the name must be a legal identifier, the database must not already exist, and you must have sufficient privileges to create it.

When you create a database, the MySQL server creates a directory under its data directory that has the same name as the database. The new directory is called the database directory. The server also creates a db.opt file in the database directory for storing database attributes.

CREATE DATABASE supports several optional clauses. The full syntax is as follows:

```
CREATE DATABASE [IF NOT EXISTS] db_name
[CHARACTER SET charset] [COLLATE collation];
```

Normally, an error occurs if you try to create a database that already exists. To suppress this error and create a database only if it does not already exist, add an IF NOT EXISTS clause:

```
CREATE DATABASE IF NOT EXISTS db_name;
```

By default, the server character set and collation become the database default character set and collation. You can use the CHARACTER SET and COLLATE clauses to set these database attributes explicitly. For example:

```
CREATE DATABASE mydb CHARACTER SET utf8 COLLATE utf8_icelandic_ci;
```

If CHARACTER SET is given without COLLATE, the default collation for the character set is used. If COLLATE is given without CHARACTER SET, the first part of the collation name determines the character set.

The character set must be one of those supported by the server, such as latin1 or sjis. The collation should be a legal collation for the character set. For further discussion of character sets and collations, see Chapter 3.

MySQL stores the database character set and collation attributes in the db.opt file. When you create a new table, if the table definition does not specify its own default character set and collation, the database defaults become the table defaults.

To see the definition for an existing database, use a SHOW CREATE DATABASE statement:

```
mysql> SHOW CREATE DATABASE mydb\G
*************************** 1. row ***************************
 Database: mydb
 Create Database: CREATE DATABASE `mydb`
/*!40100 DEFAULT CHARACTER SET utf8
 COLLATE utf8_icelandic_ci */
```