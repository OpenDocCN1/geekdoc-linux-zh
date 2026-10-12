
The command prepares MySQL for use on the system and reports helpful information. The next step is to set the password for the MySQL root user, which is discussed in the following section.

**CAUTION**

By default, the MySQL root user is created with no password. This is one of the first things you must change because the MySQL root user has access to all aspects of the database. The following section explains how to change the password of the user.

## Setting a Password for the MySQL Root User

To set a password for the root MySQL user, you need to connect to the MySQL server as the root MySQL user; you can use the command `mysql -u root` to do so. This command connects you to the server with the MySQL client. When you have the MySQL command prompt, issue a command like the following to set a password for the root user:

```
mysql> SET PASSWORD FOR root = PASSWORD('secretword');
```

*secretword* should be replaced by whatever you want to be the password for the root user. You can use this same command with other usernames to set or change passwords for other database users.

After you enter a password, you can exit the MySQL client by typing **exit** at the command prompt.

## Creating a Database in MySQL

In MySQL you can create a database by using the `CREATE DATABASE` statement. To create a database, you connect to the server by typing `mysql -u root -p` and pressing Enter. After you do so, you are connected to the database as the MySQL root user and prompted for a password. After you enter the password, you are placed at the MySQL command prompt. Then you use the `CREATE DATABASE` command. For example, the following commands create a database called animals:

```
mysql -u root -p
Enter password:
Welcome to the MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 1 to server version: 3.23.58

Type 'help;' or '\h' for help.  Type '\c' to clear the buffer.

mysql> CREATE DATABASE animals;
Query OK, 1 row affected (0.00 sec)

mysql>
```

Another way to create a database is to use the `mysqladmin` command, as the `root` user, with the `create` keyword and the name of a new database. For example, to create a new database named `reptiles`, you use a command line like this:

```
mysqladmin -u root -p create reptiles
```

## Granting and Revoking Privileges in MySQL

You probably want to grant yourself some privileges, and eventually you will probably want to grant privileges to other users. Privileges, also known as *rights*, are granted and revoked on four levels:

- **Global level**—These rights allow access to any database on a server.
- **Database level**—These rights allow access to all tables in a database.
- **Table level**—These rights allow access to all columns within a table in a database.
- **Column level**—These rights allow access to a single column within a database's table.

**NOTE**

Listing all the available privileges is beyond the scope of this chapter. See the MySQL documentation for more information.

To add a user account, you connect to the database by typing `mysql -u root -p` and pressing Enter. You are then connected as the `root` user and prompted for a password. (You did set a password for the root user, as instructed in the last section, right?) After you enter the `root` password, you are placed at the MySQL command prompt.

To grant privileges to a user, you use the `GRANT` statement, which has the following syntax:

```
grant what_to_grant on where_to_grant TO user_name IDENTIFIED BY 'password';
```

The first option, `what_to_grant`, is the privileges you are granting to the user. These privileges are specified with keywords. For example, the `ALL` keyword is used to grant global-, database-, table-, and column-level rights for a specified user.

The second option, `where_to_grant`, specifies the resources on which the privileges should be granted. The third option, `user_name`, is the username to which you want to grant the privileges. Finally, the fourth option, `password`, is a password that should be assigned to this user. If this is an existing user you already have a password and you are modifying permissions, you can omit the `IDENTIFIED BY` portion of the statement.

For example, to grant all privileges on a database named `sampledata` to a user named `foobar`, you could use the following command:

```
GRANT ALL ON animals.* TO foobar IDENTIFIED BY 'secretword';
```

The user foobar can now connect to the database sampledata by using the password secretword, and foobar has all privileges on the database, including the ability to create and destroy tables. For example, the user foobar can now log in to the server (by using the current hostname—shuttle2, in this example), and access the database like so:

```
$ mysql -h shuttle2 -u foobar -p animals
Enter password:
Welcome to the MySQL monitor. Commands end with ; or \g.
Your MySQL connection id is 43 to server version: 3.23.58

Type 'help'; or '\h' for help. Type '\c' to clear the buffer.
mysql>
```

**NOTE**

See the section “The MySQL Command-Line Client” later in this chapter for additional command-line options.

Later, if you need to revoke privileges from foobar, you can use the REVOKE statement. For example, the following statement revokes all privileges from the user foobar:

```
REVOKE ALL ON animals FROM foobar;
```

Advanced database administration, privileges, and security are very complex topics that are beyond the scope of this book. See the “Reference” section at the end of this chapter for links to online documentation. You can also check out Luke Welling’s and Laura Thompson’s book PHP and MySQL Development from Sams Publishing.

# Configuring PostgreSQL

If you do not want to use the version of PostgreSQL bundled with Fedora, the latest PostgreSQL binary files and source are available at http://www.postgresql.org/. The PostgreSQL RPMs are distributed as several files. At a minimum, you probably want the postgresql, postgresql-server, and postgresql-libs RPMs. You should see the README.rpm-dist file in the FTP directory ftp://ftp.postgresql.org/pub/ to determine whether you need any other packages.

If you are installing from the Fedora RPM files, a necessary postgres user account (that is, an account with the name of the user running the server on your system) is created for you automatically:

```
$ fgrep postgres /etc/passwd
postgres:x:26:26:PostgreSQL Server:/var/lib/pgsql:/bin/bash
```

Otherwise, you need to create a user called postgres during the installation. This user shouldn’t have login privileges because only root should be able to use su to become this user and no one will ever log in directly as the user. (Refer to Chapter 14, “Managing Users,” for more information on how to add users to a Fedora system.) After you have added the user, you can install each of the PostgreSQL RPMs you downloaded using the standard rpm -i command for a default installation.

## Initializing the Data Directory in PostgreSQL

After the RPMs are installed, you need to initialize the data directory. To do so, you must first create the data directory and you must be the root user. The following example assumes that the data directory is /usr/local/pgsql/data.

Create the /usr/local/pgsql/data directory (using mkdir) and change the ownerships of the directory (using chown and chgrp) so it is owned by the user postgres. Then use su and, as the user postgres, issue the following commands:

```
# mkdir /usr/local/pgsql
# chown postgres /usr/local/pgsql
# chgrp postgres /usr/local/pgsql
# su - postgres
bash-2.05B$ initdb -D /usr/local/pgsql/data
```

The files belonging to this database system will be owned by user “postgres”. This user must also own the server process.

The database cluster will be initialized with locale en_US.UTF-8.
This locale setting will prevent the use of indexes for pattern matching operations. If that is a concern, rerun initdb with the collation order set to “C”. For more information see the Administrator’s Guide.

```
creating directory /usr/local/pgsql/data... ok
creating directory /usr/local/pgsql/data/base... ok
creating directory /usr/local/pgsql/data/global... ok
creating directory /usr/local/pgsql/data/pg_xlog... ok
creating directory /usr/local/pgsql/data/base/1... ok
creating template1 database in /usr/local/pgsql/data/base/1... ok
creating configuration files... ok
initializing pg_shadow... ok
enabling unlimited row size for system tables... ok
initializing pg_depend... ok
creating system views... ok
loading pg_description... ok
creating conversions... ok
setting privileges on built-in objects... ok
vacuuming database template1... ok
copying template1 to template0... ok
```
