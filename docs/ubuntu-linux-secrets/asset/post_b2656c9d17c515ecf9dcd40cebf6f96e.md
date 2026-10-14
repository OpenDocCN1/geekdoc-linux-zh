
## Database Server

![](img/39e65eeb4f54001ede08c6114ae3cc6c_608_0.png)

## Secrets in This Chapter

- The MySQL Database
- The PostgreSQL Database
- Using Databases in Ubuntu

The world runs on data. Just about every application you use needs to store data in some form or another. The Ubuntu server provides two popular open-source database servers for your data storage applications. This chapter first looks at the MySQL database server. The MySQL database server is quite possibly the most popular open-source database server available. It’s the database engine behind many popular web sites, and it is used by hobbyists and corporations around the world. The second database server we’ll look at is PostgreSQL. Although not as popular as MySQL, PostgreSQL has gained following in the open-source database world, mostly because of its commercial-quality features. Both of these database servers can be invaluable in your data storage applications.

## The MySQL Server

Chapter 21, "Web Server," described the MySQL database server and showed the basics of how to use it as part of the Linux-Apache-MySQL-PHP (LAMP) environment. This section digs deeper into the operation of the MySQL database server, showing the files that the MySQL server needs to operate and walking through the mysql command-line interface, which provides a simple environment for interacting with your MySQL database server.

If you didn’t install the LAMP server on your Ubuntu server, or if you want to install MySQL on your Ubuntu workstation, you can do so using either the apt-get program or the Synaptic Package Manager (see Chapter 13, "Software Installs and Updates").

The MySQL server package comes as two main packages, with a number of dependent packages. The mysql-client package installs the application necessary to connect to a MySQL server, while the mysql-server package installs the MySQL server itself. The easiest way to install a complete MySQL environment on your Ubuntu system is to install the mysql package. It includes all of the client and server packages as dependencies.

## The MySQL Server Files

The Ubuntu server installs the MySQL database server package by default when you install the LAMP server. Four components to the MySQL database server software package are installed:

- The MySQL server program
- Configuration files for setting features that control the operation of the server
- Database files used to store the data elements (databases, tables, data fields, and user accounts) managed by MySQL
- Scripts and executable programs used to interact with the database server

The following sections walk through the various files that the Ubuntu server installation process provides to run and manage the MySQL database server.

## Managing the Server

The main MySQL server program is called `mysqld`, and it is located in the `/usr/sbin` folder. It normally starts automatically as a background process when you start the Ubuntu server.

MySQL uses a special script, called `mysqld_safe`, to start the MySQL server. This script executes the `mysqld` program, defining several command-line options, such as the location of the database files and the user account that starts the server. It uses the special `mysql` user account created in Ubuntu to run the MySQL server. This helps prevent problems should the MySQL server become compromised, because the `mysql` user account has privileges only to the MySQL database areas on the server.

You should never have to worry about actually running the `mysqld_safe` script in Ubuntu. You can control the MySQL server using the `mysql init.d` script installed in Ubuntu. If you need to shut down or restart the MySQL server by itself, just use one of these formats:

- `/etc/init.d/mysql stop`: Stops the server.
- `/etc/init.d/mysql restart`: Stops the server, then starts the server.
- `/etc/init.d/mysql start`: Starts the server.

> **Secret**
> 
> The `mysql init.d` script uses the standard command-line features of the `mysqld` program to start MySQL. If you need to start the MySQL server without the standard features, such as using an alternative database file, you can use the `mysqld_safe` script directly. Chapter 21 demonstrates this process by using the `mysqld_safe` script to start the MySQL server without the grant tables so that you can change the root password for the MySQL server if you forget it.

MySQL stores data in the `/var/lib/mysql` folder. As discussed in Chapter 21, MySQL has several methods for storing data. Because each method utilizes a different file scheme, you may see several types of files in this folder:

- `ibdata1` file: the main data storage file for the InnoDB storage engine
- `ib_logfile0` file: stores (logs) SQL statements that process data in the database for the InnoDB storage engine in case of a system crash
- `ib_logfile1` file: secondary log for SQL statements
- `mysql` folder: contains folders and files for the `mysql` system database, created using the MyISAM storage engine

As discussed in Chapter 21, the InnoDB storage engine in MySQL provides an advanced method for handling database data. The MySQL InnoDB storage engine stores all data in a single file, called the `tablespace`. The `ibdata1` file contains the tablespace. MySQL creates a tablespace file as a large block so that it can add and remove data within the file without having to interact with the operating system to request more space. This feature helps speed up insertion and removal of data from the database. Don't be surprised if you add a lot of new data to a table but don't see the `ibdata1` file size grow.
