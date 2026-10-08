(/var/lib/mysql) and log file (/var/log/mysql.log) locations, as well as the server base directory (/var/lib).

+   - The `/var/lib/mysql/my.cnf` file is used for server settings only.

+   - The `.my.cnf` file allows users to customize their access to MySQL. It is located in a user’s home directory. Note that this is a dot file.

Sample configuration **my.cnf** files can be found in the **mysql-server** directory in /usr/share/doc. The **mysql-server** directory lists configurations for small, medium, large, and huge implementations. The administrative manual is located in the **mysql** directory in /usr/share/doc. It is in the info format. Use **info mysql** to start it, and the arrow and **ENTER** keys to move through the menus. Here you can find more information about different options.

# Global Configuration:/etc/my.cnf

MySQL specifies options according to different groups, usually the names of server tools. The options are arranged in group segments. The group name is placed within brackets, and options applied to it follow. The default /etc/my.cnf file is shown here:

```
[mysqld]

datadir=/var/lib/mysql

socket=/var/lib/mysql/mysql.sock

[mysql.server]

user=mysql

basedir=/var/lib

[safe_mysqld]

err-log=/var/log/mysqld.log

pid-file=/var/run/mysqld/mysqld.pid
```

Mysql global options are listed in the /etc/my.cnf file. Options are set up according to groups that control different behaviors of the MySQL server: **mysqld** for the daemon, **mysql.server** for server options, and **safe_mysqld** for the MySQL startup script, **safe_mysqld**. The **datadir** directory, /var/lib/mysql, is where your database files will be placed. Server tools and daemons are located in the **basedir** directory, /var/lib/, and the user that MySQL will run as has the name **mysql**, as specified in the **user** option.

A client group will set up options to be sent to clients, such as the port and socket to use to access the MySQL database.

```
[client]

port=3306

socket=/var/lib/mysql/mysql.sock
```

To see what options are currently set for both client and server, you run **mysqld** directly with the `--help` option.

```
/usr/libexec/mysqld --help
```