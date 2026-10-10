# Working with MySQL Databases

The first time you start the MySQL server (using the start-up script described previously), the system creates the initial grant tables for the MySQL database. It does this by running the mysql_install_db command.

The mysql_install_db command starts you off with two databases: mysql and test. As you create data for these databases, that information is stored in the /var/lib/mysql/mysql and /var/lib/mysql/test directories, respectively.

Because the MySQL root user doesn't have to be the system's root user (provided you have the MySQL root user's password), you can be logged into CentOS as any user you choose. In the following examples, be sure to provide the MySQL root user password when you run the commands shown.

> **NOTE** If you are using the old ISAM tables instead of MyISAM, support for ISAM tables was removed for MySQL 5.0. You need to convert your tables to MyISAM using a statement such as the following:
> 
> > ALTER TABLE table ENGINE=MyISAM
> >
> > where *table* is your table name. Refer to the MySQL Reference Manual (<http://dev.mysql.com/doc/refman/5.0/en/upgrade.html>) for further information on upgrading to MySQL 5.0.

# Starting the mysql Command

To get started creating databases and tables, you can use the mysql command. From any Terminal window, open the mysql database on your computer by typing the following:

```
$ mysql -u root -p mysql
Enter password: ********

Welcome to the MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 39
Server version: 5.0.45 Source distribution
Type 'help;' or '\h' for help. Type '\c' to clear the buffer
mysql>
```

Type in the root user's MySQL password as prompted. (If no password has been set, you can skip the -p option.) The mysql> prompt appears, ready to accept commands for working with the mysql default database on the local host. If you are connecting to the MySQL server from another host computer, add -h hostname to the command line (where hostname is the name or IP address of the computer on which the MySQL server is running). Remember that you can also log in as any valid MySQL login you created, regardless of which Linux login account you are currently logged in under.