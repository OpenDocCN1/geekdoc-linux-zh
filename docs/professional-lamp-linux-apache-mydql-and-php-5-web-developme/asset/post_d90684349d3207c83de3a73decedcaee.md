
iconv_mime_encode(): Creates a MIME header field.

iconv_strlen(): Returns the character count of a string.

iconv_strpos(): Finds the position of the first occurrence of a named character within a string.

iconv_strrpos(): Finds the position of the last occurrence of a named character within the specified range of a string.

iconv_substr(): Returns a portion of a string.

idate(): Formats a local time/date as an integer.

imagefilter(): Applies a named filter to an image.

image_type_to_extension(): Returns an image file’s extension.

imap_getacl(): Returns the ACL for a given mailbox.

ldap_sasl_bind(): Binds a resource to the LDAP directory using SASL.

mb_list_encodings(): Returns an array of all supported encodings.

pcntl_getpriority(): Returns the priority of a pid.

pcntl_wait(): Pauses the current process until a child process has exited and returns the child process’s id.

pg_version(): Returns the client, protocol, and server version in an array.

php_strip_whitespace(): Removes comments, whitespace, and newlines from source code and returns the result.

proc_nice(): Alters the priority of the current process by a given increment.

pspell_config_data_dir(): Sets the location of language data files.

pspell_config_dict_dir(): Sets the location of the main word list.

setrawcookie(): Equivalent to setcookie() without a URL encode of the value.

snmp_read_mib(): Reads and parses a MIB file into the active MIB tree.

sqlite_fetch_column_types(): Returns applicable column types from a given table.

str_split(): Splits a string into an array of characters.

stream_copy_to_stream(): Copies data between streams and returns the amount of data copied.

stream_get_line(): Similar to fgets() but allows named delimiter.

stream_socket_accept(): Accepts a connection on a socket created from a previous use of the stream_socket_server() function.

stream_socket_client(): Opens a stream to an Internet or Unix domain destination.

stream_socket_get_name(): Returns the name of the socket connection.

stream_socket_recvfrom(): Receives data from a socket up to a specified length.

stream_socket_sendto(): Sends data to a specified socket, whether it is connected or not.

stream_socket_server(): Creates a stream on the specified server.

## Chapter 1

- `strpos()`: Searches a string for any of a list of given characters, and returns the remainder of the string from the first instance of success.
- `substr_compare()`: Compares two strings with named offset and optional case sensitivity.
- `time_nanosleep()`: Delays execution of the script for a number of seconds and nanoseconds.

More information about these functions can be found at the source, http://www.php.net.

### Other Changes to PHP5

Besides the laundry list of OOP changes and the multitude of new functions available, there are also other improvements that have been made in the release of PHP5.

### Configuration Changes

In PHP5 there are numerous changes to the php.ini configuration file. These are discussed in greater detail in Chapter 5, but here is a list for your reference:

- mail.force_extra_parameters
- register_long_arrays
- session.hash_function
- session.hash_bits_per_character
- zend.zel_compatibility_mode

With these new directives, you can exert a little more control over your PHP environment, which gives you a little more freedom in coding.

### MySQLi

MySQLi, as you well know, fits well with PHP in delivering database-driven dynamic websites. Thus, it is the release of the MySQLi (MySQL improved) extension that makes life easier for everyone.

### Configuration Settings

There are several new MySQLi configuration settings available in php.ini. Here’s a brief description:

- `mysqli.max_links`: Sets the maximum number of MySQL connections per process.
- `mysqli.default_port`: Sets the default TCP/IP port to connect to the MySQL server.
- `mysqli.default_socket`: Sets the default socket name for connecting to the MySQL server.
- `mysqli.default_host`: Sets the default hostname for connecting to the MySQL server.
- `mysqli.default_user`: Sets the default username for connecting to the MySQL server.
- `mysqli.default_pw`: Sets the default password for connecting to the MySQL server.

What's New in PHP5?

#### Built-in Classes and Properties

With the mysqli extension comes a new set of built-in classes and properties that you can access in your PHP scripts. These new methods can also be used as functions if your script is procedural in nature as opposed to being object-oriented. To call the functions procedurally, simply use the syntax mysqli_ before the method name. For example, to create a new connection using OOP, you would type the following:

```php
<?php
$connect = new mysqli("server", "user", "pass", "dbname");
//call methods through the mysqli class
$connect->close();
?>
```

To accomplish the same thing using traditional procedural programming, you would type the following:

```php
<?php
$connect = mysqli_connect ("server", "user", "pass", "dbname");
//call functions using mysqli_ prefix
mysqli_close($connect);
?>
```

The following sections describe the type of functions inherent in PHP5.

##### class mysqli

This class addresses a basic MySQL connection. The constructor of this class creates a new PHP/MySQL connection, and thus a new mysqli object. You would use this class to manipulate or retrieve information about the current connection, or perform basic query functions.

The methods available to this class are:

- auto_commit: Toggles whether or not transactions are automatically committed to the database.
- change_user: Switches to another user.
- character_set_name: Returns the default character set.
- close: Closes a database connection.
- commit: Commits a transaction to the database.
- connect: Opens a new connection to MySQL database server (also the mysqli constructor).
- debug: Uses the Fred Fish debugging library to debug.
- dump_debug_info: Uses the Fred Fish debugging library to dump debugging information.
- get_client_info: Retrieves information about the client.
- get_host_info: Retrieves information about the connection.
- get_server_info: Retrieves information about the MySQL server.
- get_server_version: Retrieves the current MySQL server version.
- info: Returns information about the most recently executed query.
- init: Initializes an object prior to calling the real_connect function.
- kill: Kills a MySQL thread.
- more_results: Looks for results from previously called multi_query.
- multi_query: Executes one or more queries.
- next_result: Returns the next result from previously called multi_query.
- options: Changes or sets connection options for real_connect object.
- ping: Pings a server connection or reconnects if there is no connection.
- prepare: Prepares a single SQL query statement for execution.
- query: Executes a query.
- real_connect: Connects to the MySQL database server and allows for additional options or parameters to be set.
- real_escape_string: Returns an escaped string for valid use in an SQL statement.
- rollback: Rolls back the current transaction.
- select_db: Selects the named database as active.
- set_charset: Sets the character set to be used.
- ssl_set: Sets SSL parameters, enabling a secure connection.
- stat: Returns information about the system status.
- stmt_init: Initializes a statement for use with mysqli_stmt_prepare.
- store_result: Transfers a resultset from last query.
- thread_safe: Returns whether thread safety is given or not.
- use_result: Transfers an unbuffered resultset from last query.

The properties available to this class are as follows:

- affected_rows: Gets the number of affected rows in a previous MySQL operation.
- client_info: Returns the MySQL client version as a string.
- client_version: Returns the MySQL client version as an integer.
- errno: Returns the error code for the most recent function call.
- error: Returns the error string for the most recent function call.
- field_count: Returns the number of columns for the most recent query.
