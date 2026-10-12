
**TIP:** To save yourself the trouble of typing in the password each time you run a MySQL client command, you can add a password option under the `[client]` group in one of the option files. The most secure way to do that is to create a `.my.cnf` file in the root user's home directory that contains the following lines (substituting your password for the last argument shown).

```
[client]
    password=my47gmc
```

## Setting MySQL options

You can set options that affect how the MySQL applications behave by using options files or command-line arguments. The MySQL server (as well as other administrative tools) reads the following options files when it starts up (if those files exist):

- `/etc/my.cnf` — Contains global options read by **mysqld** (server daemon) and **mysql.server** (script to start the server daemon).
- `/var/lib/mysql/my.cnf` — Contains options that are intended primarily for the **mysqld** server daemon.
- `--defaults-extra-file` — You can identify a file on the command line that contains options to be used by the server. For example, the following command would cause the file `/home/jim/.my.cnf` to be read for options after the global options and before the user-specific options:
  ```text
  # mysqld --defaults-extra-file=/home/jim/my.cnf
  ```
- `$HOME/.my.cnf` — Contains user-specific options. (The `$HOME` refers to the user's home directory, such as `/home/susyq`.)

Table 24-1 shows the MySQL commands that read the options files (in the order shown in the previous bullet list) and use those options in their processing. Options are contained within groups that are identified by single words within brackets. Group names that are read by each command are also shown in the table.

### Table 24-1: Option Groups Associated with MySQL Commands

| Command | Description | Group names |
| :--- | :--- | :--- |
| **mysqld** (in `/usr/libexec`) | The MySQL server daemon. | `[mysqld]`<br>`[server]` |
| **mysql.server** (in `/usr/share/mysql`) | Used as the start-up script to start and stop the MySQL daemon. (Red Hat Linux uses `/etc/init.d/mysqld` instead.) | `[mysql]`<br>`[server]`<br>`[mysql.server]` |
| **safe_mysqld** | Run by the `mysql` start-up script to start the MySQL server. | `[mysql]`<br>`[server]`<br>`[mysql.server]` |
| **mysql** | Offers a text-based interface for displaying and working with MySQL databases. | `[mysql]`<br>`[client]` |
| **mysqladmin** | Used to create and maintain MySQL databases. | `[mysqladmin]`<br>`[client]` |
| **isamchk** | Used to check, fix, and optimize ISAM databases (.ism suffix). | `[isamchk]` |
| **myisamchk** | Used to check, fix, and optimize MyISAM databases (.myi suffix). | `[myisamchk]` |
| **pack_isam** | Used to pack ISAM databases (.ism suffix). | `[pack_isam]` |
| **myisampack** | Used to compress MyISAM database tables. | `[myisampack]` |
| **mysqldump** | Offers a text-based interface for backing up MySQL databases. | `[mysqldump]`<br>`[client]` |
| **mysqlimport** | Loads plain-text data files into MySQL databases. | `[mysqlimport]`<br>`[client]` |
| **mysqlshow** | Shows MySQL databases and tables you select. | `[mysqlshow]`<br>`[client]` |

Though you can use any of the options files to set your MySQL options, begin by configuring the `/etc/my.cnf` file. Later, if you want to override any of the values set in that file you can do so using the other options files or command-line arguments.

## Creating the my.cnf configuration file

Global options that affect how the MySQL server and related client programs run are defined in the `/etc/my.cnf` file. The default `my.cnf` file contains only a few settings needed to get a small MySQL configuration going. The following is an example of the `/etc/my.cnf` file that comes with MySQL:

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

Most of the settings in the default `my.cnf` file define the locations of files and directories needed by the `mysqld` server. Each option is associated with a particular group, with each group identified by a name in square brackets. The above options are associated with the `mysqld` daemon (`[mysqld]`), the MySQL server (`[mysql.server]`), and the `safe_mysqld` script that starts the `mysqld` daemon (`[safe_mysqld]`). (See Table 24-1 for a list of these clients.)

The default `datadir` value indicates that `/var/lib/mysql` is the directory that stores the `mysql` databases you create. The `socket` option identifies `/var/lib/mysql/mysql.sock` as the socket that is used to create the MySQL communications end-point associated with the `mysqld` server. The `basedir` option identifies `/var/lib` as the base directory in which the `mysql` software is installed. The `user` option identifies `mysql` as the user account that has permission to do administration of the MySQL service.

The `err-log` and `pid-file` options tell the `safe_mysqld` script the locations of the error log (`/var/log/mysqld.log`) and the file that stores the process ID of the `mysqld` daemon when it is running (`/var/run/mysqld/mysqld.pid`). The `safe_mysqld` script actually starts the `mysqld` daemon from the `mysqld` start-up script.

> **NOTE:** Each option that follows a group name is assigned to that group. Group assignments end when a new group begins or when the end of file is reached.

## Choosing options

There are many values that are used by the MySQL server that are not explicitly defined in the `my.cnf` file. The easiest way to see which options are available for MySQL server and clients is to run each command with the `--help` option. For example, to see available `mysqld` options (as well as other information) type the following from a Terminal window:

```
# /usr/libexec/mysqld --help | less
```

Then press the spacebar to step through the information one screen full at a time.

Another way to find what options are available is with the `man` command. For example, to see which options are available to set for the `mysqld` daemon, type the following:

It's quite likely that you can try out your MySQL database server without changing any options at all. However, after you set up your MySQL database server in a production environment, you will almost surely want to tune the server to match the way the server is used. For example, if it is a dedicated MySQL server, you will want to allow MySQL to consume more of the system resources than it would by default.

Below are a few examples of additional options that you may want to set for your MySQL configuration:

- **password = yourpwd** — Adding this option to a `[client]` group in a user's `$HOME/.my.cnf` file allows the user to run MySQL client commands without having to enter a password each time. (Replace `yourpwd` with the user's password.)
- **port = #** — Defines the port number to which the MySQL service listens for MySQL requests. Replace `#` with the port number you want to use. By default, MySQL listens to port number 3306 on TCP and UDP protocols.
- **safe-mode** — Tells the server to skip some optimization steps when the server starts.
- **tmpdir = path** — Identifies a directory, other than the default `/tmp`, for MySQL to use for writing temporary files. Substitute a full path name for `path`.

In addition to the options you can set, MySQL clients also have a lot of variables that you can set. Variables set such things as buffer sizes, timeout values, and acceptable packet lengths. These variables are also listed on the `--help` output. To change a variable value, you can use the `--set-variable` option, followed by the variable name and value. For example, to set the `sort_buffer` variable to 10MB, you could add the following option under your `[mysqld]` group:

```
[mysqld]
set-variable = sort_buffer=10M
```

The following is a list of other variables you could set for your server. In general, raising the values of these variables improves performance, but does consume more system resources. So you need to be careful raising this value on machines that are not dedicated to MySQL or that have limited memory resources.

> **NOTE:** For variables that require you to enter a size, indicate Megabytes using an M (e.g. 10M) or Kilobytes using a K (e.g. 256K).

- **key_buffer_size = size** — Sets the buffer size that is used for holding index blocks that are used by all threads. This is a key value to raise to improve MySQL performance.
- **max_allowed_packet = size** — Limits the maximum size of a single packet. Raise this limit if you require processing of very large columns.
