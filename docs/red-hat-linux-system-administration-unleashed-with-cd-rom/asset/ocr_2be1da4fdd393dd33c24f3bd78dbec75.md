```
; -- tmp   temporary file space
; -- usr   base of the secondary hierarchy
; -- var   variable system data including system logs
```

Some restrictions placed on the root directory are that no applications be allowed to create or require special files in the root directory, and that the contents of the root directory be kept to a minimum. This becomes clearer as we examine each of the directories found in the root filesystem.

The first directory in the preceding list is the /bin directory, which contains commands essential to system operation. The FHS contains a list of the files that should be found there. These commands fall into three categories:

+   - General commands
+   - Restoration commands
+   - Network commands

The first category includes commands such as ls, cp, mv, and rm. It also includes the Bourne and C-shells or their equivalents, such as ash, bash, or tcsh. Essential commands are those that system initialization scripts use and those required to access other filesystems, such as /usr and /var after the system has booted.

The second category of commands is loosely defined to be the minimal set required to restore other parts of the system, such as tar, gzip, or other commands used by your backup system.

The final category of commands are network commands and include hostname, domainname, netstat, and ping. Regardless of the category, these are commands that both root and normal users may need to run, as opposed to those intended for administrative use only, such as those found in /sbin. The next directory in the diagram is /boot, which contains files required by the boot loader program. Files may include map files, kernel images, and other data not normally edited by hand. The commands required to create boot loader maps should be located in /sbin, and configuration files for the boot loader should be kept in the /etc directory. There may be restrictions on where this directory is physically located, such as on some personal computers based on the Intel iX86 family of processors, which require that these files be located below cylinder 1024, or other restrictions as to the filesystem type on which these files are located. In such cases, the filenames can be altered to conform to the restrictions of the filesystem in question.

Unlike Windows and other popular operating systems, each device available on Linux and other UNIX systems is represented by a special file that you can access using normal file semantics. The /dev directory contains these device special files. In addition to these files, this directory may also contain a program or script called MAKEDEV that is used to create