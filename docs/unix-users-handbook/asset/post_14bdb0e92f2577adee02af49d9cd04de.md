
It is highly desirable for a system administrator to keep applications separate from the operating system, so you don’t inadvertently have application files overwriting operating system files. In addition, if applications are loaded in a separate area, they are “modular,” meaning that a system administrator can add, remove, and modify them without affecting the operating system or other applications. Applications are kept in the /opt directory.

- Intrasystem files are kept in a separate area from intersystem, or network-accessible files. /usr and /sbin are shared operating system directories. No host specific information is in these two directories. /etc is used to hold the host-specific configuration files.
- Executable files are kept separate from system configuration files so that the executables may be shared among hosts. Having the configuration files separate from the programs that use them also means that updates to the operating system won’t affect the configuration files.

I provide descriptions of some of the most important directories of the file system layout.

/ This is the root directory, which is the base of the file system’s hierarchical tree structure. A directory is logically viewed as being part of /. Regardless of the disk on which a directory or logical volume is stored, it is logically viewed as a part of the root hierarchy.

*/dev* Contains host-specific devices files.

*/etc* Contains host-specific system and application configuration files. The information in this directory is important to the operation of the system and is of a permanent nature. There are also additional configuration directories below */etc*. There are two */etc* subdirectories of particular interest:

*/export* Servers export root directories for networked clients. For instance, a server might export user directories such as */export/home/username*.

*/home* Users’ home directories are located here. Because the data stored in users’ home directories will be modified often, you can expect this directory to grow in size.

*/kernel* Contains kernel configuration and binary files that are required to bring up a system such as genux.

*/lost+found* This is the lost files directory. Here you find files that are in use but are not associated with a directory. These files typically become “lost” as a result of a system crash that caused the link between the physical information on the disk and the logical directory to be severed. The program **fsck**, which is run at the time of boot, finds these files and places them in the **lost+found** directory.

**/mnt** This directory is reserved as a mount point for local file systems. You can either mount directly to **/mnt** or have **/mnt** subdirectories as mount points such as **/mnt1**, **/mnt2**, **/mnt3**, etc.

**/net** Name reserved as mount points for remote file systems.

**/opt** The directory under which applications are installed. As a rule, application vendors never specify a particular location for their applications to be installed. Now, with **/opt**, we have a standard directory under which applications should be installed. This is an organizational improvement for system administrators, because we can now expect applications to be loaded under **/opt** and the application name.

**/sbin** Contains commands and scripts used to boot, shut down, and fix file system mounting problems. **/sbin** is available when a system boots, because it contains commands required to bring up a system.

/stand Contains kernel configuration and binary files that are required to bring up a system. Two significant files contained in this directory are the system and vmunix (kernel) files.

/tmp This is a free-for-all directory where any user can *temporarily store* files. Because of the loose nature of this directory, it should not be used to store anything important, and users should know that whatever they have stored in /tmp can be deleted without notice. Application working files should go in /var/tmp or /var/opt/appname, not in /tmp.

/usr Most of the UNIX operating system is contained in /usr. Included in this directory are commands, libraries, and documentation. A limited number of subdirectories that can appear in /usr.

/var Holds files that are primarily temporary. Files such as log files, which are frequently deleted and modified, are stored here. Think of this as a directory of "variable" size. Files that an application or command create at runtime should be placed in this directory, including log and spool files. However, some applications may store state information in /var.

## Linux File System Layout

The Linux file system layout is very similar to the other UNIX variants described earlier, both in concept and in implementation. Files are contained in directories, and directories can have any number of subdirectories. Most operating systems are arranged this way, including UNIX.

The following is a long listing at the root level of a Caldera Linux system:

![](img/75f39fc91296b889c0653851accdfd46_105_0.png)

```
# ls -l /
total 439
-rw-rw-rw-    1 root      root          23 Nov  5 07:10 .lgdb
... (multiple lines of file listing including ., .., amd, auto, bin, boot, dev, etc, home, initrd, install, LST, lib, lost+found, mnt, opt, proc, root, sbin, tmp, usr, var, vmlinuz)
... (truncated)
```

Most of the directories are the same as those described earlier. A couple of directory names did not appear earlier that are significant. The Linux kernel, **vmlinuz**, appears at the root level. The directory **/root** is the home directory of the user *root*.

The **/proc** directory contains information about the Linux system. The **/proc** directory is really a set of data structure information that looks like a directory. The following is a long listing of the /proc directory:

```
# ls -l /proc
total 0
dr-xr-xr-x    3 root     root            0 Nov  7 00:13 1
dr-xr-xr-x    3 root     root            0 Nov  7 00:16 1011
dr-xr-xr-x    3 root     root            0 Nov  7 00:13 104
dr-xr-xr-x    3 bin      root            0 Nov  7 00:13 106
dr-xr-xr-x    3 root     root            0 Nov  7 00:13 116
dr-xr-xr-x    3 root     root            0 Nov  7 00:13 118
dr-xr-xr-x    3 root     root            0 Nov  7 00:13 146
dr-xr-xr-x    3 root     root            0 Nov  7 00:13 155
dr-xr-xr-x    3 root     root            0 Nov  7 00:13 156
dr-xr-xr-x    3 daemon   root            0 Nov  7 00:13 162
dr-xr-xr-x    3 root     root            0 Nov  7 00:13 167
dr-xr-xr-x    3 root     root            0 Nov  7 00:13 170
dr-xr-xr-x    3 root     65535           0 Nov  7 00:13 178
dr-xr-xr-x    3 root     root            0 Nov  7 00:13 18
dr-xr-xr-x    3 root     root            0 Nov  7 00:13 19
dr-xr-xr-x    3 nobody   65535           0 Nov  7 00:13 193
dr-xr-xr-x    3 root     root            0 Nov  7 00:13 199
dr-xr-xr-x    3 root     root            0 Nov  7 00:13 2
dr-xr-xr-x    3 root     root            0 Nov  7 00:13 20
dr-xr-xr-x    3 root     root            0 Nov  7 00:13 200
dr-xr-xr-x    3 root     root            0 Nov  7 00:13 201
dr-xr-xr-x    3 root     root            0 Nov  7 00:13 202
dr-xr-xr-x    3 root     root            0 Nov  7 00:13 203
dr-xr-xr-x    3 root     root            0 Nov  7 00:13 204
dr-xr-xr-x    3 root     root            0 Nov  7 00:13 205
dr-xr-xr-x    3 root     root            0 Nov  7 00:13 21
dr-xr-xr-x    3 root     root            0 Nov  7 00:13 273
dr-xr-xr-x    3 root     root            0 Nov  7 00:13 274
dr-xr-xr-x    3 root     root            0 Nov  7 00:13 276
dr-xr-xr-x    3 root     root            0 Nov  7 00:13 3
dr-xr-xr-x    3 root     root            0 Nov  7 00:13 307
dr-xr-xr-x    3 root     root            0 Nov  7 00:13 327
dr-xr-xr-x    3 root     root            0 Nov  7 00:13 358
dr-xr-xr-x    3 root     root            0 Nov  7 00:13 375
dr-xr-xr-x    3 root     root            0 Nov  7 00:13 443
dr-xr-xr-x    3 root     root            0 Nov  7 00:13 444
dr-xr-xr-x    3 root     root            0 Nov  7 00:13 445
dr-xr-xr-x    3 root     root            0 Nov  7 00:13 45
dr-xr-xr-x    3 root     root            0 Nov  7 00:13 482
dr-xr-xr-x    3 root     root            0 Nov  7 00:13 483
dr-xr-xr-x    3 root     root            0 Nov  7 00:16 996
dr-xr-xr-x    3 root     root            0 Nov  7 00:16 997
dr-xr-xr-x    3 root     root            0 Nov  7 00:16 998
-r--r-----    1 root     root            0 Nov  7 00:13 cmdline
-r--r-----    1 root     root            0 Nov  7 00:13 cpuinfo
-r--r-----    1 root     root            0 Nov  7 00:13 devices
-r--r-----    1 root     root            0 Nov  7 00:13 dma
-r--r-----    1 root     root            0 Nov  7 00:13 filesys
-r--r-----    1 root     root            0 Nov  7 00:13 interrupt
-r--r-----    1 root     root            0 Nov  7 00:13 ioports
-r--------    1 root     root        33558528 Nov  7 00:13 kcore
```
