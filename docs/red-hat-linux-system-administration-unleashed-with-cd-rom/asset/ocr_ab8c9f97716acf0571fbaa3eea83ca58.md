support for “dump-levels.” This “dump-level” is the same as that used by the tar program: Any dump-level backs up files that have been changed or added since the same or higher-numbered level was done. Level-0 is highest, level-9 lowest, so a level-1 includes levels 1 through 9, but not level-0.

This command creates a level-0 backup of one subdirectory:

```
/sbin/dump -0u -f /dev/nst0 /usr/src
```

All files are backed up, in this case to the tape unit attached to the floppy drive controller. An incremental may be given a dump-level arbitrarily from 1 to 9; if you always use the same value, you will get files modified since the last incremental at the same level or a higher numbered one.

The command

```
/sbin/dump -3u -f /dev/nst0 /usr/src
```

would only back up changed files from the /usr/src tree if they have been modified since the last level-3 or higher numbered backup was run.

To recover files, directories, or filesystems backed up with the dump command, the restore command is used. When used with the -i option (as in restore -if /dev/nst0), specific files or subdirectories may be recovered. For example, restoring the file /etc/cron.daily/logrotate, which I have modified, generates this for output:

```
[root@clarence /root]# /sbin/restore -if /dev/nst0
restore > ls
.:
dev/ etc/ root/ tmp/ usr/ var/

restore > cd etc
restore > ls
./etc:
cron.daily/ dumpdates

restore > add cron.daily
restore > ls cron.daily
./etc/cron.daily:
*logrotate

restore > extract
You have not read any tapes yet.
Unless you know which volume your file(s) are on you should start
with the last volume and work towards the first.
Specify next volume #: 1
```