You might expect that creating the database would also make it the default (or current) database, but it doesn't. You can see this by executing the following statement to check what the default database is:

```
```text
mysql> SELECT DATABASE();
+----------------+
| DATABASE()     |
+----------------+
| NULL           |
+----------------+
```
```

NULL means “no database is selected.” To select sampdb as the default database, issue a USE statement:

```
```text
mysql> USE sampdb;
mysql> SELECT DATABASE();
+----------------+
| DATABASE()     |
+----------------+
| sampdb         |
+----------------+
```
```

Another way to select a default database is to name it on the command line when you invoke mysql:

```
$ mysql sampdb
```

That is, in fact, the usual way to select the database you want to use. If you need any connection parameters, specify them on the command line. For example, the following command enables the sampadm user to connect to the sampdb database on the local host (the default when no host is named):

```
$ mysql -p -u sampadm sampdb
```

If you need to connect to a MySQL server running on a remote host, specify that host on the command line:

```
$ mysql -h cobra.snake.net -p -u sampadm sampdb
```

Unless otherwise indicated, all following examples assume that when you invoke mysql, you name the sampdb database on the command line to make it the default database. If you invoke mysql but forget to name the database on the command line, just issue a USE sampdb statement at the mysql> prompt.

# 1.4.6 Creating Tables

In this section, we'll build the tables that are needed for the sampdb sample database. First, we'll consider the tables needed for the Historical League, and then those for the grade-keeping project. This is the part where some database books start talking about Analysis and Design, Entity-Relationship Diagrams, Normalization Procedures, and other such