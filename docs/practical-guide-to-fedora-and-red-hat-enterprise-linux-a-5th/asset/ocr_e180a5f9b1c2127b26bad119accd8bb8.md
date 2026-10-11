ps -ef command to determine whether a user has created a runaway process that is creating a huge file. When evaluating the output of ps, look for a process that has consumed a large amount of CPU time. If such a process is running and creating a large file, the file will continue to grow as you free up space. If you remove the huge file, the space it occupied will not be freed until the process terminates, so you need to kill the process. Try to contact the user running the process, and ask the user to kill it. If you cannot contact the user, log in as root and kill the process yourself. Refer to kill on page 409 for more information.

You can also truncate a large log file rather than removing it, although you can better deal with this recurring situation with logrotate (discussed in the next section). For example, if the /var/log/messages file has become very large because a system daemon is misconfigured, you can use /dev/null to truncate it:

```
# cp /dev/null > /var/log/messages
```

or

```
# cat /dev/null > /var/log/messages
```

or, without spawning a new process,

```
# : > /var/log/messages
```

If you remove /var/log/messages, you have to restart the rsyslogd (FEDORA) or syslogd (RHEL) daemon. If you do not restart rsyslogd, the space on the filesystem is not released.

When no single process is consuming the disk space but capacity has instead been used up gradually, locate unneeded files and delete them. You can archive these files by using cpio, dump, or tar before you delete them. You can safely remove most files named core that have not been accessed for several days. The following command line performs this function without removing necessary files named core (such as /dev/core):

```
# find / -type f -name core \| xargs file \| grep 'B core file' \| sed 's/:ELF.*/g/\' \| xargs rm -f
```

The find command lists all ordinary files named core and sends its output to xargs, which runs file on each of the files in the list. The file utility displays a string that includes B core file for files created as the result of a core dump. These files need to be removed. The grep command filters out from file lines that do not contain this string. Finally sed removes everything following the colon so that all that is left on the line is the pathname of the core file; xargs removes the file.

To free up more disk space, look through the /tmp and /var/tmp directories for old temporary files and remove them. Keep track of disk usage in /var/mail, /var/spool, and /var/log.

# logrotate: Manages Log Files

Rather than deleting or truncating log files, you may want to keep these files for a while in case you need to refer to them. The logrotate utility helps you manage system log (and