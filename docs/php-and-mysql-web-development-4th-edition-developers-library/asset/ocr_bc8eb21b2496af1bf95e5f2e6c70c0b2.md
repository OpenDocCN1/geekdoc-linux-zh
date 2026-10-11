```
# Argument 1: log filename

if [ $# -ne 1 ]; then
   echo "Usage: $0 logname" 1>&2
   exit 1
fi

logfile=$1

mv $logfile.6 $logfile.7
mv $logfile.5 $logfile.6
mv $logfile.4 $logfile.5
mv $logfile.3 $logfile.4
mv $logfile.2 $logfile.3
mv $logfile.1 $logfile.2
mv $logfile $logfile.1
mysqladmin flush-logs
```

The script takes the log filename as its argument. You can either specify the full path- name of the file or change directory into the log directory and specify the file's name in that directory. For example, to rotate a log file named qlog in /usr/mysql/data, execute the script like this:

```
% rotate_fixed_logs.sh /usr/mysql/data/qlog
```

Or like this:

```
% cd /usr/mysql/data
% rotate_fixed_logs.sh qlog
```

# Note

The first few times the log rotation script executes, you won't have a full set of log files in the rotation, so the script complains that it can't find all the files to be rotated. That's normal.

To make sure that you have permission to rename the log files, run the script while logged in under the same account that you use for running the server (that's the mysql account in this book). Note that the mysqladmin command in the script includes no connection parameter arguments such as -u or -p. If the relevant parameters for invoking mysqladmin are stored in the .my.cnf option file in the mysql account home directory, you don't need to specify them on the mysqladmin command in the script. If you don't use an option file, the mysqladmin command needs to know how to connect to the server using a MySQL account that has sufficient privileges to flush the logs. To handle this, you might want to set up a limited-privilege account that can't do anything but issue flush commands. Then you can put that account's password in the script with minimal risk if you make the script accessible only to mysql. If you want to do this, the MySQL account