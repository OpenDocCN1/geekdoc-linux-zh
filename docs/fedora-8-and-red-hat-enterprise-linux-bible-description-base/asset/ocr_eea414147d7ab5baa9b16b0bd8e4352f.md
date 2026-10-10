**NOTE:** While you are in a *mysql* session, keep in mind that you can use the up arrow key to retrieve and change previous commands. This is particularly useful if you are manually entering database records that contain similar information.

# Manually entering data

To do the procedure in this section, I assume you have an open interactive *mysql* session and that you have created a database and table as described in the previous section. If you are not already connected to a *mysql* session, type the following command (assuming the *mysql* user name of root):

```
$ mysql -u root -P
Enter password: ********
mysql>
```

To add data to an existing MySQL database, the following procedure describes how to view the available tables and load data into those tables manually. The next section describes how to create a plain-text file containing database data and how to load that file into your database.

+   1. To make the database you want to use your current database (in this case, allusers), type the following command from the *mysql>* prompt:

```
mysql> USE allusers;
Database changed
```

+   2. To see the tables that are associated with the current database, type the following command from the *mysql>* prompt:

```
mysql> SHOW tables;
+-------------------+
| Tables_in_allusers |
+-------------------+
| name             |
+-------------------+
1 row in set (0.00 sec)
```

You can see that the only table defined so far for the allusers database is the one called name.

+   3. To display the format of the name table, type the following command at the *mysql>* prompt:

```
mysql> DESCRIBE name;
+------------+----------+------+-----+-------+-------+
| Field      | Type     | Null | Key | Default| Extra |
+------------+----------+------+-----+-------+-------+
| firstname  | varchar(20)| NO |     |       |       |
| lastname   | varchar(20)| NO |     |       |       |
| streetaddr | varchar(30)| NO |     |       |       |
| city       | varchar(20)| NO |     |       |       |
```