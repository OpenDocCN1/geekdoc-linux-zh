
server name, a colon, and the VNC session number. For instance, you might type the following command:

```
$ vncviewer bluebox.luna.edu:1
VNC server supports protocol version 3.8 (viewer 3.3)
Password:
```

If you type the correct password, `vncviewer` displays more text in your terminal and opens a window displaying the remote computer's desktop. VNC clients are also available for many other OSs; check the original VNC or the TightVNC Web sites for these clients. These non-Linux VNC clients work much like the Linux VNC client, but they emphasize dialog boxes for entering the server's hostname and password.

One important drawback of VNC is that the user must ordinarily launch the VNC server from the server computer before running the VNC client program from the client computer. In some cases, this requirement isn't a major issue. For instance, if you're sitting at a workstation and know you'll want to use it from another location in the near future, you can launch the server before leaving the workstation. In other cases, though, you may need to log into the VNC server computer using a text-mode login tool in order to launch the VNC server. This procedure requires two logins, which is a nuisance. What's more, this means you must run two login protocols on the server computer, increasing its security exposure.

## Deploying MySQL

The Structured Query Language (SQL), as its expanded name suggests, is a language used for retrieving data from a database. In practice, SQL is implemented in several different database products. Thus, you should know a little about the SQL products that are available for Linux. With a SQL package installed, you can begin learning about the principles of SQL use and run a SQL product.

### Picking a SQL Package

SQL is a language for accessing data, and specific SQL packages implement that language. This distinction is similar to that between a network protocol (such as SMTP) and the servers that implement it (such as sendmail and Postfix). In principle, you can use any SQL package to satisfy your SQL database needs. In practice, specific products that store data using SQL may work better with (or even require) particular packages. Some of the more common choices in Linux include the following:

- **MySQL**: Sun owns this SQL implementation, which it has released under the GPL. Most major Linux distributions include MySQL in their package databases. For a complete installation, you'll probably need to install multiple packages, such as a client, a server, and perhaps development tools. You can learn more at http://www.sun.com/software/products/mysql/.
- **PostgreSQL**: This SQL implementation evolved from the earlier Ingres software (the name *PostgresSQL* is a compressed form of *post-Ingres SQL*). It’s available under the BSD license and is available as multiple packages in most Linux distributions. As with MySQL, you’ll most likely have to install a client, a server, and perhaps additional support packages. PostgreSQL is headquartered at http://www.postgresql.org.
- **SQLite**: This package, based at http://www.sqlite.org, is a library that implements SQL. As such, it’s not a stand-alone database; instead, it’s intended as a way to provide programs with access to SQL database features within the program. If you install a program that uses SQLite, your distribution’s package manager should install the relevant libraries for you. If you want to write a program that requires database access and you don’t want to install a complete client-server SQL package such as MySQL or PostgreSQL, SQLite may be just what you need.

There are dozens more SQL database products for Linux. For the purpose of learning SQL, MySQL or PostgreSQL should do fine, or you can use another full implementation if you prefer. If you have a specific purpose in mind for using SQL, though, you should research SQL packages in more detail. You may need a particular product for compatibility with other software, or you may need a SQL package that provides specific features. The Linux+ objectives mention only MySQL by name.

As just noted, some SQL packages, including MySQL and PostgreSQL, operate on a client-server model: one program (the server) manages the database, while another (the client) provides users and programs with access to the database. Such implementations can work over a network, enabling users at multiple client systems to access a centralized database server.

## Using MySQL

To learn about SQL, you should have access to a SQL database. For purposes of demonstration, I’m using MySQL as a reference. Other SQL implementations are similar to what I describe here, but some details differ. From an administrative perspective, you need to know how to set MySQL configuration options, how to start and stop the server, and how to test that it’s working. Actually performing database queries with MySQL is a complex topic that’s beyond the scope of this book or the Linux+ exam.

## Configuring, Starting, and Stopping MySQL

MySQL’s main configuration file is called *my.cnf*, and it’s usually stored in `/etc` or `/etc/mysql`. You should peruse this file to familiarize yourself with some of the key MySQL options. Unless you know you need to change the defaults, though, you should be cautious about changing this file’s contents, at least initially.

One initial configuration task you must perform is to set the MySQL root password. Just like Linux itself, MySQL requires an administrative (root) user; however, MySQL’s root isn’t the same as the Linux root account. A default MySQL installation is likely to require no password for administrative access. To enable a password, type the following command:

```
$ mysqladmin -u root password newpassword
```

Change `newpassword` to the password you want to use, of course. If your system already has a root password set, you can change it with another command:

```
$ mysqladmin -u root -p'oldpassword' password newpassword
```

![](img/a78bc63f22351f522ba5ec1fa0c060d2_540_0.png)

Some distributions, such as Ubuntu, include installation scripts that prompt you to enter a MySQL root password when you install the software. Thus, you might not need to type these commands.

Typically, MySQL is started and stopped using SysV startup scripts, such as `/etc/init.d/mysqlld`. Chapter 4 describes SysV startup scripts in more detail, so consult it if you need help starting or stopping MySQL. You can verify that MySQL is running using `ps`; search for a process called `mysqlld`:

```
# ps ax | grep mysql
1948 ? S 0:00 /bin/sh /usr/bin/mysqlld_safe
2013 ? S1 33:30 /usr/sbin/mysqlld --basedir=/usr --datadir=/var/lib/mysql --user=mysql --pid-file=/var/run/mysqlld/mysqlld.pid --skip-locking --port=3306 --socket=/var/run/mysqlld/mysqlld.sock
2014 ? S 0:00 logger -p daemon.err -t mysqlld_safe -i -t mysqlld
30933 pts/0 S+ 0:00 grep mysql
```

In this example, the `/usr/sbin/mysqlld` program is the MySQL server, so it's definitely running. This output also shows the options used to launch the program. Three other MySQL-related processes were also found by this query, including the `grep` command used to search for MySQL. Be sure that you find `mysqlld` (the daemon, whose name ends in `d`); the `mysql` program is the client, and it could be running even if the server isn't running. If you can't find the MySQL daemon running, try using its SysV startup script, and if that fails, search your log files for clues to what might be going wrong when you try to launch the server.

### Testing the MySQL Connection

To test MySQL's basic operation, you should first ensure that the server is running, as just described. You can then start the SQL client. In the case of MySQL, this program is called `mysql`:

```
$ mysql
```

If the client can connect to a server, you’ll see a `mysql>` prompt. If the server isn’t running or can’t be contacted, you’ll see an error message. To verify the status of the `mysql` client connection to its server, you can use the `STATUS` command:

```
mysql> STATUS;
---------------
mysql  Ver 14.12 Distrib 5.0.51a, for debian-linux-gnu (x86_64) using readline 5.2
Connection id:		29
```

Several additional lines of status information will appear, as well. You can peruse these to learn a few more details, such as what version of the server is in use and how long it has been running.

If you’ve just installed MySQL, it may have no databases defined. To learn what’s defined, you can use the `SHOW DATABASES` command:

```
mysql> SHOW DATABASES;
+--------------------+
| Database         |
+--------------------+
| information_schema |
+--------------------+
1 row in set (0.00 sec)
```

These operations should be more than sufficient to verify basic functioning of MySQL. You might not get in so easily, though, particularly if you use a computer other than the one on which the MySQL server is running to test the server’s operation. (If network operation is important in your installation, you should definitely test network access to ensure that firewalls or other network issues won’t cause problems.) If you receive a `Can’t connect to MySQL server` message, chances are either the MySQL server isn’t running or a network configuration is blocking access to the server. If you receive an `Access denied` message, the problem is with authentication—you must specify a legal account and password.

To connect to a remote server, use a particular MySQL account, or send a particular MySQL password, you must use the `--host` (or `-h`), `--user` (or `-u`), or `--password` (or `-p`) options, respectively. For instance, to connect to the MySQL server running on `third.luna.edu` as `dbuser` with a password of `e4blug7IQ`, you might type the following:

```
$ mysql --host=third.luna.edu -u dbuser -pe4blug7IQ
```
