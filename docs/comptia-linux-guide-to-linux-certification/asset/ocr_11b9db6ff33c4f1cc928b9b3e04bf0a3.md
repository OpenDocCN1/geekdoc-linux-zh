computer. In the following output, you see that /dev/fd0 and /dev/fd1 share the same major number of 2, yet the minor number for /dev/fd0 is 0 and the minor number for /dev/fd1 is 1, which differentiates them from each other.

```
[root@server1 ~]# ls -1/dev/fd0 /dev/fd1
brw-rw---- 1 root floppy 2, 0 Feb 23 16:02 /dev/fd0
brw-rw---- 1 root floppy 2, 1 Feb 23 16:02 /dev/fd1
[root@server1 ~]#_ 
```

Together, the device file type (block or character), the major number (device driver), and the minor number (specific device) make up the unique characteristics of each device file. To create a device file, you simply need to know these three pieces of information.

If a device file becomes corrupted, it is usually listed as a regular file instead of a block or character special file. Recall from Chapter 4 that the find /dev -type f command can be used to search for regular files underneath the /dev directory to identify whether corruption has taken place. If you find a corrupted device file or accidentally delete a device file, the mknod command can be used to re-create the device file if you know the type, major, and minor numbers. An example of re-creating the /dev/fd0 block device file used earlier with a major number of 2 and a minor number of 0 is shown in the following example:

```
[root@server1 ~]# ls -1/dev/fd0
brw-rw---- 1 root floppy 2, 0 Feb 23 16:02 /dev/fd0
[root@server1 ~]# rm -f /dev/fd0
[root@server1 ~]# ls -1/dev/fd0
[root@server1 ~]# mknod /dev/fd0 b 2 0
[root@server1 ~]# ls -1/dev/fd0
brw-r-r-- 1 root root 2, 0 May 8 13:26 /dev/fd0
[root@server1 ~]#_ 
```

To see a list of devices that are currently used on the system and their major numbers, you can view the contents of the /proc/devices file, as shown here:

```
[root@server1 ~]# cat /proc/devices
Character devices:
1 mem
4 /dev/vc/0
4 tty
4 ttyS
5 /dev/tty
5 /dev/console
5 /dev/ptmx
7 vcs
10 misc
13 input
14 sound
21 sg
29 fb
116 alsa
128 ptp
136 pts
```