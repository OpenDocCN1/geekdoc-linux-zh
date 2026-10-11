MySQL programs check the following environment variables:

+   *   `MYSQL_DEBUG`
+   
+       The options to use when debugging. This variable has no effect unless MySQL
+       was built with debugging support enabled. Setting `MYSQL_DEBUG` is like using the
+       `--debug` option.
+   
+   *   `MYSQL_PWD`
+   
+       The password to use when establishing connections to the MySQL server. Setting
+       `MYSQL_PWD` is like using the `--password` option.
+   
+       Using the `MYSQL_PWD` variable to store a password constitutes a security risk because
+       other users on your system can easily discover its value. For example, the `ps` utility
+       shows environment variable settings for other users.
+   
+   *   `MYSQL_TCP_PORT`
+   
+       For `mysqld`, this is the port on which to listen for TCP/IP connections. For client
+       programs, this is the port number to use when establishing a TCP/IP connection to
+       the server. Setting `MYSQL_TCP_PORT` is like using the `--port` option.
+   
+   *   `MYSQL_UNIX_PORT`
+   
+       For `mysqld`, this is the socket file on which to listen for local connections. For
+       client programs, this is the pathname of the Unix socket file to use when establish-
+       ing socket file connections to the server running on `localhost`. Setting
+       `MYSQL_UNIX_PORT` is like using the `--socket` option.
+   
+   *   `TMPDIR`
+   
+       The pathname of the directory in which to create temporary files. Setting this vari-
+       able is like using the `--tmpdir` option. However, although `mysqladmin` and `mysqld`
+       understand a value containing a list of directories for `--tmpdir`, do not set `TMPDIR`
+       that way. Other non-MySQL programs that do not understand the list-of-
+       directories convention also use `TMPDIR`.
+   
+   *   `USER`
+   
+       This is the MySQL username to use when connecting to the server. This variable is
+       used only by client programs running under Windows or NetWare; setting it is like
+       using the `--user` option.

The `mysql` client checks the value of three additional environment variables:

+   *   `MYSQL_HISTFILE`
+   
+       On Unix, the name of the file to use for storing command-line history during in-
+       teractive use. The default value if this variable is not set is `$HOME/.mysql_history`,
+       where `$HOME` is the location of your home directory.
+   
+   *   `MYSQL_HOST`
+   
+       The host to connect to when establishing a connection to the MySQL server. Set-
+       ting this variable is like using the `--host` option.