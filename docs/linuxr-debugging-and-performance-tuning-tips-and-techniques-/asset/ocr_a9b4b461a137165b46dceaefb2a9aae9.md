The print_mount() function prints the information in the struct mntent. The output ends up being much the same as that of `cat /etc/mtab`:

```
```
$ ch08-mounted              Run the program

$ cat /proc/mounts
/dev/hda2       / ext3 rw 0 0
none /proc proc rw 0 0
usbdevfs /proc/bus/usb usbdevfs rw 0 0
/dev/hda5       /d ext3 rw 0 0
none /dev/pts devpts rw,gid=5,mode=620 0 0
none /dev/shm tmpfs rw 0 0
none /proc/sys/fs/binfmt_misc binfmt_misc rw 0 0
/dev/hda1       /win vfat rw,noexec,nosuid,nodev,uid=2076,gid=10,user=arnold 0 0
```
```

# 8.3 Retrieving Per-Filesystem Information

Printing per-filesystem information is all fine and good, but it’s not exciting. Once we know that a particular mount point represents a filesystem, we want information *about* the filesystem. This allows us to do things like print the information retrieved by `df` and `df -i`:

```
```
$ df                         Show free/used space

Filesystem       1K-blocks      Used Available Use% Mounted on
/dev/hda2        6199436    4940316    943248    84% /
/dev/hda5       61431520   27618536   30692360   48% /d
none             256616         0     256616    0% /dev/shm
/dev/hda1        8369532   2784700    5584832   34% /win

$ df -i                      Show free/used inodes

Filesystem       Inodes     IUsed     IFree IUse% Mounted on
/dev/hda2        788704    332216    555488   30% /
/dev/hda5        7815168   503243   7311925    7% /d
none                  1      64153       1% /dev/shm
/dev/hda1             0         0         - /win
```
```

# 8.3.1 POSIX Style: statvfs() and fstatvfs()

Early Unix systems had only one kind of filesystem. For them, it was sufficient if `df` read the superblock of each mounted filesystem, extracted the relevant statistics, and formatted them nicely for printing. (The superblock was typically the second block in the filesystem; the first was the *boot block*, to hold bootstrapping code.)

However, in the modern world, such an approach would be untenable. POSIX provides an XSI extension to access this information. The main function is called