```
basedir=/var/lib

[mysql_safe]
err-log=/var/log/mysql.log
pid-file=/var/run/mysql/mysqld.pid
```

Most of the settings in the default my.cnf file define the locations of files and directories needed by the mysqld server. Each option is associated with a particular group, with each group identified by a name in square brackets. The previous options are associated with the mysqld daemon (`[mysqld]`), the MySQL server (`[mysql_server]`), and the *safe_mysqld* script that starts the *mysqld* daemon (`[mysql_safe]`). (Refer to Table 24-1 for a list of these groups.)

The default *datadir* value indicates that `/var/lib/mysql` is the directory that stores the MySQL databases you create. The *socket* option identifies `/var/lib/mysql/mysql.sock` as the socket that is used to create the MySQL communications end-point associated with the *mysqld* server. The *basedir* option identifies `/var/lib` as the base directory in which the *mysql* software is installed. The *user* option identifies *mysql* as the user account that has permission to do administration of the MySQL service. Based on the *old_passwords*=1 value, your MySQL database will use the password format used in previous MySQL 3.x databases.

The *err-log* and *pid-file* options tell the *safe_mysqld* script the locations of the error log (`/var/log/mysql.log`) and the file that stores the process ID of the *mysqld* daemon when it is running (`/var/run/mysql/mysqld.pid`). The *safe_mysqld* script actually starts the *mysqld* daemon from the *mysqld* startup script.

> **NOTE:** Each option that follows a group name is assigned to that group. Group assignments end when a new group begins or when the end of a file is reached.

# Choosing options

Many values are used by the MySQL server that are not explicitly defined in the *my.cnf* file. The easiest way to see which options are available for MySQL server and clients is to run each command with the `--help` option. For example, to view the available *mysqld* options (as well as other information) type the following from a Terminal window:

```
# /usr/libexec/mysqld --verbose --help | less
```

Then press the Spacebar to step through the information one screen at a time. (An example of this output is shown in the next section.)

You can also use the *man* command to find which options are available. For example, to see which options are available to set for the *mysqld* daemon, type the following:

```
man mysqld
```