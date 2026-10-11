When the script executes, it will read the named file for connection parameters. Suppose that /home/paul/.my.cnf has the following contents:

```
[client]
host=localhost
user=sampadm
password=secret
```

In this case, the connect() call will attempt to connect to the MySQL server on localhost and will connect as user sampadm with password secret. Under Unix, you can tell your script to use the option file that belongs to the person who happens to be running it by parameterizing the filename like this:

```
my $dsn = "DBI:mysql:sampdb;mysql_read_default_file=$ENV{HOME}/.my.cnf";
```

$ENV{HOME} contains the pathname to the home directory of the user running the script, so the connection parameters that it uses will be pulled from that user's own option file. By writing a script in this way, you don't have to embed connection parameters literally in the script.

Using mysql_read_default_file causes the script to read only the named option file, which may be undesirable if you want it to look for parameters in system-wide option files as well (such as /etc/my.cnf under Unix or C:\my.ini under Windows). To have the script read all the standard option files for connection parameters, use mysql_read_default_group instead. This option causes parameters in the [client] group to be used, as well as in the group that you specify in the option's value. For example, if you have options that are specific to your sampdb-related scripts, you can list them in a [sampdb] group and then use a data source value like this:

```
my $dsn = "DBI:mysql:sampdb;mysql_read_default_group=sampdb";
```

If you want to read just the [client] group from the standard option files, specify the option like this:

```
my $dsn = "DBI:mysql:sampdb;mysql_read_default_group=client";
```

For more details on options for specifying the data source string, see Appendix H (online). For more information on the format of MySQL option files, see Appendix F “MySQL Program Reference.”

One difficulty with using mysql_read_default_file on Windows is that file pathnames typically begin with a drive letter and a colon. That's a problem, because DBI interprets colon as the character that separates parts of the DSN string. It's possible to work around this, although the method is ugly:

+   1. Use chdir() to change location to the root directory of the drive where the option file is located, so that pathnames specified without a drive letter will be interpreted relative to that drive.
+   2. Specify the filename as the value of the mysql_read_default_file option in the DSN, but without the leading drive letter or colon.