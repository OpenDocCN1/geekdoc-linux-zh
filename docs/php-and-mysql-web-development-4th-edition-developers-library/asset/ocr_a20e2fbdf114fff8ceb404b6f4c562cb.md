# F.13 mysqld_multi

The `mysqld_multi` script makes it easier to run several `mysqld` servers on a single host. It enables you to start or stop servers, or determine whether they are running:

```
mysqld_multi [options] command server_list
```

command is one of start, stop, or report. The server_list argument indicates which servers you want to manipulate. For further instructions on using `mysqld_multi`, see Section 12.11.4, “Using mysqld_multi for Server Management.”

# F.13.1 Standard Options Supported by mysqld_multi

```
--help --silent --verbose
--password --user --version
```

--silent and --verbose are available as of MySQL 5.0.2.

mysqld_multi passes the --user and --password option values to `mysqladmin` when it needs to stop servers or determine whether they are running.

# F.13.2 Options Specific to mysqld_multi

+   - -config-file=file_name
+   
+   As of MySQL 5.0.42/5.1.18, this option is deprecated; use the standard -defaults-extra-file option instead. For earlier versions, this option names the option file from which to read to obtain options for the servers that `mysqld_multi` manipulates; without -config-file, `mysqld_multi` reads /etc/my.cnf and the .my.cnf file in your home directory to obtain server options. (mysqld_multi reads the standard option files for its own options. This option does not change that behavior.)

+   - -example
+   
+   Displays a sample option file that demonstrates option file groups suitable for use with `mysqld_multi`.

+   - -log-file=file_name
+   
+   The name of the log file where `mysqld_multi` should log its actions. Output is appended to the log if it already exists. The default log file is named `mysqld_multi.log` in the data directory. To disable logging, use --no-log.

+   - -mysqladmin=file_name
+   
+   The pathname to the `mysqladmin` binary you want to use. This can be useful if `mysqld_multi` cannot find `mysqladmin` by itself, or if you want to use a particular version.

+   - -mysql=file_name
+   
+   The pathname to the `mysqld` binary you want to use. This can be useful if `mysqld_multi` cannot find `mysqld` by itself, or if you want to use a particular