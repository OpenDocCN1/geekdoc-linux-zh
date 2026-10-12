```
```
# run-parts
01 * * * * root run-parts /etc/cron.hourly
02 4 * * * root run-parts /etc/cron.daily
22 4 * * 0 root run-parts /etc/cron.weekly
42 4 1 * * root run-parts /etc/cron.monthly
```
```

If you take a look under the `/etc/cron.daily` directory, you'll see

```
@anacron logrotate makewhatis.cron slocate.cron tmpwatch
```

These files are executable shell scripts that are run (according to the `/etc/crontab.daily` entry) each day at 4:02 a.m. If your backup operations take too long and can possibly run into the morning work hours, you should adjust this setting, or create your own `/etc/crontab` entry, such as:

```
30 2 * * * /bin/tar cvzf /backup/daily.tgz /home
```

This example will back up the `/home` directory to the file named `daily.tgz` under the `/backup` directory each morning at 2:30 a.m.

# # Performing Backups with the taper Script

The taper script (`/usr/sbin/taper`), included with Red Hat Linux, is a backup and restore program with a graphical interface you can use to maintain compressed or uncompressed archives on tapes or removable media (even over a network!). Using taper is easy; the format of a taper command line looks like this:

```
# taper -<T tape-type> <option> <device>
```

You first need to decide what type of device (or media) you'd like to use with `taper`. This program supports a number of devices, which are listed in Table 22.2 along with the command lines to use.

**TABLE 22.2 Device Support by taper**

| Device | Type | Command Line |
| :--- | :--- | :--- |
| /dev/zftape | Floppy tape driver | # taper -T z |
| /dev/ht0 | IDE tape driver | # taper -T i |
| file | File on hard disk | # taper -T l |
| /dev/ftape | Floppy tape driver | # taper -T f |
| /dev/fd0 | Removable floppy drive | # taper -T r |
| /dev/sda4 | Removable Zip drive | # taper -T r -b /dev/sda4 (-b denotes the device and archive file) |
| /dev/sda | SCSI tape drive | # taper -T s |