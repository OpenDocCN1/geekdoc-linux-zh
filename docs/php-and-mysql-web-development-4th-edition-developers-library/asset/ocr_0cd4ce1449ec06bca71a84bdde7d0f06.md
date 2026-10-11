+   • **--syslog-tag**=*tag*
+   
+       When *error output* is sent to *syslog*, messages from *mysqld_safe* and *mysqld* are tagged with the program name as a prefix. The **--syslog-tag** option modifies the prefix to be *mysqld_safe-*tag and *mysqld-*tag, respectively. This option was introduced in MySQL 5.1.21.

+   • **--timezone**=*tz_name*
+   
+       Sets the server system time zone to *tz_name*. This might be useful if the server doesn't determine the system time zone automatically.

+   • **--user**=*user_name*, **--user**=*uid*
+   
+       The username or numeric user ID of the account to use for running the server.

# F.15  mysqldump

The *mysqldump* program writes the contents of database tables into text files. These files can be used for a variety of purposes, such as database backups, moving databases to another server, or setting up a test database based on the contents of an existing database.

By default, output for each dumped table consists of a *CREATE TABLE* statement that creates the table, followed by a set of *INSERT* statements that load the contents of the table. If the **-tab** option is given, the table contents are written to a data file as tab-separated values, one line per row, and the table-creation SQL statement is written to a separate file.

mysqldump can be run in any of three modes:

```
```
mysqldump [options] db_name [tbl_name] ...
mysqldump [options] --databases db_name ...
mysqldump [options] --all-databases
```
```

In the first case, *mysqldump* dumps the named tables in the given database. If no tables are named, *mysqldump* dumps all tables in the database. In the second case, all arguments are taken as database names and *mysqldump* dumps all tables in each one. In the third case, *mysqldump* dumps all tables in all databases. If **--databases** or **--all-databases** is used, the output contains *CREATE DATABASE IF EXISTS* and *USE* statements preceding the statements for the tables in each database.

One common way to use *mysqldump* is as follows:

```
```
% mysqldump db_name > backup_file
```
```

The backup file should be imported back into MySQL with *mysql* rather than with *mysqlimport*:

```
```
% mysql db_name < backup_file
```
```

*mysqldump* ignores and does not dump the *INFORMATION_SCHEMA* database, even if you name it explicitly on the command line.