
[root@server1 ~]# `ls -l /var/log/boot.log`

`-rw---- 1 root root 21705 Aug 27 10:52 /var/log/boot.log`

[root@server1 ~]# `lp -d printer1 /var/log/boot.log`

[root@server1 ~]# `ls -1 /var/log/boot.log`

`-rw---- 1 root root 0 Aug 27 10:52 /var/log/boot.log`

Alternatively, you can schedule the `logrotate` command to back up and clear log files entries stored in the `/etc/logrotate.conf` file and files stored in `/etc/logrotate.d` directory. The `logrotate` command typically renames (or rotates) log files on a cyclic basis; the log file will be renamed to contain a numeric or date extension, and a new log file will be created to accept system information. You can specify the type of extension as well as the number of log files that are kept. If configured to keep only two copies of old log files, then after two rotations, the oldest log file will be automatically removed.

### Example of `/etc/logrotate.conf`

```
[root@server1 ~]# cat /etc/logrotate.conf
# see "man logrotate" for details

# rotate log files weekly
weekly

# keep 4 weeks worth of backlogs
rotate 4

# create new (empty) log files after rotating old ones
create

# use date as a suffix of the rotated file
dateext

# uncomment this if you want your log files
#compress

# RPM packages drop log rotation information into this directory
include /etc/logrotate.d
```

```
# no packages own wtmp and btmp -- we'll rotate them here
/var/log/wtmp {
  monthly
  create 0664 root utmp
  minsize 1M
  rotate 1
}

/var/log/btmp {
  missingok
  monthly
  create 0600 root utmp
  rotate 1
}
```

In the preceding output, any `#` characters indicate a comment and are ignored. The other lines indicate log files contained in this file and all other files in the `/etc/logrotate.d` directory (`include /etc/logrotate.d`) are rotated on a weekly basis unless specified (`weekly`) using a date extension (`dateext`), and up to 4 weeks of log files will be kept (`rotate 4`).

The bottom of the `/logrotate.conf` file has two entries that override these values. For the file `/var/log/wtmp`, this rotation occurs monthly instead of weekly, only if the size of the log file is greater than 1MB. Only one old log file is kept, and the new log file has the permissions `0664(rw-rw-)`, the owner `root`, and the group `utmp`. For the file `/var/log/btmp`, rotation occurs monthly instead of weekly, and no errors are reported if the log file is missing. Only one old log file is kept, and the new log file has the permissions `0600 (rw-------)`, the owner `root`, and the group `utmp`.

Most rotation within `/etc/logrotate.conf` is overridden from files stored in the `/etc/logrotate.d` directory. Take the file `/etc/psacct` as an example:

```
[root@server1 ~]# cat /etc/logrotate.d/psacct
# Logrotate file for psacct
/var/log/psacct {
  compress
  daily
  rotate 7
  create 0600 root root
  postrotate
    /usr/sbin/killall -HUP psacct
  endscript
}
```
