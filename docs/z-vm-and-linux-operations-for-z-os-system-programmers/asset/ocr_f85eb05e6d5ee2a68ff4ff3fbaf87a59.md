```
May 29 13:54:49 1ngxgill sshd[1256]: Accepted keyboard-interactive/pam\nfor root from 9.57.138.243 port 2063 ssh2\nMay 29 14:02:55 1ngxgill sshd[1332]: Accepted keyboard-interactive/pam\nfor root from 9.57.138.243 port 2102 ssh2
```

The **head** command does the same thing, but displays only the first lines of a log file. The **dmesg** command displays the messages logged by the kernel logger daemon.

# Log files archiving

To avoid storing large amounts of data, the log files are rotated on a regular basis. The rotation process is managed by the **logrotate** command, which is controlled by a **cronjob** launched daily. For more information about cronjob, refer to section 5.4.1, “Job scheduling” on page 275.

Depending on the configuration options of **logrotate**, log files are kept several days or weeks, compressed or not, until they reach a certain age or size.

As shown in Example 8-16, the older messages log file has been rotated four times, compressed, and kept on disk. These were the defaults for SUSE Linux 9.

*Example 8-16   Content of /var/log/ directory*

```text
mastervm12:/var/log # ls -al
total 3424
drwxr-xr-x   5 root root  4096 May 16 04:15 .
drwxr-xr-x  13 root root  4096 Jan 16  2007 ..
drwxr-xr-x   2 root root  4096 Feb 12 15:10 YaST2
drwxr-x---   2 root root  4096 Feb 12 10:11 apache2
-rw-r-----   1 root root  4096 Jan 16  2007 boot.log
-rw-r--r--   1 root root 13651 Apr 19 23:13 boot.msg
-rw-r--r--   1 root root 15623 Apr 19 23:12 boot.omsg
-rw-r--r--   1 root root  586 Jan 16  2007 convert_for_getconfig.log
-rw-r--r--   1 root root 32096 Apr 10 00:15 faillog
-rw-r--r--   1 root tty  29688 May 27 21:27 lastlog
-rw-r--r--   1 root root   474 Dec  6 15:37 localmessages
-rw-r-----   1 root root  5334 Apr 30 17:20 mail
-rw-r-----   1 root root  1796 Apr 30 17:20 mail.err
-rw-r-----   1 root root  5334 Apr 30 17:20 mail.info
-rw-r-----   1 root root  3974 Apr 30 17:20 mail.warn
-rw-r-----   1 root root 214109 May 27 21:27 messages
-rw-r-----   1 root root 333920 Dec 11 04:15 messages-20071211.gz
-rw-r-----   1 root root 340177 Feb  2 04:15 messages-20080202.gz
-rw-r-----   1 root root 337732 Feb 21 04:15 messages-20080221.gz
-rw-r-----   1 root root 329943 May 16 04:15 messages-20080516.gz
[...]
```