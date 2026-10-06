# Chapter 23 ✦ Running FTP Server on SUSE 607

Each download is also logged.
Note you can force vsftpd to write its logs to its own log file by making a small change to /etc/vsftpd.conf. Simply make sure that the following lines are present:

```
log_ftp_protocol=YES
xfer_enable=YES
vsftpd_log_file=/var/log/vsftpd.log
```

Then comment out or remove the line:
syslog_enable=YES

You can create a customized FTP banner by including a line like this in the configuration-file:

```
ftpd_banner="Welcome to our very fine FTP service."
```

When users log in using text mode FTP or a dedicated FTP client, they will see the following message before the login prompt:

```
220 "Welcome to our very fine FTP service."
Name (localhost:user):
```

This can be used to offer service messages, but is not useful for users connecting with a browser. It may be useful to include the files README and README.html, which these users can click.

You can also place a file named .message in /srv/ftp/ or any of its subdirectories. When the user changes to a directory with a file in it, the file's contents will be displayed.

```
ftp> cd pub
250-This directory contains useful files
250 Directory successfully changed.
ftp->
```

The file /srv/ftp/pub/.message contained just the line:

```
This directory contains useful files
```

vsftpd allows passive FTP connections unless you set
pasv_enable=NO

In the configuration file. You almost certainly want to allow passive connections, as otherwise many clients connecting from behind a firewall will be unable to connect.