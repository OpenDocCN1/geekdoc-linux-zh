+   version_comment
+   The value of the `--with-comment` option specified to configure at the time the server was built. The default value is "Source distribution" if you don't specify any comment at configuration time.

+   version_compile_machine
+   The compilation machine (hardware type). The value is determined during the configuration process when MySQL is built.

+   version_compile_os
+   The compilation operating system. The value is determined during the configuration process when MySQL is built.

+   wait_timeout (startup; set directly; runtime; global, session)
+   The number of seconds a non-interactive client connection can remain idle before the server considers itself free to close it. For interactive clients, the value of the `interactive_timeout` variable is used instead. This applies only to TCP/IP and Unix socket file connections.

# D.2 Session-Only System Variables

The following list describes system variables that exist in session-only form. That is, each client gets its own set of these variables when it connects to the server, but there are no corresponding global variables. A client that sets any of these variables affects server operation only for itself.

Most of the session-only system variables do not show up in the output from `SHOW VARIABLES`, but you can select the value for each with `SELECT @@SESSION.var_name` or `SELECT @@var_name`.

Session variable names are not case sensitive.

+   autocommit
+   The autocommit mode for transaction processing. This is 1 by default, so autocommit is enabled and statements take effect immediately; essentially, each statement is its own transaction. Setting the value to 0 disables autocommit so that subsequent statements do not take effect until a commit is performed (either with a `COMMIT` statement, or by setting `autocommit` to 1). Statements in the transaction may be canceled with `ROLLBACK` if a commit has not occurred. Setting `autocommit` to 1 re-enables autocommit (and implicitly commits any pending transaction).

+   big_tables
+   All internal temporary tables are stored on disk rather than in memory if this variable is set to 1. Performance is slower, but `SELECT` statements that require large temporary tables will not generate "table full" errors. The default is 0 (hold temporary tables in memory). Normally you need not set this variable.