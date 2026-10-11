const char *  
`mysql_get_client_info (void)`;

Returns a null-terminated string describing the client library version; for example, `"5.0.60"`.

unsigned long  
`mysql_get_client_version (void)`;

Returns an integer that indicates the client library version. The format of the return value is the same as for `mysql_get_server_version()`.

const char *  
`mysql_get_host_info (MYSQL *conn)`;

Returns a null-terminated string describing the given connection, such as `"Localhost via Unix socket"`, `"cobra.snake.net via TCP/IP"`, `" via named pipe"`, or `"Shared memory"`.

unsigned int  
`mysql_get_proto_info (MYSQL *conn)`;

Returns an integer indicating the client/server protocol version used for the given connection.

const char *  
`mysql_get_server_info (MYSQL *conn)`;

Returns a null-terminated string describing the server version; for example, `"5.0.60-debug-log"`. The value consists of a version number, possibly followed by one or more suffixes. The suffix values are listed in the description of the `VERSION()` function in Appendix C, "Operator and Function Reference."

unsigned long  
`mysql_get_server_version (void)`;

Returns an integer that indicates the server version in `x.yzz` format, where `x`, `yy`, and `zz` represent the major version, release level, and version within the release level. For example, if the version is MySQL 5.1.25, this function returns `50125`.

const char *  
`mysql_info (MYSQL *conn)`;

Returns a null-terminated string containing information about the effect of the most recently executed statement of the following types. The string format is given immediately following each statement:

```
```
ALTER TABLE ...
Records: 0 Duplicates: 0 Warnings: 0
INSERT INTO ... SELECT ...
```
```