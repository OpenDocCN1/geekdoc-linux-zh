# TABLE 10.2 Helpful mount Flags

| Flag | Meaning |
|------|---------|
| -a | Ensure that all devices listed in /etc/fstab are mounted, and mount them if they are detached. This can be combined with -t to allow mount -a -t ufs, for example, which will force all UFS filesystems listed in the /etc/fstab file to be mounted if possible. |
| -o opts | Specify opts options to mounting. Common values are ro (read-only), rw (read/write), noatime (disable updating access times on files, speeding up disk interaction), noauto (disk can only be mounted explicitly, rather than with a mount -a), and noexec (disable execution of binaries on the disk). |
| -r | Mount read-only (analogous to -o ro). |
| -t type | Mount the disk as type type. Common values are ext2, ext3, hfs, hfs+, nfs, ufs, iso9660, and xfs, depending on which platform you're on. |
| -v | Verbose output. Shows more of what's happening. |
| -w | Mount read/write (analogous to -o rw). |

As a further experiment, let's copy an executable binary onto the disk, then mount the disk read-only to demonstrate some interesting behaviors:

```
# mkdir /disk2
# cp /bin/ls /home/taylor
# umount /dev/hdb

# mount -o ro,noexec -v -t ext2 /dev/hdb /disk2
/dev/hdb on /disk2 type ext2 (ro,noexec)
# ls -alf /disk2
# ls -al /disk2
total 63
drwxr-xr-x 3 root root 1024 Jan 28 18:14 ./
drwxr-xr-x 20 root root 4096 Jan 28 15:38 ../
drwxr-xr-x 2 root root 12288 Jan 28 15:34 lost+found/
-rwxr-xr-x 1 root root 45948 Jan 28 18:10 ls*
```

As you can see, there's a copy of the executable binary for /bin/ls on the disk. But because the disk was mounted noexec, watch what happens when the executable is invoked:

```
# /disk2/ls
tcsh: /disk2/ls: Permission denied
```