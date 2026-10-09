files. Previous to AIX 5L, this type is information was hidden under the covers, but now that it has been made available to snoop into, extreme caution should be used at all times! This is not the place to ever try to store information or attempt to fix anything.

You can look at the statistics of the /proc pseudo-filesystem with either the df command or the mount command.

```
# df -k
Filesystem   1024-blocks  Free 6used  Iused 6Iused Mounted on
/dev/hd4       32768  3972  8% 1783  13% /
/dev/hd2      1212416 37544 97% 97689  13% /usr
/dev/hd9var    53248 25328 53% 596  5% /var
/dev/hd3       106496  99768  7% 168  1% /tmp
/dev/hd1        4096  3904  5% 42  5% /home
/dev/hd10opt   638976  22388 97% 15603  10% /opt
/proc           -     -     -     -     - /proc
# mount
node       mounted     mounted over   vfs    date      options
---------------------------------------------
/dev/hd4        /                     jfs     Feb 04 10:55 rw log=/dev/hd8
/dev/hd2        /usr                  jfs     Feb 04 10:55 rw log=/dev/hd8
/dev/hd9var     /var                  jfs     Feb 04 10:55 rw log=/dev/hd8
/dev/hd3        /tmp                  jfs     Feb 04 10:55 rw log=/dev/hd8
/dev/hd1        /home                 jfs     Feb 04 10:56 rw log=/dev/hd8
/dev/hd10opt    /opt                  jfs     Feb 04 10:56 rw log=/dev/hd8
/proc                     /proc      Feb 04 10:56 rw
```

Notice that in both df and mount, the /proc filesystem really has no statistics. This pseudo-filesystem does not have a size, a percentage used, or inodes. In the mount command output, /proc has a filesystem type of procs, as opposed to a jfs filesystem. The entry in the /etc/vfs file for procs is shown here:

```
# lsvfs procs
procs       6           none     none
```

Each process on the system is assigned a directory in /proc with a name equal to the PID of the process. Under each one of these process directories are several files and subdirectories that relate the corresponding internal control data structures of the process. Most, but not all, of these files are read-only, but some are available for process control and can be written to. The tools that are used to work with these files are the standard C language subroutines open(), read(), write(), and close(). A description of each of the data structures can be found in the /usr/include/sys/ procs.h file. All of the files in /proc are owned by the PID owner, a fact that allows regular users to access only the processes that they own.