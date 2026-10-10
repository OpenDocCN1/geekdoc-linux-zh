
Most of the settings in the default my.cnf file define the locations of files and directories needed by the mysqld server. Each option is associated with a particular group, with each group identified by a name in square brackets. The previous options are associated with the mysqld daemon ([mysqld]) and the safe_mysqld script that starts the mysqld daemon ([mysql_safe]). (Refer to Table 23-1 for a list of these groups.)

The default datadir value indicates that /var/lib/mysql is the directory that stores the MySQL databases you create. The socket option identifies /var/lib/mysql/mysql.sock as the socket that is used to create the MySQL server communication end-point associated with the mysqld server. The user option identifies mysql as the user account that has permission to do administration of the MySQL service. Based on the old_passwords=1 value, your MySQL database will use the password format used in previous MySQL 3.x databases.

The log-error and pid-file options tell the safe_mysqld script the locations of the error log (/var/log/mysql.log) and the file that stores the process ID of the mysqld daemon when it is running (/var/run/mysql/mysql.pid). The safe_mysqld script actually starts the mysqld daemon from the mysqld startup script.

The last two sections ([ndbd] and [ndb_mgm]) can be set if you are using MySQL Cluster features. Those entries let you identify the location of the storage daemon (ndbd) and the management tool (ndb_mgm), respectively.

> **NOTE:** Each option that follows a group name is assigned to that group. Group assignments end when a new group begins or when the end of a file is reached.

## Choosing options

Many values are used by the MySQL server that are not explicitly defined in the my.cnf file. The easiest way to see which options are available for MySQL server and clients is to run each command with the --help option. For example, to view the available mysqld options (as well as other information), type the following from a Terminal window:

```
# /usr/libexec/mysqld --verbose --help | less
```

Then press the spacebar to step through the information one screen at a time. (An example of this output is shown in the next section.)

You can also use the man command to find which options are available. For example, to see which options are available to set for the mysqld daemon, type the following:

```
man mysqld
```

It’s quite likely that you can try out your MySQL database server without changing any options at all. However, after you set up your MySQL database server in a production environment, you will almost certainly want to tune the server to match the way the server is used. For example, if it is a dedicated MySQL server, you will want to allow MySQL to consume more of the system resources than it would by default.

The following list shows a few examples of additional options that you might want to set for MySQL:

- **password = yourpwd** — Adding this option to a [client] group in a user's `$HOME/.my.cnf` file allows the user to run MySQL client commands without having to enter a password each time. (Replace *yourpwd* with the user's password.)
- **port = #** — Defines the port number to which the MySQL service listens for MySQL requests. (Replace # with the port number you want to use.) By default, MySQL listens to port number 3306 on TCP and UDP protocols.
- **safe-mode** — Tells the server to skip some optimization steps when the server starts.
- **tmpdir = path** — Identifies a directory, other than the default `/tmp`, for MySQL to use for writing temporary files. (Substitute a full path name for *path*.)

In addition to the options you can set, MySQL clients also have a number of variables you can set. Variables set such things as buffer sizes, timeout values, and acceptable packet lengths. These variables are also listed on the `--help` output. To change a variable value, you can use the `--set-variable` option, followed by the variable name and value. For example, to set the `sort_buffer` variable to 10MB, you could add the following option under your `[mysqld]` group:

```
[mysqld]
set-variable = sort_buffer=10M
```

The following list identifies other variables you could set for your server. In general, raising the values of these variables improves performance, but doing so also consumes more system resources. So you need to be careful raising these values on machines that are not dedicated to MySQL or that have limited memory resources.

> **NOTE:** For variables that require you to enter a size, indicate megabytes using an M (for example, 10M) or kilobytes using a K (for example, 256K).

- **key_buffer_size = size** — Sets the buffer size used for holding index blocks that are used by all threads. This is a key value to raise to improve MySQL performance.
- **max_allowed_packet = size** — Limits the maximum size of a single packet. Raise this limit if you require processing of very large columns.
- **myisam_sort_buffer_size = size** — Sets the buffer size used for sorting while repairing an index, creating an index, or altering a table.
- **sort_buffer = size** — Defines how much buffer size is allocated for each thread that needs to do a sort. Raising this value makes sorting threads go faster.
- **table_cache = #** — Limits the total number of tables that can be open at the same time for all threads. The number of this variable represents the total number of file descriptors that MySQL can have open at the same time.
- **thread_cache_size = size** — Sets the number of threads that are kept in cache, awaiting use by MySQL. When a thread is done being used, it is placed back in the cache. If all the threads are used, new threads must be created to service requests.

## Checking options

In addition to seeing how options and variables are set in the options files, you can also view how all variables are set on your current system. You can view both the defaults and the current values being used by the MySQL server.

The `--help` command-line argument lets you see the options and variables as they are set for the server and for each MySQL client. Here is an example of the output showing this information for the `mysqld` server daemon:

```
# /usr/libexec/mysqld --verbose --help | less
.
.
.
Variables (--variable-name=value)
and boolean options [FALSE|TRUE]   Value (after reading options)
-------------------------------------------------------------
abort-slave-event-count          0
allow-suspicious-udfs            FALSE
auto-increment-increment         1
autocommit-sp-privileges         TRUE
basedir:                         /usr/
.
.
.
tmp table size                   16777216
transaction alloc block_size     8192
transaction prealloc_size        4096
updatable_views_with_limit       1
use-symlink-links                TRUE
verbose                            TRUE
wait timeout                     28800
warnings                         1
To see what values a running MySQL server is using, type
'mysqladmin variables' instead of 'mysqld --verbose --help'
```

After the server has been started, you can see the values that are actually in use by running the `mysqladmin` command with the `variables` option. (Pipe the output to the `less` command so you can page through the information.) Here is an example (if you haven’t stored your password, you will be prompted to enter your password before you see any output):

```
# mysqladmin -u root -p variables | less
```

| Variable_name | Value |
| :--- | :--- |
| auto_increment_increment | 1 |
| auto_increment_offset | 1 |
| autocommit | ON |
| automatic_sp_privileges | ON |
| back_log | 50 |
| basedir | /usr/ |
| ... | ... |
| version | 5.1.39 |
| version_comment | Source distribution |
| version_compile_machine | i386 |
| version_compile_os | redhat-linux-gnu |
| wait_timeout | 28800 |
| warning_count | 0 |

If you decide that the option and variable settings that come with the default MySQL system don’t exactly suit you, you don’t have to start from scratch. Sample my.cnf files that come with the mysql package let you begin with a set of options and variables that are closer to the ones you need.

## Using sample my.cnf files

Sample my.cnf files are available in the /usr/share/doc/mysql-server* directory. To use one of these files, do the following:

1. Keep a copy of the old my.cnf file:
   ```
   # mv /etc/my.cnf /etc/my.cnf.old
   ```
2. Copy the sample my.cnf file you want to the /etc/my.cnf file. For example, to use the my-medium.cnf file, type the following:
   ```
   # cp /usr/share/doc/mysql-server*/my-medium.cnf /etc/my.cnf
   ```
3. Edit the new /etc/my.cnf file (as root user), using any text editor, to further tune your MySQL variables and options.

The following list describes each of the sample my.cnf files.
