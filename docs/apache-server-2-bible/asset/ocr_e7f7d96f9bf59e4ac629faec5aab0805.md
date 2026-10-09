Creating logs in Apache is easy and useful. Creating logs enables you to learn more about what's going on with your Apache server. Logs can help you detect and identify your site's problems, find out about your site's best features, and much more. Can something so beneficial come without a catch? If you said no, you guessed right. Log files take up a lot of valuable disk space, so they must be maintained regularly.

# # Log Maintenance

By enabling logging, you may be able to save a lot of work, but the logs themselves do add some extra work for you: they need to be maintained. On Apache sites with high hit rates or many virtual domains, the log files can become huge in a very short time, which could easily cause a disk crisis. When log files become very large, you should rotate them.

You have two options for rotating your logs: you can use a utility that comes with Apache called *rotatelog*, or you can use *logrotate*, a facility that is available on most Linux systems.

# ## Using rotatelog

Apache comes with a support utility called *rotatelog*. You can use this program as follows:

```
TransferLog "| /path/to/rotatlogs logfile rotation_time_in_seconds"
```

For example, if you want to rotate the access log every 86,400 seconds (that is, 24 hours), use the following line:

```
TransferLog "| /path/to/rotatlogs /var/logs/httpd 86400"
```

Each day's access log information will be stored in a file called /var/logs/httpd.nnnn, where *nnnn* represents a long number.

# ## Using logrotate

The *logrotate* utility rotates, compresses, and mails log files. It is designed to ease the system administration of log files. It enables the automatic rotation, compression, removal, and mailing of log files on a daily, weekly, or monthly, or size basis. Normally, *logrotate* is run as a daily *cron* job. Read the *man* pages for *logrotate* to learn more about it.

If your system supports the *logrotate* facility, you should create a script called /etc/logrotate.d/apache as shown in Listing 8-2.