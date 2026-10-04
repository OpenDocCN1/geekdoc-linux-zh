```
$ kill 325
$ ps
PID TTY STAT TIME COMMAND
325 v01 S 0:00 -bash
460 v02 S 0:00 -bash
559 v02 R 0:00 ps
$ kill -9 325
$ ps
PID TTY STAT TIME COMMAND
460 v02 S 0:00 -bash
561 v02 R 0:00 ps
```

First, the tty command shows that the user is currently switched to virtual terminal 2. A ps command then gives the PID of the shell on virtual terminal 1 as 325. A kill command to this PID followed by a second ps shows that the shell is able to ignore the default signal to terminate. However, a second kill command to the same PID using a -9 switch does terminate the shell, as seen from the final call to ps.

# 2.7 Space

In addition to processes, there are several system resources that it is useful to be able to monitor, the most common being disk space and memory space. In order to see on a per filesystem basis the amount of disk space available and in use, you use the df command:

```
$ df
Filesystem 1024-blocks Used Available Capacity Mounted on
/dev/hda3 199270 182354 6625 96% /
/dev/hda1 610608 209675 369394 36% /usr
/dev/hda4 199271 147953 41027 78% /home/pc
```

The numbers and sizes of partitions on your system will obviously differ from this example, but the principle is the same. The first column in the df listing specifies the pathname of the special file that represents the disk partition. The second column gives the number of 1024-byte data blocks contained in the partition, with third and fourth columns being the number of these blocks in use and available respectively. You may be surprised to discover that the values in the fourth column when added to those in the third column do not add up the numbers in the second column. This is because, by default, a small percentage of the space on each partition is reserved for use by the system administrators so that they can login and still have some working space for sorting out problems, even when the filesystems are full as far as ordinary users are concerned.