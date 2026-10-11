+   - `--skip-line-numbers`, `-L`
+   See the description for `--line-numbers`. The `-L` form of this option is deprecated.

+   - `--table`, `-t` *(boolean)*
+   Produces output in tabular format, with values in each row delimited by bars and lined up vertically. This is the default output format when `mysql` is not run in batch mode.

+   - `--tee=file_name`
+   Appends a copy of all output to the named file. Output copying can be disabled with `--skip-tee`. This option does not work in batch mode.

+   - `--unbuffered`, `-n` *(boolean)*
+   After each statement, flushes the buffer used for communication with the server.

+   - `--vertical`, `-E`
+   Prints query results vertically—that is, with each row of a query result displayed as a set of output lines, one column per line. (Each line consists of a column name and value.) The display for each row is preceded by a line indicating the row number within the result set. Vertical display format may be useful when a query produces very long lines.
+   If this option is not specified, you can enable vertical display format for individual queries by terminating them with `\G` rather than with `;` or `\g`.

+   - `--wait`, `-W`
+   Waits and retries if a connection to the server cannot be established.

+   - `--xml`, `-X` *(boolean)*
+   Produces XML output.

# F.5.3 Variables for mysql

The following `mysql` variables can be set using the instructions given in Section E.2.1.2, “Setting Program Variables.”

+   - `connect_timeout`
+   The number of seconds to wait before timing out when attempting to connect to the server. The default value is 0.

+   - `max_allowed_packet`
+   The maximum size of the buffer used for communication between the server and the client. The default value is 16MB and the maximum is 1GB.