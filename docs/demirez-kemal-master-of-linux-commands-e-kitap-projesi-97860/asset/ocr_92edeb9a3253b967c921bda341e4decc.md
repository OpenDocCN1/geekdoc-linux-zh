# Cpio

A simple way to backup and to restore a directory, you can use cpio command. Simple use of the command is as follows:

+   - ls | cpio -ov > backup.cpio : cpio extension of the backup file is created

+   - cpio -idv < backup.cpio : restore the backup created with cpio

+   - cpio --list < backup.cpio : lists the contents of the backup file

For example, if you want to backup /etc directory, in /etc directory when you first use ls | cpio -ov > /tmp/backup.cpio command, etc directory backed under /tmp with backup.cpio name.

```
root@kemal:/etc# ls | cpio -ov > /tmp/backup.cpio
adduser.conf
adjtime
aliases
alternatives
amap
anacrontab
apache2
apg.conf
apm
apparmor.d
apt
arpwatch.conf
at.deny
at-spi2
navahi
avavrdude.conf
```