It's quite likely that you can try out your MySQL database server without changing any options at all. However, after you set up your MySQL database server in a production environment, you will almost surely want to tune the server to match the way the server is used. For example, if it is a dedicated MySQL server, you will want to allow MySQL to consume more of the system resources than it would by default.

Below are a few examples of options additional options that you may want to set for your MySQL configuration:

+   - **password = yourpwd** — Adding this option to a [client] group in a user's $HOME/.my.cnf file allows the user to run MySQL client commands without having to enter a password each time. (Replace yourpwd with the user's password.)
+   - **port = #** — Defines the port number to which the MySQL service listens for MySQL requests. Replace # with the port number you want to use. By default, MySQL listens to port number 3306 on TCP and UDP protocols.
+   - **safe-mode** — Tells the server to skip some optimization steps when the server starts.
+   - **tmpdir = path** — Identifies a directory, other than the default /tmp, for MySQL to use for writing temporary files. Substitute a full path name for path.

In addition to the options you can set, MySQL clients also have a lot of variables that you can set. Variables set such things a buffer sizes, timeout values, and acceptable packet lengths. These variables are also listed on the --help output. To change a variable value, you can use the --set-variable option, followed by the variable name and value. For example, to set the sort_buffer variable to 10MB, you could add the following option under your [mysqld] group:

```
```
[mysqld]
set-variable = sort_buffer=10M
```
```

The following is a list of other variables you could set for your server. In general, raising the values of these variables improves performance, but does consume more system resources. So you need to be careful raising this value on machines that are not dedicated to MySQL or that have limited memory resources.

> **NOTE:** For variables that require you to enter a size, indicate Megabytes using an M (e.g. 10M) or Kilobytes using a K (e.g. 256K).

+   - **key_buffer_size = size** — Sets the buffer size that is used for holding index blocks that are used by all threads. This is a key value to raise to improve MySQL performance.
+   - **max_allowed_packet = size** — Limits the maximum size of a single packet. Raise this limit if you require processing of very large columns.