Now lets use --list < backup.cpio command to list of the backup file content.

```
root@kemal:/tmp# -l backup.cpio
-rw-r--r-- 1 root root 956416 Kas 25 01:23 backup.cpio
root@kemal:/tmp# file backup.cpio
backup.cpio: cpio archive
root@kemal:/tmp# cpio --list < backup.cpio
adduser.conf
adjtime
aliases
alternatives
amap
anacrontab
apache2
apg.conf
apm
```

We must use cpio -idv < /tmp/backup.cpio to restore backup file.

```
root@kemal:/etc# cpio -idv < /tmp/backup.cpio
cpio: adduser.conf oluşturulmadi: daha yeni ya da
adduser.conf
```