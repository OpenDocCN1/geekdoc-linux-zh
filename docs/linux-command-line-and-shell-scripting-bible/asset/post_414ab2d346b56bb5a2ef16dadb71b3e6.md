
# Part V Advanced Topics

when the Linux system boots. You can create a link in your distribution's startup script to refer to the MySQL startup script, located at:

```
/usr/local/mysql/support-files/mysql.server
```

This script automatically starts the MySQL server using the Linux user account.

# Securing the MySQL user account

There's one final step for the MySQL server installation. The MySQL server maintains its set of user accounts for controlling access to database objects. By default, the MySQL server has a master administrator called root. Unfortunately, that account doesn't have a password. It's a very good idea to change the password for the root user account. You do this using the mysqladmin command at the Linux command prompt:

```
$ mysqladmin -u root password newpasswd
```

where newpasswd is the text for the new password you're assigning to the root user account.

# The MySQL client interface

The portal to the MySQL database is the mysql command line interface program. This section describes the mysql client program and how to use it to interact with your database.

# Connecting to the server

The mysql client program allows you to connect to any MySQL database server anywhere on the network, using any user account and password. By default, if you enter the mysql program on a command line without any parameters it'll attempt to connect to a MySQL server running on the same Linux system, using the login user name.

Most likely this isn't how you want to connect to the database. There are lists of command parameters that allow you to control only which MySQL you connect to but also the behavior of the mysql interface. Table 24-1 shows the command line parameters you can use with the mysql program.

As you can see, there are quite a lot of command line options available for modifying your log into the MySQL server.

By default, the mysql client program attempts to log in to the MySQL server using your Linux login name. If this name isn't configured in MySQL as a user account, you'll need to use the -u parameter to specify your log in:

```
$ mysql -u root -p
Enter password:
Welcome to the MySQL monitor. Commands end with : or g.
Your MySQL connection id is 7
Server version: 5.0.45 Source distribution
```

Type 'help?' or '\h' for help. Type '\c' to clear the buffer.

```
mysql>
```

# TABLE 24-1

# The mysql Command Line Parameters

| Parameter | Description |
| --- | --- |
| -A | Disable automatic rehashing. |
| -b | Disable beep after error. |
| -B | Don't use a history file. |
| -C | Compress all information sent between the client and the server. |
| -D | Specify the database to use. |
| -e | Execute the specified statement and exit. |
| -E | Display query output vertically, one data field per line. |
| -f | Continue if an SQL error occurs. |
| -G | Enable named SQL commands. |
| -h | Specify the MySQL server hostname (the default is localhost). |
| -H | Display query output in HTML code. |
| -i | Ignore spaces after function names. |
| -N | Don't display column names in results. |
| -o | Ignore statements except for the default database named on the command line. |
| -p | Specify the password for the user account. |
| -P | Specify the TCP port number to use for the network connection. |
| -q | Don't cache each query result. |
| -r | Display column values without escape conversion. |
| -s | Silent mode. |
| -S | Specify a socket for connection to the localhost. |
| -t | Display output in table form. |
| -T | Display debugging information, memory, and CPU statistics when the program exits. |
| -u | Specify the user account to log in. |
| -U | Allow only UPDATE and DELETE statements that specify key values. |
| -v | Verbose mode. |
| -w | If the connection can't be established, wait and retry. |
| -X | Display query output in XHTML code. |

# Part V Advanced Topics

The p parameter tells MySQL to query for a password to use with the user account to log in. Once you're logged into the server, you can start entering commands.

# The mysql commands

The mysql program uses two different types of commands:

- Special mysql commands
- Standard SQL statements

The mysql program uses its own set of commands that let you easily control the environment and retrieve information about the MySQL server. Table 24-2 shows these commands.

You can use either the full command or the shortcut command directly from the mysql prompt:

```
mysql> \s

MySQL Ver 14.12 Distrib 5.0.45, for redhat-linux-gnu (i386) using readline 5.0

Connection: 10
Current database: root@localhost
Current user: Not in use
SSL:
Current pager: stdout
Using outfile:
Using delimiter: :
Server version: 5.0.45 Source distribution
Protocol version: 10
Connection: Localhost via UNIX socket
Server charset: latin1
Db charset: latin1
Client charset: latin1
Conn. charset: latin1
UNIX socket: /var/lib/mysql/mysql.sock
Uptime: 4 hours 15 min 22 sec
```

Threads: 1 Queries: 53 Slow queries: 0 Opens: 23 Flush tables: 1 Open tables: 17 Queries per second avg: 0.003

```
mysql>
```

The mysql program implements all of the standard Structured Query Language (SQL) commands supported by the MySQL server. The “Creating MySQL database objects” section later on discusses this in more detail.

646

# TABLE 24-2

# The mysql Commands

| Command | Shortcut | Description |
| --- | --- | --- |
| ? | \? | Help. |
| clear | \c | Clear command. |
| connect | \r | Connect to database and server. |
| delimiter | \d | Set SQL statement delimiter. |
| edit | \e | Edit the command with the command line editor. |
| ego | \G | Send the command to the MySQL server, and display results vertically. |
| exit | \q | Exit from the mysql program. |
| go | \g | Send command to MySQL server. |
| help | \h | Display help. |
| nopager | \n | Disable pager and send output to STDOUT. |
| note | \t | Don't send output to. |
| output | \t | Append output to file. |
| pager | \P | Set pager command to specified program. |
| print | \p | Print current command. |
| prompt | \R | Change the mysql prompt. |
| quit | \q | Quit from the mysql program (same as exit). |
| refresh | \# | Rebuild command table. |
| source | \. | Execute the SQL script in the specified file. |
| status | \s | Retrieve status information from the MySQL server. |
| system | \! | Execute a shell command on the system. |
| tee | \T | Append all output to the specified file. |
| use | \u | Use another database. |
| charset | \C | Change to another character set. |
| warnings | \W | Show warnings after every statement. |
| nowarning | \w | Don't show warnings after every statement. |

# Advanced Topics

One uncommon SQL command that the mysql program implements is the SHOW command. Using this command you can extract information about the MySQL server, such as the databases and tables created:

```
mysql> SHOW DATABASES;
+----------------------+
| Database             |
+----------------------+
| Information_schema   |
| mysql                 |
+----------------------+
2 rows in set (0.04 sec)

mysql> USE mysql;
Database changed
mysql> SHOW TABLES;
+----------------------+
| Tables_in_mysql     |
+----------------------+
| columns_priv         |
| db                   |
| help_category        |
| help_keyword         |
| help_relation        |
| help_topic          |
| host                 |
| proc                 |
| procs_priv           |
| tables_priv          |
| time_zone            |
| time_zone_leap_second|
| time_zone_name       |
| time_zone_transition |
| time_zone_transition_type|
| user                 |
+----------------------+
17 rows in set (0.00 sec)
```

In this example, I used the SHOW SQL command to display the databases currently configured on the MySQL server, then the USE SQL command to connect to a single database. Your mysql session can only be connected to one database at a time.

You'll notice that after each command I added a semicolon. The semicolon indicates the end of a command to the mysql program. If you don't use a semicolon, it prompts for more data:

```
mysql> SHOW
  -> DATABASES;
```

648
