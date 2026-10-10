The status information tells you about the version of the MySQL server (14.12) and the distribution (5.0.45). The output also reminds you of the current database (mysql1) and your user name (root@localhost). You can see how long the server has been up (Uptime). You can also see how many threads are currently active and how many commands have been run to query this server (Questions).

# ## Creating a database with mysql

Within an interactive *mysql* session, you can create and modify databases and tables. If you are not already connected to a *mysql* session, type the following command (assuming the *mysql* user name of root):

```
$ mysql -u root -p
Enter password: ********
mysql>
```

The general steps for creating a MySQL database include creating the database name, identifying the new database as the current database, creating tables, and adding data to the tables. While you are connected to a *mysql* session, you can run the following procedure to create a sample database.

+   1. To create a new database name, use the CREATE DATABASE command at the mysql> prompt. For example, to create a database named allusers, type the following:

```
mysql> CREATE DATABASE allusers;
```

This action creates a database called *allusers* in the /var/lib/mysql directory. (While you don’t have to use capitals for the commands just shown, it makes it easier to distinguish the commands from the database entries.)

> **NOTE:** Alternatively, you can create a database from the command line using the *mysqladmin* command. For example, to create a database named *allusers* with *mysqladmin*, you could type the following: *mysqladmin -u root -p create allusers*

+   2. To see what databases are available for your *mysql* server, type the following at the *mysql>* command prompt:

```
mysql> SHOW DATABASES;
+--------------------+
| Database           |
+--------------------+
| information_schema |
| allusers           |
| mysql              |
| test               |
+--------------------+
4 rows in set (0.00 sec)
```