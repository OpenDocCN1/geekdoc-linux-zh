The regular client library includes versions of *mysql\_library\_init*() and *mysql\_library\_end*() that perform initialization and finalization appropriate to client/server communication rather than to communication with an embedded server.

# 7.8 Using Multi-Statement Execution

The MySQL client library supports multiple-statement execution capability. This enables you to send a string to the server consisting of multiple statements separated by semi-colons, and then retrieve the result sets one after the other.

Multiple-statement execution is not enabled by default, so you must tell the server that you want to use it. There are two ways to do this. The first is to add the *CLIENT\_MULTI\_STATEMENTS* option in the *flags* argument to *mysql\_real\_connect*() at connect time:

```
```C
opt_flags |= CLIENT_MULTI_STATEMENTS;
if (mysql_real_connect (conn, opt_host_name, opt_user_name, opt_password,
    opt_db_name, opt_port_num, opt_socket_name, opt_flags) == NULL)
{
    print_error (conn, "mysql_real_connect() failed");
    mysql_close (conn);
    exit (1);
}
```
```

The other is to use *mysql\_set\_server\_option*() to enable the capability for an existing connection. For example:

```
```C
if (mysql_set_server_option (conn, MYSQL_OPTION_MULTI_STATEMENTS_ON) != 0)
    print_error (conn, "Could not enable multiple-statement execution");
```
```

Which method is preferable? If the program does not use stored procedures, either one is suitable. If the program does use stored procedures and invokes a CALL statement that returns a result set, the first method is better. That's because *CLIENT\_MULTI\_STATEMENTS* also turns on the *CLIENT\_MULTI\_RESULTS* option, which must be enabled or an error occurs if a stored procedure attempts to return a result. (More preferable yet might be to add *CLIENT\_MULTI\_RESULTS* to the *flags* argument to *mysql\_real\_connect*(), because that makes it explicit that you're enabling the option.)

Two functions provide the basis for checking the current status of result retrieval when you're processing multiple result sets:

+   - *mysql\_more\_results*() returns non-zero if more results are available and zero otherwise.
+   - *mysql\_next\_result*() returns a status and also initiates retrieval of the next set if more results are available. The status is zero if more results are available, -1 if not, and a value greater than zero if an error occurred.

You can use these functions by putting your result-retrieval code inside a loop. After retrieving a result with your usual code, check whether there are any results yet to be