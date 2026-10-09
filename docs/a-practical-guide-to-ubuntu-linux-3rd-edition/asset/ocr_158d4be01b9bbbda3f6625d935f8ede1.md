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

# Specifying the default database

For subsequent commands, if you do not tell MySQL which database you are working with, you must prefix the names of tables with the name of the database. For example, you would need to specify the **people** table in the **maxdb** database as **maxdb.people**. When you specify the **maxdb** database with a USE statement, you can refer to the same table as **people**. In the following example, Max specifies **maxdb** as the database he is working with:

```
mysql> USE maxdb;
Database changed
```