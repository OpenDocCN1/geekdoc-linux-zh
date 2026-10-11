--character-sets-dir is available as of MySQL 5.0.3. --debug-check and --debug-info are available as of MySQL 5.1.21.

# F.10.2 Options Specific to mysqlbinlog

+   • -base64-output[=value]
+       Indicates when output should consist of BINLOG statements in base-64-encoded form. This option was introduced in MySQL 5.1.5 as a boolean option. As of 5.1.24, it takes argument values of auto (use base-64 only when necessary), always, or never. The default is auto if the option is not given; if given with no argument, the default is always.

+   • -database=db_name,-d db_name
+       Extracts statements from the log file only for the named database. This option works only when reading local logs.

+   • -disable-log-bin,-D (boolean)
+       Includes statements in the output that disable binary logging of the update statements in the log. This prevents the statements from being logged again when they are re-executed.

+   • -force-if-open,-F (boolean)
+       Reads binary log files even if they were not closed properly (or are currently in use). This option was introduced in MySQL 5.1.15.

+   • -force-read,-f (boolean)
+       This option controls what mysqlbinlog does when it reads an event from the binary log that it is unable to recognize. By default, it stops. If this option is enabled, mysqlbinlog continues after logging a warning and discarding the event.

+   • -hexdump,-H (boolean)
+       Includes a hexadecimal/ASCII event dump in the output. This option was introduced in MySQL 5.0.16.

+   • -local-load=dir_name,-l dir_name
+       The directory in which to create to create temporary data files for processing LOAD DATA LOCAL statements.

+   • -offset=n,-o n
+       Skips the first n events in the log file.

+   • -position=n,-j n
+       This option is deprecated in favor of -start-position.