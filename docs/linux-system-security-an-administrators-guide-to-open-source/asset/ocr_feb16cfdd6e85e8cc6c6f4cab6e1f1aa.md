valuable in isolating user activity or command execution at certain times. But in order for it to be available, you must turn it on! (See *Process Accounting* on page 153.)

# ACCOUNTING FILES

Essentially, the files `/var/run/wtmp`, `/var/log/wtmp`, and `/var/log/pacct` are dynamic database files. Of them, `/var/log/pacct` and `/var/log/wtmp` grow by having entries appended and modified. The problem is that since these files grow dynamically, at some point they become large. The general issue of managing log files is discussed in detail in Chapter 17. However, we provide the following to get you started and to address the immediate problem of managing your growing `/var/log/pacct` and `/var/log/wtmp` files.

There is a really cool program available in the Red Hat 5.2/6.0 Linux distribution called logrotate. It reads a configuration file called `/etc/logrotate.conf`, which among other things tells it to read all of the files in the `/etc/logrotate.d` directory. Consequently, whenever you need to manage a file that grows dynamically, all you have to do is put a logrotate conforming script in `/etc/logrotate.d`. The script in Example 7-8 is one way to manage the `/var/log/wtmp` accounting files.

# Example 7-8  Log Rotation Script for Accounting Files

```
/var/log/wtmp {
    rotate 5
    weekly
    errors root@topcat
    mail root@topcat
    copytruncate
    compress
    size 100k
}
```

Put this script into a file—call it accounting, for example—in the `/etc/logrotate.d` directory and your accounting files will be rotated every week. For complete details on how this works see Chapter 17.

While you may be tempted to do something similar with `/var/log/pacct`, don't! Remember that it accumulates data about process activity and, as long as the system is up and running, it will be maintaining that information dynamically. If this file gets too large, archive it while in single-user mode. If the system cannot be brought down on a regular basis, you can turn off process accounting by executing `accton` as root, then archive the file. This latter approach will cause some data loss, so the best solution is to turn off process accounting when the system is most quiescent. You can automate this process with `logrotate` as described in `logrotate` on page 492 in Chapter 17.