The last-backed-up timestamp is stored in the file /etc/dumpdates, and a somewhat annoying characteristic of dump must be considered: it can only back up one partition or disk at a time. A quick glance at the output of df shows

```
# df
Filesystem     1k-blocks    Used Available Use% Mounted on
/dev/sda5      380791     102093   259038  29% /
/dev/sda1      49558      7797    39202  17% /boot
/dev/sda3      16033712   40416   1578808  1% /home
none           256436     0      256436  0% /dev/shm
/dev/sdb1      17224524   1310620  1558876  9% /usr
/dev/sdb2      253871     86739   154025  37% /var
```

Ignore /dev/shm because it's part of the virtual memory system, and you can see that there are five different partitions on this system. This means that you'll need to invoke dump five times to successfully backup the entire system.

2. To do a full backup within the Linux environment to a nonrewinding SCSI tape drive would therefore look like this:

```
dump -0uf /dev/nst0 /
dump -0uf /dev/nst0 /boot
dump -0uf /dev/nst0 /home
dump -0uf /dev/nst0 /usr
dump -0uf /dev/nst0 /var
```

Somewhat tedious, admittedly, but backup utilities are fairly crude in the world of Unix, even after 30 years of development.

The dump command has many starting flags, of which the most critical are highlighted in Table 7.3.

# TABLE 7.3 Critical Flags for dump

| Flag | Meaning |
|------|---------|
| 0-9 | Dump level. Level 0 is always a full dump. |
| -b size | Block size of the output device. |
| -f file | Send output to specified file or device. |
| -S | Estimate the amount of tape needed, without actually doing the backup itself. |
| -T date | Calculate what files to dump based on whether they're newer than the specified date. See ctime(3) for correct date format. |
| -u | Update the /etc/dumpdate file after a successful dump. |
| -W | Show which file systems need to be backed up, and when the last backup of each system was, if ever. |