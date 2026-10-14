
Table 7-4 shows the most important files in a user’s home directory:

| File | Description |
|---|---|
| `.profile` | Private login script of the user |
| `.bashrc` | Configuration file for bash |
| `.bash_history` | List of commands previously run in bash |

## Table 7-4

If there are no special settings, the home directories of all users are located beneath the `/home` directory. The home directory of a user can also be addressed via the shortcut `~`, so `~/.bashrc` refers to the file `.bashrc` in the user’s home directory.

In many cases, the /home directory is located on a different partition or can even be located on a different computer (with central administration of home directories).

## Libraries (/lib)

Many programs use specific functions that are also used by other programs. Such standard functions are removed from the actual program, stored in the system, and only called up when the program runs. They are called *shared libraries*.

The `/lib` directory contains the libraries that are used by programs in the `/bin` and `/sbin` directories. The kernel modules (hardware drivers not compiled into the kernel) are located in the `/lib/modules/` directory.

You can find additional libraries below the directory `/usr`.

## Mountpoints for Removable Media (media/*)

SUSE Linux creates directories in the `/media/` directory for removable media. It creates a separate directory for each kind of media it detects:

- `/media/floppy/`—Created for a floppy disk drive.
- `/media/cdrom/`—Created for a CD-ROM drive.
- `/media/cdrecorder`—Created for a CD burner.
- `/media/dvd/`—Created for a DVD drive.
- `/media/usbdisk/`—Created for a USB stick.
- `/media/medianame`—Created after inserting a labeled removable media.

## Application Directory (/opt)

Installed programs can store their static files in the `/opt` directory. First, a directory with the name of the application is created. The files are then stored in that directory. Examples include GNOME (`/opt/gnome`) and KDE (`/opt/kde3`).

## Home Directory of the Administrator (/root)

The home directory of the system administrator is not located beneath /home like that of a normal user. Preferably, it should be on the same partition as the root directory, “/”. Only then is it guaranteed that the user root can always log in without a problem and have his or her own configured environment available.

## System Binaries (/sbin)

The /sbin directory contains important programs for system administration. Programs that are run by normal users are also located in /bin.

Programs in the /sbin directory can also, as a rule, be run by normal users but only to display the configured values. Changes to the configuration can only be made by the user root.

Table 7-5 is an overview of important files in the /sbin directory.

| File | Description |
|---|---|
| `/sbin/SuSEconfig` | Starts the SuSEconfig modules in the directory `/sbin/conf.d/`. |
| `/sbin/conf.d/*` | Contains the scripts from the SuSEconfig family that are called up by `/sbin/SuSEconfig`. They are used to configure the overall system, evaluate entries in the configuration files in the `/etc/sysconfig/` directory, and write further configuration files. |
| `/sbin/yast` | Administration tool for SUSE Linux Enterprise Server. |
| `/sbin/fdisk` | Modifies partitions. |
| `/sbin/fsck*` | Checks file systems (file system check). |
| `/sbin/init` | Initializes the system. |
| `/sbin/mkfs*` | Creates a file system (formatting). |
| `/sbin/shutdown` | Shuts down the system. |

## Table 7-5

## Data Directories for Services (/srv)

The subdirectories of the /srv directory contain data of various services. For example, the files of the Apache Web server are located in the /srv/www/ directory and the FTP server files are located in the /srv/ftp/ directory.

## Temporary Area (/tmp)

Various programs create temporary files that are stored in /tmp until they are deleted.

## The Hierarchy Below /usr

The /usr directory, in accordance with the FHS, represents a second hierarchical layer. (/usr means *UNIX Special Resources* or *UNIX System Resources*.)

This is the location for all application programs, graphical interface files, additional libraries, locally installed programs, and commonly shared directories containing documentation. See Table 7-6.

| Directory | Description |
|---|---|
| `/usr/X11R6/` | Files of the X Window System |
| `/usr/bin/` | Almost all executable programs |
| `/usr/lib/` | Libraries |
| `/usr/local/` | Locally installed programs that are not part of the SUSE Linux Enterprise Desktop 10 distribution |
| `/usr/sbin/` | Programs for system administration |
| `/usr/share/doc/` | Documentation |
| `/usr/share/man/` | The manual pages (command descriptions) |
| `/usr/src/` | Source files of all programs and the kernel (if installed) |

## Table 7-6

## Variable Files (/var)

The /var directory and its subdirectories contain files that can be modified while the system is running.

Table 7-7 provides an overview of the most important directories beneath /var.

| Directory | Description |
|---|---|
| `/var/lib/` | Variable libraries (such as databases for the commands locate and rpm) |
| `/var/log/` | Log files for most services |
| `/var/run/` | Files with information on running processes |
| `/var/spool/` | Directory for queues (printers, e-mail) |
| `/var/lock/` | Lock files to protect devices from multiple use |

## Table 7-7

## Windows Partitions (/windows)

If YaST finds any partitions with a Microsoft file system, it automatically creates a /windows directory. Inside this directory are subdirectories labeled with Windows drive characters (C, D, and so on).

## Process Files (/proc)

Linux handles process information that is made available to users via the /proc directory. This directory does not contain any real files and therefore does not occupy any space on the hard disk.

The /proc directory is generated dynamically when it is accessed (for example, with ls /proc). It contains files and directories. Values in these files can be read as if they were in a regular file on the hard disk. Some values, such as kernel parameters, can also be set by writing to the corresponding files. Changes to this virtual file system only have an effect as long as the system is running; they do not persist across reboots.

Each process has its own directory. For example, the init process always has the process number 1. Information about it is therefore found in the /proc/1/ directory. This directory contains the following files:

```
```text
da10:~ # ls -l /proc/1
total 0
dr-xr-xr-x    3 root root 0 Apr 5 17:28 .
dr-xr-xr-x   62 root root 0 Mar 30 15:09 ..
dr-xr-xr-x    2 root root 0 Apr 5 17:36 attr
-r--r--r--    1 root root 0 Apr 5 17:36 auxv
-r--------    1 root root 0 Apr 5 17:28 cmdline
lrwxrwxrwx    1 root root 0 Apr 5 17:36 cwd -> /
-r--------    1 root root 0 Apr 5 17:36 delay
-r--------    1 root root 0 Apr 5 17:36 environ
lrwxrwxrwx    1 root root 0 Apr 5 17:28 exe -> /sbin/init
dr-x------    2 root root 0 Apr 5 17:36 fd
-rw-------    1 root root 0 Apr 5 17:36 map_base
-r--r--r--    1 root root 0 Apr 5 17:36 maps
-rw-------    1 root root 0 Apr 5 17:36 mem
-r--r--r--    1 root root 0 Apr 5 17:36 mounts
lrwxrwxrwx    1 root root 0 Apr 5 17:36 root -> /
-r--r--r--    1 root root 0 Apr 5 17:28 stat
-r--r--r--    1 root root 0 Apr 5 17:36 statm
-r--r--r--    1 root root 0 Apr 5 17:36 status
dr-xr-xr-x    3 root root 0 Apr 5 17:36 task
-r--r--r--    1 root root 0 Apr 5 17:36 wchan
da10:~ #
```
```

The files can be viewed with the cat command. For instance, the file /proc/1/status shows the status of the process, as in the following:

```
```text
da10:~ # cat /proc/1/status
Name: init
State: S (sleeping)
SleepAVG: 26%
Tgid: 1
Pid: 1
PPid: 0
TracerPid: 0
Uid: 0 0 0 0
Gid: 0 0 0 0
FDSize: 32
Groups:
VmSize: 588 kB
VmLck: 0 kB
VmRSS: 108 kB
VmData: 136 kB
VmStk: 8 kB
VmExe: 432 kB
VmLib: 0 kB
Threads: 1
SigPnd: 0000000000000000
ShdPnd: 0000000000000000
SigBlk: 0000000000000000
SigIgn: ffffffffff770d8fc
SigCgt: 00000000002882603
CapInh: 0000000000000000
CapPrm: 00000000ffffffff
CapEff: 00000000ffffffff
da10:~ #
```
```

In this example, a list displays what the process is called (init), what state it is in (sleeping), and to which user it belongs (Uid: 0 for root).

In addition to directories for each individual process, /proc also includes directories and files containing information about the state of the system.
