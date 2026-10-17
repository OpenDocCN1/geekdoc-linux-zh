
### Combining the du command

Although the `du` command does not, like the `df` command, have a `-x` option to exclude other filesystems. Or, if you have `du` report on all other filesystems by using a usage report at the mount point. For example, `du` will merrily chunk and summarize how much room your Windows directories take up:

```
# du -b --summarize /mnt/*; sort -nr

12948405 /mnt/windows

23929345 /mnt/soffice

2081184 /mnt/photosen

7740406 /mnt/transit

8628992 /mnt/org2

8647520 /mnt/lapink

5556496 /mnt/atobat3

4041127 /mnt/pocr

3753962 /mnt/psp

3603469 /mnt/insync

3176769 /mnt/antivirus

2669335 /mnt/airirlite

2408920 /mnt/winfax
```

This (shortened) report shows that next to the operating system, the largest space is taken up by certain applications. This information can be helpful in making a decision on what applications to uninstall if you need more disk space.

### Checking Symbolic Links with the stat Command

The `stat` command will give you a lot of information about a file or directory. Much of this information is technical, but you may find the `stat` command useful for checking symbolic links. The `stat` command does not have any command-line options, but you can specify directories or filenames, for example:

```
# stat ./
File: ""
Filetype: Directory
Size: 2048
Mode: (0775/drwxr-xr-x) UID: (500/bball) Gid: (500/bball)
Device: 3, Inode: 9932 Links: 19
Access: Wed Nov 19 17:20:42 1997 (00000.00:04:16)
Modify: Wed Nov 19 16:52:12 1997 (00000.00:42:16)
Change: Wed Nov 19 16:52:12 1997 (00000.00:42:16)
```

You can see that the `stat` command shows who the file or directory belongs to, along with permissions, and other information. If you want use `stat` to check symbolic links, you can try:

- `touch file1`
- `ln -s file1 file2`

### Saving Space

If this is too much information for you, then you can use the `--summarize` option to get the total in kilobytes or bytes, as follows:

```
# du -b --summarize
26786903
```

The command can also help you keep track of directories which, unattended, sometimes grow out of control or use a lot of disk space. If you specify a path, `du` will report on the different size of the directories, pinpointing any that may contain too much information, for example:

```
# du --summarize -b /var/*; sort -nr
647535 /var/lib
2336494 /var/log
868183 /var/catman
73562 /var/spool
14591 /var/dt
2385 /var/run
2048 /var/lock
2048 /var/local
1024 /var/tmp
1024 /var/preserve
1024 /var/nis
```

### Getting Memory Information

Although the industry trend has been to offer more hard drive space and more memory for less, many people don't outlay cash to expand their systems. The good news is that Linux is very efficient at using memory, even a 16MB system provides enough room (with an equal amount of swap space) to run X11 and most programs well. The bad news is that programs are getting larger the time, especially with feature creep, which more and more functions creep into programs. This section introduces you to some programs you may find helpful in understanding your system's memory, and gives you some tips on conserving memory.

### Memory Reporting with the free Command

The `free` command shows breakdowns of the amounts and totals of free and used memory, including your swap usage. It has several command-line options, but is easy to run and understand, for example:

```
# free
```

| Mem: | used | free | shared | buffers | cached |
|---|---|---|---|---|---||
| -/+ buffers: | 30892 | 28004 | 2888 | 14132 | 3104 | 10444 |
| Swap: | 34268 | 7964 | 26304 | | | |
