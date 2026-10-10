
## Checking options

It’s quite likely that you can try out your MySQL database server without changing any options at all. However, after you set up your MySQL database server in a production environment, you will almost surely want to tune the server to match the way the server is used. For example, if it is a dedicated MySQL server, you will want to allow MySQL to consume more of the system resources than it would by default.

The following list shows a few examples of additional options that you might want to set for MySQL:

- `password = yourpwd` — Adding this option to a [client] group in a user’s $HOME/.my.cnf file allows the user to run MySQL client commands without having to enter a password each time. (Replace yourpwd with the user’s password.)
- `port = #` — Defines the port number to which the MySQL service listens for MySQL requests. (Replace # with the port number you want to use.) By default, MySQL listens to port number 3306 on TCP and UDP protocols.
- `safe-mode` — Tells the server to skip some optimization steps when the server starts.
- `tmpdir = path` — Identifies a directory, other than the default /tmp, for MySQL to use for writing temporary files. (Substitute a full path name for path.)

In addition to the options you can set, MySQL clients also have a lot of variables that you can set. Variables set such things as buffer sizes, timeout values, and acceptable packet lengths. These variables are also listed on the `--help` output. To change a variable value, you can use the `--set-variable` option, followed by the variable name and value. For example, to set the sort_buffer variable to 10MB, you could add the following option under your [mysqld] group:

```
[mysqld]
set-variable = sort_buffer=10M
```

The following list identifies other variables you could set for your server. In general, raising the values of these variables improves performance, but also consumes more system resources. So you need to be careful raising these values on machines that are not dedicated to MySQL or that have limited memory resources.

> **NOTE:** For variables that require you to enter a size, indicate Megabytes using an M (for example, 10M) or Kilotytes using an K (for example, 256K).

- `key_buffer_size = size` — Sets the buffer size that is used for holding index blocks that are used by all threads. This is a key value to raise to improve MySQL performance.
- `max_allowed_packet = size` — Limits the maximum size of a single packet. Raise this limit if you require processing of very large columns.
- `myisam_sort_buffer_size = size` — Sets the buffer size used for sorting while repairing an index, creating an index, or altering a table.
- `sort_buffer = size` — Defines how much buffer size is allocated for each thread that needs to do a sort. Raising this value makes sorting threads go faster.
- `table_cache = #` — Limits the total number of tables that can be open at the same time for all threads. The number of this variable represents the total number of file descriptors that MySQL can have open at the same time.
- `thread_cache_size = size` — Sets the number of threads that are kept in cache, awaiting use by MySQL. When a thread is done being used, it is placed back in the cache. If all the threads are used, new threads must be created to service requests.

In addition to seeing how options and variables are set in the options files, you can also view how all variables are set on your current system. You can view both the defaults and the current values being used by the MySQL server.

The `--help` command-line argument lets you see the options and variables as they are set for the server and for each MySQL client. Here is an example of the output showing this information for the `mysqld` server daemon:

```bash
# /usr/libexec/mysqld --verbose --help | less
…
…
…
Variables (--variable-name=value)
and boolean options {FALSE|TRUE}        Value (after reading options)
---------------------------------------  -----------------------
help                                     TRUE
abort-slave-event-count                 0
allow-suspicious-udfs                  FALSE
auto-increment-increment               1
automatic-sp-privileges                TRUE
basedir                                /usr/
…
…
…
tmp_table_size                         33554432
transaction_alloc_block_size           8192
transaction_prealloc_size            4096
updatable_views_with_limit             1
wait_timeout                           28800
```

To see what values a running MySQL server is using, type `mysqladmin variables` instead of `mysqld --verbose --help`. After the server is started, you can see the values that are actually in use by running the `mysqladmin` command with the `variables` option. (Pipe the output to the `less` command so you can page through the information.) Here is an example (if you haven't stored your password, you will be prompted to enter your password before you see any output):

```bash
# mysqladmin -u root -p variables | less

+--------------------------------------+-------------+
| Variable name                        | Value       |
+--------------------------------------+-------------+
| auto_increment_increment             | 1           |
| auto_increment_offset                | 1           |
| autocommit                           | ON          |
| back_log                             | 50          |
| basedir                              | /usr/       |
| bdb_cache_size                       | 8388600     |
| bdb_log_buffer_size                  | 32768       |
| bdb_home_dir                         | /var/lib/mysql/ |
| bdb_max_locks                        | 10000       |
| bdb_logdir                           |             |
| bdb_shared_data                      | OFF         |
| bdb_tmpdir                           | /tmp/       |
| .                                    |             |
| .                                    |             |
| .                                    |             |
| tmp_table_size                       | 33554432    |
| tmpdir                               | /tmp/       |
| version                              | 5.0.45      |
| wait_timeout                         | 28800       |
+--------------------------------------+-------------+
```

If you decide that the option and variable settings that come with the default MySQL system don't exactly suit you, you don't have to start from scratch. Sample my.cnf files that come with the mysql package let you begin with a set of options and variables that are closer to the ones you need.

## Using sample my.cnf files

Sample my.cnf files are available in the `/usr/share/doc/mysql-server*` directory. To use one of these files, do the following:

1. Keep a copy of the old my.cnf file:
   ```bash
   # mv /etc/my.cnf /etc/my.cnf.old
   ```
2. Copy the sample my.cnf file you want to the /etc/my.cnf file. For example, to use the my-medium.cnf file, type the following:
   ```bash
   # cp /usr/share/doc/mysql-server/my-medium.cnf /etc/my.cnf
   ```
3. Edit the new /etc/my.cnf file (as root user) using any text editor to further tune your MySQL variables and options.

The following bullets describe each of the sample my.cnf files.

- **my-small.cnf** — This options file is recommended for computer systems that have less than 64MB of memory and are used only occasionally for MySQL. With this options file, MySQL won't be able to handle a lot of usage but it won't be a drag on the performance of your computer.
  - For the mysqld server, buffer sizes are set low — only 64K for the `sort_buffer` and 16K for the `key_buffer`. The `thread_stack` is set to only 64K and `net_buffer_length` is only 2K. The `table_cache` is set to 4.

- **my-medium.cnf** — As with the small options file, the `my-medium.cnf` file is intended for systems where MySQL is not the only important application running. This system also has a small amount of total memory available — between 32MB and 64MB — but more consistent MySQL use is expected.
  - The `key_buffer` size is set to 16M in this file, while the `sort_buffer` value is raised to 512K for the mysqld server. The `table_cache` is set to 64 (allowing more simultaneous threads to be active). The `net_buffer_length` is raised to 8K.

- **my-large.cnf** — The `my-large.cnf` sample file is intended for computers that are dedicated primarily to MySQL service. It assumes about 512M of available memory.
  - Server buffers allow more active threads and better sorting performance. Half of the system's assumed 512M of memory is assigned to the `key_buffer` variable (256M). The `sort_buffer` size is raised to 1M. The `table_cache` allows more simultaneous users (up to 256 active threads).

- **my-huge.cnf** — As with the `my-large.cnf` file, the `my-huge.cnf` file expects the computer to be used primarily for MySQL. However, the system for which it is intended offers much more total memory (between 1G and 2G of memory).
  - Sort buffer size (`sort_buffer`) is raised to 2M while the `key_buffer` is set to consume 384M of memory. The `table_cache` size is doubled to allow up to 512 active threads.

- **my-innodb-heavy-4G.cnf** — This sample configuration file is best suited for computers with 4GB of RAM that are expected to service complex queries without too many connections (using the InnoDB transaction storage engine). Special `innodb` options in this file allow MySQL to take advantage of a large buffer pool size (2G).

### Starting the MySQL Server

For Fedora and RHEL, the MySQL server is off by default. To turn it on, however, is fairly simple. The `/etc/init.d/mysqld` startup script is delivered with the mysql-server package. To start the server, you can run the `mysqld` startup script to have it start immediately, and then set it to start each time your system boots.
