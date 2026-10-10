# Chapter 5: System Administration Tools

+   - **-1** This option limits the display to local filesystems—that is, the computer’s own hard disk, CD-ROM drive, and so on, excluding network filesystems.

+   - **-n** This option displays only information that’s already available in memory. Normally, df causes FreeBSD to query each filesystem as to its current state. If a filesystem has become unavailable, though, this won’t work. For instance, a network problem might prevent df from obtaining information on a network filesystem.

+   - **-t type** This option displays information only on filesystems of the specified type. You can specify multiple types by separating types with commas. For instance, df -t ufs,cd9660 causes df to display information only on FFS and ISO-9660 filesystems.

+   - **file | filesystem** You can limit the output to certain filesystems by listing them, either via their device filenames (such as `/dev/ad0s2h`) or their filesystem mount points (such as `/home`).

Information produced by this command includes the filesystem device, the filesystem size, the used space, the available space, the percentage of capacity filled, and the filesystem mount point. For instance, the following command displays information on one system, formatted for easy human consumption:

```
```
$ df -h
Filesystem   Size   Used Avail Capacity   Mounted on
/dev/ad0s2a  124M   62M   52M    54%      /
devfs         1.0K  1.0K    0B    100%    /dev
/dev/ad0s2h   1.8G 486M  1.2G    29%      /home
/dev/ad0s2f  145M  31M  103M    23%      /tmp
/dev/ad0s2g   1.6G  1.2G  269M    82%      /usr
/dev/ad0s2e   145M  7.4M  126M     6%      /var
/dev/ad0s1    2.0G 697M  1.3G     34%      /windows
procfs        4.0K  4.0K    0B     100%    /proc
speaker:/home  4.5G  1.7G  2.8G    38%      /speaker:/home
```
```

This output reveals that the root (/) filesystem is 124MB in size and is 54 percent full, that /home is 29 percent full, and so on. The /speaker:/home filesystem is a network mount, as indicated by the speaker:/home device name—this is really an NFS mount specification. The /dev and /proc filesystems are special virtual filesystems—they don’t correspond to physical partitions or other devices, but are generated on the fly for special purposes. Thus, the fact that they’re both reported as having 0 bytes free isn’t a problem. The fact that /usr is 82 percent full is potentially more troublesome, should the need arise to add more than 269MB of new programs. In practice, it’s usually best to keep a few megabytes free on /usr (or on the root partition, if there’s no separate /usr partition).

![](bbox=[0.92, 0.25, 0.97, 0.45])