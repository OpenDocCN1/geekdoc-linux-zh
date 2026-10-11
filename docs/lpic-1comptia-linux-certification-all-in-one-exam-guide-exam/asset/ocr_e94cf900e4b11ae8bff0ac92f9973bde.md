```
tmpfs          tmpfs      246M   232M   246M    1% /dev/shm
/dev/sda1       ext4       ≈98M    25M    69M    27% /boot
/dev/sda4       ext4       3.0G   196M    2.7G    7% /
/dev/sdb1       ext4       6.1G   141M    5.6G    3% /mnt/extraspace
wsl1:~ #
```

Another useful option you can use with `df -i`, which lists inode usage information instead of disk space usage. Recall earlier in this chapter that when a file system is created on a partition, a fixed maximum number of inodes is assigned. If the file system stores a huge number of very small files, then it's possible for it to run out of inodes even though there is plenty of disk space still available. You can monitor inode usage using the `df -i` command, as shown here:

```
wsl1:~ # df -i
Filesystem      Inodes  IUsed   IFree  IUse%  Mounted on
/dev/sda3     5242188 155903 368385    30% / 
/dev/sda5        62602   687  61915     2% /dev
  tmpfs        62961   12  62949     1% /dev/shm
/dev/sda1        25896    40  25856     1% /boot
/dev/sda4       196800  1345 195455     1% /var
/dev/sdb1       402192    12 402180     1% /mnt/extraspace
wsl1:~ #
```

Another utility you can use to monitor disk space usage is the `du` utility. Its function is to provide you with a summary of disk space usage of each file, recursively, for a specified directory. The syntax is `du directory`. Some useful options you can use with `du` include the following:

+   - `-c` Calculate a grand total.
+   - `-h` Display in human-readable format.
+   - `exclude filename_or_pattern` Excludes all files that match the specified filename or pattern.

The `-h` option is the most useful one, in my experience. Here is an example of viewing the space used by files in the `/tmp` directory in human-readable format:

```
wsl1:~ # du -h /tmp
4.0K  /tmp/tracker-tux
4.0K  /tmp/.ICE-unix
4.0K  /tmp/virtual-tux.F5Cebv
36K   /tmp/hsperfdata_root
4.0K  /tmp/tracker-root
4.0K  /tmp/pulse-lqlPdtp8gsL
4.0K  /tmp/pulse-las83DyyhRR
4.0K  /tmp/.esd-1001
4.0K  /tmp/unique
4.0K  /tmp/orbit2-gdm
4.0K  /tmp/virtual-tux.ZKQpyRR
4.0K  /tmp/.esd-107
4.0K  /tmp/virtual-tux.J6cNKY
4.0K  /tmp/.esd-0
4.0K  /tmp/pulse-Iuf4flp9j9NB
4.0K  /tmp/X11-unix
4.0K  /tmp/virtual-tux.u5tda2
4.0K  /tmp/.esd-1000
```