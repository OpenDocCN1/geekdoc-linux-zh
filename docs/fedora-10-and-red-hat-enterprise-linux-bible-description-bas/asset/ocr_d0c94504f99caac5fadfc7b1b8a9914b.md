# Chapter 24: Setting Up a MySQL Database Server 937

already connected to a mysql session, type the following command (assuming the mysql name of root):

```
$ mysql -u root -p
Enter password: ********
mysql>
```

To add data to an existing MySQL database, the following procedure describes how to view the available tables and load data into those tables. The next section describes how to create a plain-text file containing database data and how to load that file into your database.

+   1. To make the database you want to use your current database (in this case, allusers), type the following command from the mysql> prompt:

```
mysql> USE allusers;
Database changed
```

+   2. To see the tables that are associated with the current database, type the following command from the mysql> prompt:

```
mysql> SHOW tables;
```

|--------------------------------------+
| Tables_in_allusers                   |
|--------------------------------------+
| name                                  |
|--------------------------------------+
1 row in set (0.00 sec)

You can see that the only table defined so far for the allusers database is the one called name.

+   3. To display the format of the name table, type the following command at the mysql> prompt:

```
mysql> DESCRIBE name;
```

| Field | Type | Null | Key | Default | Extra |
|-------|------|------+------+---------+-------|
| firstname | varchar(20) | NO | | | |
| lastname | varchar(20) | NO | | | |
| streetaddr | varchar(30) | NO | | | |
| city | varchar(20) | NO | | | |
| state | varchar(20) | NO | | | |
| zipcode | varchar(10) | NO | | | |

+   4. To add data to the new table, you can use the INSERT INTO command from the mysql> prompt. Here is an example of how to add a person's name and address to the new table: