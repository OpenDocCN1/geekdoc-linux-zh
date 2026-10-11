forth. This is the information that you can specify using table_option values in the CREATE TABLE syntax. (See Appendix E.)
This option is enabled by default; use --skip-create-options to disable it.

+   - --databases, -B (boolean)
+   Interprets all arguments as database names and dumps all tables in each database.
+   This option also causes the dump output to include CREATE DATABASE IF NOT EXISTS and USE statements for each database.

+   - --delayed-insert (boolean)
+   Writes INSERT DELAYED statements rather than INSERT statements. If you are loading a dump file for MyISAM tables into another database and you want to minimize the impact of the operation on other statements that may be taking place in that database, --delayed-insert is helpful for achieving that end.

+   - --delete-master-logs
+   Deletes the binary log files on the server and begins a new one by issuing a FLUSH MASTER statement after generating the dump output. Don’t use this option unless you’re sure you want the existing binary logs to be wiped out. This option enables --master-data.

+   - --disable-keys, -K (boolean)
+   Adds ALTER TABLE ... DISABLE KEYS and ALTER TABLE ... ENABLE KEYS statements to the output, to disable updates to non-unique indexes while INSERT statements are being processed. This speeds up index creation for each MyISAM table by causing it to happen all at once after the table is loaded.

+   - --dump-date (boolean)
+   Adds a comment indicating the dump date to the end of the output. This option was introduced in MySQL 5.0.52/5.1.23.

+   - --dump-slave[=n]
+   This option is like --master-data, but is used for dumping a replication slave server and produces a CHANGE MASTER statement in the output that indicates the binary log coordinates of the slave’s master, not those of the slave itself. See the description of --master-data for a description of how the option argument is used. The --dump-slave option was introduced in MySQL 6.0.4.

+   - --events, -E (boolean)
+   Includes events in the dump output. This option was introduced in MySQL 5.1.18.

+   - --extended-insert, -e (boolean)
+   Writes multiple-row INSERT statements. These can be loaded more efficiently than single-row statements.