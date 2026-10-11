```
[mysqld50124]
  basedir=/var/mysql/50124
  datadir=/var/mysql/50124/data
  mysqld=/var/mysql/50124/bin/mysqld_safe
  socket=/var/mysql/50124/mysql.sock
  port=50124
  user=mysql
  log=qlog
  log-bin=binlog
  innodb_data_file_path = ibdata1:50M:autoextend
  event_scheduler=ON
```

```
[mysqld60005]
  basedir=/var/mysql/60005
  datadir=/var/mysql/60005/data
  mysqld=/var/mysql/60005/bin/mysqld_safe
  socket=/var/mysql/60005/mysql.sock
  port=60005
  user=mysql
  log=qlog
  log-bin=binlog
  skip-innodb
  language=french
  character-set-server=utf8
```

The layout parameters that I've set up here for each server correspond to the directory configuration described in Section 12.10.2, "Configuring and Compiling Different Servers." I've also specified additional server-specific parameters that correspond to variations in types of logs, storage engines, and so forth.

To start a given server, invoke `mysqld_multi` with a command word of *start* and the server's option group number on the command line:

```
% mysqld_multi --no-log start 50124
```

The `--no-log` option causes status messages to be sent to the terminal rather than to a log file. This enables you to see what's going on more easily. You can specify more than one server by giving the group numbers as a comma-separated list. A range of server numbers can be specified by separating the numbers with a dash. However, there must be no whitespace in the server list. For example:

```
% mysqld_multi --no-log start 50056,50124-60005
```

To stop servers or obtain a status report indicating whether they are running, use a command word of *stop* or *report* followed by the server list. For these commands, `mysqld_multi` invokes `mysqladmin` to communicate with the servers, so you'll also need to specify a username and password for an administrative account:

```
% mysqld_multi --nolog --user=root --password=rootpass stop 50056
% mysqld_multi --nolog --user=root --password=rootpass report 50056,60005
```