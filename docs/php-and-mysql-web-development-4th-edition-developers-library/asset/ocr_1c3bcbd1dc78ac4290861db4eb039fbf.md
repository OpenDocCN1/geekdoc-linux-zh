+   MYSQL_OPT_NAMED_PIPE

Specifies that the connection to the server should use a named pipe. *arg* should be *NULL*. This option is for Windows clients only, and only for connections to Windows servers with named-pipe support enabled.

+   MYSQL_OPT_PROTOCOL

Specifies the protocol to use for connecting to the server, assuming that the server supports the protocol. *arg* should point to an *unsigned int* value containing the protocol code. The allowable codes are *MYSQL_PROTOCOL_MEMORY* (shared memory), *MYSQL_PROTOCOL_PIPE* (Windows named pipe), *MYSQL_PROTOCOL_SOCKET* (Unix socket file), and *MYSQL_PROTOCOL_TCP* (TCP/IP).

+   MYSQL_OPT_READ_TIMEOUT

The timeout for reading from the server, in seconds. This option applies only to TCP/IP connections, and only on Windows before MySQL 5.0.25/5.1.12. *arg* should be a pointer to an *unsigned int* containing the timeout value. The effective timeout is three times the option value due to retries if the initial read fails.

+   MYSQL_OPT_RECONNECT

Enables or disables automatic reconnection behavior if the connection goes down. *arg* should point to a *my_bool* that is set *true* or *false*. Automatic reconnect has been the default since MySQL 5.0.3. This option was introduced in MySQL 5.0.13 to enable control over reconnect behavior.

+   MYSQL_OPT_SET_CLIENT_IP

If the program includes an embedded server that has authentication support, this option causes the server to treat the connection as having originated from the given IP number given by *arg*, which should point to the number specified as a null-terminated string (for example, "*192.168.3.12*").

+   MYSQL_OPT_SSL_VERIFY_SERVER_CERT

Enables or disables verification of the Common Name in the server's certificate. The value must match the hostname used for connecting to the server or the connection attempt fails. This helps prevent man-in-the-middle exploits. *arg* should point to a *my_bool* that is set *true* or *false*. Verification is disabled by default.

This option was introduced in MySQL 5.0.23/5.1.11.

+   MYSQL_OPT_USE_EMBEDDED_CONNECTION

If the program includes an embedded server, this option tells the server library to the embedded server library rather than a remote server. *arg* should be *NULL*.