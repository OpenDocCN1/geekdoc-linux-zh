# Commands for checking disk-space usage

I want to tell you about two commands — `df` and `du` — that you can use to check the disk-space usage on your system. These commands are simple to use. The `df` command shows you a summary of disk-space usage for all mounted devices. For example, here’s the result of typing `df` on one of my PCs running SUSE Linux:

```
Filesystem             1K-blocks       Used Available Use% Mounted on
/dev/hda11             6357688     1994348  4363340  32% /
tmpfs                  124004          36   123968   1% /dev/shm
/dev/hda7                43885       69749    31870  24% /boot
/dev/hdc               6464234      664234        0 100% /media/cdrecorder
```

The output is a table that lists the device, the total kilobytes of storage, how much is in use, how much is available, the percentage being used, and the mount point.

To see the output of `df` in a more human-readable format, type **df -h**. Here is the output of the `df -h` command:

![](bbox=[0.1313, 0.4162, 0.207, 0.4886])

```
Filesystem             Size  Used Avail Use% Mounted on
/dev/hda11             6.1G  2.0G  4.2G  32% /
tmpfs                  122M  3.6K   122M   1% /dev/shm
/dev/hda7              43M   9.6M    32M  24% /boot
/dev/hdc              649M   649M     0  100% /media/cdrecorder
```

If you compare this output with the output of plain `df` (see previous listing), you see that `df -h` prints the sizes with terms like M for megabytes and G for gigabytes. These are clearly easier to understand than 1K-blocks.

The other command — `du` — is useful for finding out how much space a directory takes up. For example, type **du /etc/X11** to view the contents of all the directories in the `/etc/X11` directory. (This directory contains X Window System configuration files.) You end up with a list that looks similar to the following:

```
4          /etc/X11/fs
4          /etc/X11/twm
84         /etc/X11/xdm/pixmaps
153        /etc/X11/xdm
372        /etc/X11/xkb/rules
44         /etc/X11/xkb/types
... lines deleted ...
40         /etc/X11/xstart
4          /etc/X11/proxymngr
2920       /etc/X11
```