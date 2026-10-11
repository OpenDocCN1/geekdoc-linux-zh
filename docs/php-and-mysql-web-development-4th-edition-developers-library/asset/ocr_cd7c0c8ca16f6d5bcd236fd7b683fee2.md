should apply to all servers. These need not be replicated in individual per-server option files.

Be sure that any options placed into a common option group are understood by all servers that you run. For example, you can’t use event_manager=1 to enable the event scheduler if any of your servers are older than version 5.1.6, because that is when events were introduced. Its presence in a common option group will cause startup failure for older servers.

If all of your servers are from MySQL 4.0.2 or newer, you can use the loose-opt_name syntax to specify options that are not understood by all servers. Servers that do not understand an option given this way will ignore the option and continue to execute after logging a warning. For more information about “loose” options, see Section F.1, “Specifying Program Options.”

+   - Use the mysqld_multi script to manage startup for multiple servers. This script enables you to list the options for all servers in a single file but associate each server with its own particular option group in the file.
+   - Under Windows, you can run multiple services, using the special option file group naming conventions specific to this style of server setup. See Section 12.2.2.2, “Running the Server as a Windows Service.”

The following sections show some ways to apply these strategies by demonstrating how to use mysqld_multi and how to run multiple servers under Windows.

# 12.10.4 Using mysqld_multi for Server Management

On Unix, the mysqld_safe and mysqld.server scripts that are commonly used to start the server both work best in a single-server setting. To make it easier to handle several servers, the mysqld_multi script can be used instead.

mysqld_multi works on the basis that you assign a specific number to each server setup you want to create, and then list that server’s options in an option file ([mysqldn] group, where n is the number.The option file can also contain a [mysqld_multi] group that lists options specifically for mysqld_multi itself. For example, if I have servers installed for MySQL 5.0.56, 5.1.24, and 6.0.5, I might designate their option groups as [mysqld50056], [mysqld50124], and [mysqld60005] and set up the options in the /etc/my.cnf file like this:

```
```ini
[mysqld50056]
basedir=/var/mysql/50056
datadir=/var/mysql/50056/data
mysqld=/var/mysql/50056/bin/safe_mysqld
socket=/var/mysql/50056/mysql.sock
port=50056
user=mysql
log=1og
log-bin=binlog
innodb_data_file_path = ibdata1:100M
```
```