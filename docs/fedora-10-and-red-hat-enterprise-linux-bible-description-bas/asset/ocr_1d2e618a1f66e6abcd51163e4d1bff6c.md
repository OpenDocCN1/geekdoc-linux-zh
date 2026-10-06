# Part IV: Fedora and RHEL Network and Server Setup

It's quite likely that you can try out your MySQL database server without changing any options at all. However, after you set up your MySQL database server in a production environment, you will almost surely want to tune the server to match the way your server is used. For example, if it is a dedicated MySQL server, you will want to allow MySQL to consume more of the resources than it would by.

The following list shows a few examples of additional options that you might want to set for MySQL:

+   * **password = yourpwd** — Adding this option to a [client] group in a user's $HOME/.cnf file allows the user to run MySQL commands without having to enter a password each time. (Replace yourpwd with the user's password)
* **port #** — Defines the port number to the MySQL service listens for requests. (Replace # with the port number you want to use.) By default, MySQL listens on port 3306 for TCP and UDP protocols.
* **safe-mode — Tells the server to skip optimization steps when the server starts.
* **tmpdir = path** — Identifies a directory, other than the default /tmp, for MySQL to use for writing temporary files. (Substitute with a full path for path*)

In addition to the options you can set, MySQL clients also have a lot of variables that you can set. Variables set such as buffer sizes, timeout values, and acceptable packet lengths. These variables are also listed by the --help output. To change a variable value, you can use the --set-variable option, defined by the variable name and value. For example, to set the sort_buffer variable to 10MB, you could add the following option under your [mysql] group:

```
[mysql]
set-variable = sort_buffer=10M
```

The following list identifies other variables you could set for your server. In general, raising the values of these variables improves performance, but also consumes more system resources. So you need to be careful raising these values on machines that are not dedicated to MySQL or have limited memory resources.

> NOTE: For variables that require you to enter a size, indicate Megabytes by an M (for example, 10M) or Kilobytes by a K (for example, 256K).

+   * **key_buffer_size = size** — Sets the buffer size that is used for holding index blocks that are used by all threads. This is a key value to raise MySQL performance.
* **max_allowed_packet = size** — Limits the maximum size of a packet. Raise this limit if you require processing of very large columns.
* **myisam_buffer_size = size** — Sets the buffer size used for sorting while repairing an index, creating an index, or altering a table.