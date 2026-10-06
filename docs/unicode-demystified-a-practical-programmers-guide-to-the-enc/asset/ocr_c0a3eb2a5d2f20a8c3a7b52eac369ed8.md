# Chapter 17 Red Hat Linux System Administration

or

```
# /dev/null > /var/log/messages
or, without spawning a new process,
# : /var/log/messages
```

If you remove /var/log/messages, you have to restart the syslogd daemon. With-out restarting syslogd, the space on the filesystem is not released.

When no single process is consuming the disk space but it has instead used up gradually, locate unused files and delete them. You can archive them by using cpio, dump, or tar before you delete them. You can safely remove most files that have not been accessed for several days. The following command line performs this without removing necessary files core (such as /dev/core, which is a symbolic link to /proc/kcore):

```
# find -type f -name core | grep '8 core file' | sed 's/.*//$' | xargs rm -f
```

The find command lists all ordinary files named core and sends its output to xargs, which runs file on each of the files in the list. The file utility displays a string that includes 8 core file for files created as the result of a core dump. These files need to be removed. The grep command filters out from file lines that do not contain this string. Finally, sed removes everything following the colon so that all is left on the line is the pathname of the core file; xargs removes the file.

Look through the /tmp and /var/tmp directories for temporary files and remove them. Keep track of disk usage in /var/mail, /var/spool, and /var/log.

# logrotate: Manages Log Files

Rather than deleting or truncating log files, you may want to keep the contents around for a while in case you need to refer to them. The logrotate utility helps you manage system log (and other) files automatically by rotating (page 1490), pressing, mailing, and removing each as you specify. The logrotate utility is controlled by the /etc/logrotate.conf file, which sets default values and can optionally specify files to be rotated. logrotate.conf has an include statement that points to unit-specific specification files in /etc/logrotate.d. Following is the default logrotate.conf:

```
# cat /etc/logrotate.conf
# see "logrotate" for details
# rotate log files weekly
```

```
# keep 4 weeks worth of backlogs
rotate 4
```

```
# create (empty) log files after rotating old ones
create
```

```
# uncomment this if you want your log files compressed
compress
```