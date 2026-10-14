# Managing the Server

The main MySQL server program is called `mysqld`, and it is located in the `/usr/sbin` folder. It normally starts automatically as a background process when you start the Ubuntu server.

MySQL uses a special script, called `mysqld_safe`, to start the MySQL server. This script executes the `mysqld` program, defining several command-line options, such as the location of the database files and the user account that starts the server. It uses the special `mysql` user account created in Ubuntu to run the MySQL server. This helps prevent problems should the MySQL server become compromised, because the `mysql` user account has privileges only to the MySQL database areas on the server.

You should never have to worry about actually running the `mysqld_safe` script in Ubuntu. You can control the MySQL server using the `mysql init.d` script installed in Ubuntu. If you need to shut down or restart the MySQL server by itself, just use one of these formats:

+   - `/etc/init.d/mysql stop`: Stops the server.
+   - `/etc/init.d/mysql restart`: Stops the server, then starts the server.
+   - `/etc/init.d/mysql start`: Starts the server.

> **Secret**
> 
> The `mysql init.d` script uses the standard command-line features of the `mysqld` program to start MySQL. If you need to start the MySQL server without the standard features, such as using an alternative database file, you can use the `mysqld_safe` script directly. Chapter 21 demonstrates this process by using the `mysqld_safe` script to start the MySQL server without the grant tables so that you can change the root password for the MySQL server if you forget it.

MySQL stores data in the `/var/lib/mysql` folder. As discussed in Chapter 21, MySQL has several methods for storing data. Because each method utilizes a different file scheme, you may see several types of files in this folder:

+   - `ibdata1` file: the main data storage file for the InnoDB storage engine
+   - `ib_logfile0` file: stores (logs) SQL statements that process data in the database for the InnoDB storage engine in case of a system crash
+   - `ib_logfile1` file: secondary log for SQL statements
+   - `mysql` folder: contains folders and files for the `mysql` system database, created using the MyISAM storage engine

As discussed in Chapter 21, the InnoDB storage engine in MySQL provides an advanced method for handling database data. The MySQL InnoDB storage engine stores all data in a single file, called the `tablespace`. The `ibdata1` file contains the tablespace. MySQL creates a tablespace file as a large block so that it can add and remove data within the file without having to interact with the operating system to request more space. This feature helps speed up insertion and removal of data from the database. Don't be surprised if you add a lot of new data to a table but don't see the `ibdata1` file size grow.