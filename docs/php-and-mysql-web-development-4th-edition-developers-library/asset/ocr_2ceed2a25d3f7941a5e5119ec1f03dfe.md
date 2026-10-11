+   `` $h->{TraceLevel} ;``
+   Sets or gets the trace level for the given handle. This attribute provides an alternative to the trace() method.

# H.4.3 MySQL-Specific Database-Handle Attributes

These attributes are specific to the DBI MySQL driver, DBD::mysql. Most of them correspond to a function in the MySQL C API, as indicated in the attribute descriptions. See Appendix G (online) for more information about the C functions.

+   `` $srv = $dbh->{mysql_auto_reconnect} ;``
+   Whether the driver automatically reconnects to the server after the connection goes down. Normally, auto-reconnect is disabled by default, but will be enabled if the GATEWAY_INTERFACE or MOD_PERL environment variables are set. If AutoCommit is disabled, the mysql_auto_reconnect setting is ignored and no reconnects are attempted.

+   `` $hash_ref = $dbh->{mysql_dbd_stats} ;``
+   A hash reference containing driver statistics. Currently this hash has two keys, auto_reconnects_ok and auto_reconnects_failed, indicating the number of times the driver tried successfully and unsuccessfully to reconnect to the server.

+   `` $rv = $dbh->{mysql_errno} ;``
+   The most recent error number, like the mysql_errno() C API function.

+   `` $str = $dbh->{mysql_error} ;``
+   The most recent error string, like the mysql_error() C API function.

+   `` $str = $dbh->{mysql_hostinfo} ;``
+   A string describing the given connection, like the mysql_get_host_info() C API function.

+   `` $str = $dbh->{mysql_info} ;``
+   Information about statements that affect multiple rows, like the mysql_info() C API function.

+   `` $rv = $dbh->{mysql_insertid} ;``
+   The AUTO_INCREMENT value that was most recently generated on the connection associated with $dbh, like the mysql_insert_id() C API function.

+   `` $rv = $dbh->{mysql_protoinfo} ;``
+   A number indicating the client/server protocol version used for the given connection, like the mysql_get_proto_info() C API function.

+   `` $rv = $dbh->{mysql_server_prepare} ;``
+   True if server-side statement preparation is enabled; false if statement preparation is emulated on the client side.