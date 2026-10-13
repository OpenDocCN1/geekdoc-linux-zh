two options for rotating your logs: use a utility that comes with Apache called rotatelog, or use logrotate.

# Using rotatelog

Apache comes with a support tool called rotatelog. You can use this program as follows:

```
TransferLog "| /path/to/rotatelogs logfile rotation time in seconds"
```

For example, if you want to rotate the access log every 86,400 seconds (24 hours), use the following line:

```
TransferLog "| /path/to/rotatelogs /var/logs/httpd 86400"
```

You will have each day's access log information stored in a file called /var/logs/httpd.nnnn, where nnnn represents a long number.

# Using logrotate

The logrotate utility rotates, compresses, and mails log files. It is designed to ease the system administration of log files. It enables the automatic rotation, compression, removal, and mailing of log files on a daily, weekly, or monthly basis, or on a size basis. Normally, logrotate is run as a daily cron job. You can create a file called /etc/logrotate.d/apache as follows:

```
/path/to/apache/access_log {
compress
rotate 5
main webmaster@yourdomain.com
errors root@yourdomain.com
size=1024K
postrotate
kill -HUP `cat /path/to/httpd.pid`
endscript
}
```

This configuration specifies that the /path/to/apache/access_log file be rotated whenever it grows over 1MB (1,024K) in size, and that the old log files be compressed and mailed to webmaster@yourdomain.com after going through five rotations, rather than being removed. Any errors that occur during processing of the log file are mailed to root@yourdomain.com.