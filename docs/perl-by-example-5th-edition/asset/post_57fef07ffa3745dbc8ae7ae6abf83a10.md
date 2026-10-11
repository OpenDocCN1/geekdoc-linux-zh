
## 15.3 Getting Started with MySQL

![](img/8556abcb353c0991f12099420ec28735_564_0.png)

**Figure 15.16 The MySQL Query Browser.**

### The phpMyAdmin Tool

The phpMyAdmin tool (see Figure 15.17) is written in PHP to handle the administration of MySQL over the Web. It is used to create and drop databases, manipulate tables and fields, execute SQL statements, manage keys on fields, manage privileges, and export data into various formats. You can download it from http://www.phpmyadmin.net/home_page/index.php.

![](img/8556abcb353c0991f12099420ec28735_565_0.png)

**Figure 15.17 The phpMyAdmin tool.**

**The MySQL Privilege System.** With a driver's license, “authentication” is verifying that it is really you who owns the license by checking your picture and expiration date, and “authorization” is validating what type of vehicle you are authorized to drive, such as a car, a large truck, or a school bus.

Similarly, the primary purpose of the MySQL privilege system is to authenticate that the user and password are valid to connect to the specified host, as demonstrated in the previous examples in both the command line and graphical client. The second purpose of the privilege system is to specify what the user, once connected to the database, is authorized to do. For example, some users may only be authorized to select and view the data from a specific table. When MySQL is installed, the MySQL database is created with tables called **grant tables** that define the initial user accounts and privileges. The first account is that of a user named *root*, also called the *superuser*. The superuser can do anything, meaning anyone logged on to the database as *root* is granted all privileges. Initially, the *root* account has no password, making it easy for anyone to log on as the superuser. The other types of accounts created are anonymous-user accounts, also without a password. For both the root and anonymous accounts, Windows gets one each and UNIX gets two. Either way, to avoid security problems, the first thing you should do, once the MySQL server starts, is to set a password on the *root* account and the anonymous accounts. For administration purposes, you should have root access rights to your server. The *mysqladmin* utility is useful for creating passwords and performing other MySQL administrative tasks. In the next example it is used to set the password for the user *root*.

#### EXAMPLE 15.2

```
1  $ mysqladmin -u root -h localhost password quigley1
2  $ mysql -u root -h localhost -pquigley1
Welcome to the MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 29 to server version: 5.0.21 community-nt

Type 'help;' or '\h' for help.  Type '\c' to clear the buffer.
```

#### EXPLANATION

- 1. The *mysqladmin* program is used to set the password for user *root* on the localhost. The password is *quigley1*.
- 2. The user *root* logs in to the database server. The *-u* switch is followed by the user or login name (no spaces between *-u* and the user name). This user is logging in as *root*. Similarly, the *-p* switch is followed by the actual password; in this case, *quigley1*. If a password is not provided, you will be prompted to enter one.

### 15.3.4 Finding the Databases

The database server keeps a list of available databases, which can be displayed as a table by issuing the *show* command at the *mysql* prompt, as shown in the following example. Typically, when you install MySQL, it comes with two databases: *test* and *mysql.test*, which is an empty database used for practicing and testing various features. You normally don’t need to have any special permissions to be able work in the *test* database. The *mysql* database is a special database where the MySQL server stores various access permissions. For now, you should not worry about this database unless you need to administer privileges. See the GRANT command in the MySQL manual.

#### EXAMPLE 15.3

```
1  mysql> -u root -pquigley1
Welcome to the MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 5 to server version: 4.1.11-nt

Type 'help;' or '\h' for help.  Type '\c' to clear the buffer.

2  mysql> show databases;
+--------------------+
| Database
+--------------------+
| information_schema |
| mysql              |
| phpmyadmin         |
| test               |
+--------------------+
4 rows in set (0.00 sec)
mysql>
```

#### EXPLANATION

- 2. The `show database` command lists all the databases on this server. Typically, when you install MySQL, you will be given the `mysql` database and the `test` database. The `test` database is just for testing purposes and is empty. The `mysql` database contains all the MySQL server privilege information.

**Creating and Dropping a Database.** Creating a database is simple. Designing it is another story and depends on your requirements and the model you will use to organize your data. Even with the smallest database, you will have to create a table. The next section will discuss how to create and drop both databases and tables. Assuming you have been granted permission to create a database, you can do it at the `mysql` command line or with the `mysqladmin` tool as shown in the following example.

#### EXAMPLE 15.4

- 1. `mysql> CREATE database my_sample_db;`
    - `Query OK, 1 row affected (0.00 sec)`
- 2. `mysql> USE my_sample_db;`
    - `Database changed`
- 3. `mysql> SHOW tables;`
    - `Empty set (0.00 sec)`
- 4. `mysql> CREATE table test (`
    - `--> field1 INTEGER,`
    - `--> field2 VARCHAR(50)`
    - `-->);`
    - `Query OK, 0 rows affected (0.36 sec)`
- 5. `mysql> SHOW tables;`
    - `+--------------------+`
    - `| Tables_in_my_sample_db |`
    - `+--------------------+`
    - `| test               |`
    - `+--------------------+`
    - `1 row in set (0.00 sec)`
- 6. `mysql> DROP table test;`
    - `Query OK, 0 rows affected (0.11 sec)`
- 7. `mysql> DROP database my_sample_db;`
    - `Query OK, 0 rows affected (0.01 sec)`

#### EXPLANATION

- 1. This command creates a database called `my_sample_db`.
- 2. Just because the database has been created doesn't mean you are in it. To enter the new database, the `use` command is executed.
- 3. The `show command` lists the tables in the database. This database is empty.
- 4. A table called `test` is created for the `my_sample_db` database. When a table is created, two columns, `field1` and `field2` are defined. Each field is assigned the type of data that will be stored there; `field1` will store whole numbers, and `field2` will store a string of up to 50 characters.
- 5. The `show` command lists all the tables in the database.
- 6. The `drop table` command destroys a table and its contents.
- 7. The `drop database` command destroys a database and its contents.

### 15.3.5 Getting Started with Basic Commands

The examples in this next section illustrate how to issue SQL commands from the MySQL client. These examples do not attempt to cover all the possible SQL statements supported by MySQL, but are here to illustrate the basic syntax for creating and dropping databases and tables and how to insert, delete, edit, alter, and select data from the tables. For a complete description of all that you can do with MySQL, visit the MySQL Documentation page at `http://dev.mysql.com/doc` (see Figure 15.18).

**Creating a Database with MySQL.** Now we are ready to create a database. This database is called `sample_db`. The `CREATE DATABASE` command creates the database, and the `SHOW DATABASES` statement demonstrates that it is now listed with the other databases. (You can also use the `mysqladmin` command to create and drop databases.)

#### EXAMPLE 15.5

```
1 mysql> CREATE DATABASE sample_db;
  Query OK, 1 row affected (0.03 sec)

2 mysql> SHOW DATABASES;

-------------------
| Database          |
-------------------
| information_schema |
| mysql              |
| northwind          |
| phpmyadmin         |
| sample_db          |
| test               |
-------------------
6 rows in set (0.00 sec)
```
