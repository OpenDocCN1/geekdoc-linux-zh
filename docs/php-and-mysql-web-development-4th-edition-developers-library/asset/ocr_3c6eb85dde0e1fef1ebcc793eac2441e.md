mysql_com.h lists other CLIENT_XXX values besides those in the preceding list, but those are either unused or intended for internal use, so client programs should not specify them in the flags value.

+   * int
+   mysql_select_db (MYSQL *conn, const char *db_name);

Selects the database named by db_name as the default database, which becomes the default for table references that contain no explicit database specifier. If you do not have permission to access the database, mysql_select_db() fails.
mysql_select_db() is most useful for changing databases within the course of a connection. Normally you will specify the initial database to use when you call mysql_real_connect(), which is faster than calling mysql_select_db() after connecting.
mysql_select_db() returns zero for success, non-zero for failure.

+   * int
+   mysql_set_character_set (MYSQL *conn, const char *cs_name);

Sets the default character set for the connection (as though a SET NAMES statement had been executed). cs_name points to a string containing a character set name.
mysql_set_character_set() returns zero for success, non-zero for failure.
This routine was introduced in MySQL 5.0.7.

+   * my_bool
+   mysql_ssl_set (MYSQL *conn,
+   const char *key,
+   const char *cert,
+   const char *ca,
+   const char *capath,
+   const char *cipher);

This function is used for setting up a secure connection over SSL to the MySQL server. If SSL support is not compiled into the client library, mysql_ssl_set() does nothing. Otherwise it sets up the information required to establish an encrypted connection when you call mysql_real_connect(). (In other words, to set up a secure connection, call mysql_ssl_set() first and then mysql_real_connect().)
mysql_ssl_set() always returns 0; any SSL setup errors will result in an error at the time you call mysql_real_connect().
key is the path to the key file. cert is the path to the certificate file. ca is the path to the certificate authority file. capath is the path to a directory of trusted certificates to be used for certificate verification. cipher is a string listing the cipher or ciphers to use. Any parameter that is unused may be passed as NULL.