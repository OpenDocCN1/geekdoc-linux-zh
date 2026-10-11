# **Table 11-5  
logrotate Commands**

| Command | Use |
| --- | --- |
| compress | Compresses old logs using gzip. |
| copytruncate | Copies old logs and then truncates them. |
| create | Creates permissions for files. If none are specified, the permissions of the old files are used. |
| daily | Rotates log files daily. |
| delaycompress | Compresses log files during the next rotation. |
| errors mailto | Mails error messages to the specified address. |
| ifempty | Rotates empty log files. |
| include filename | Used to read the filename into the config file. |
| mail mailto | Specifies address to mail log files to when they are deleted. |
| monthly | Rotates log files monthly. |
| nocompress | Does not compress log files. |
| nocopytruncate | Does not copy and truncate. |
| nocreate | Specifies not to create a new log file. |
| nodelaycompress | Compresses log files immediately. |
| noolddir | Log files are not moved to another directory. |
| noifempty | Empty log files are not rotated. |
| olddir directory | Old log files are moved to a specified directory. |
| postrotate | Script is run after log is rotated. |
| prerotate | Script is run before log is rotated. |
| rotate n | Specifies the number of old log files to keep. |
| size n | Rotates when log files reach the size specified. Can be used with n for bytes, k for kilobytes, and M for megabytes. |

# ## Identifying problems using log files

Simply keeping log files won’t solve or prevent problems on your systems. For log files to be useful you must regularly examine the data that is logged. The `dmesg` command can be used to display system messages. The command is used with the following syntax:

```
`dmesg [options]`
```