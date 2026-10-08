
## THE /proc FILE SYSTEM

A further interesting application of the /proc file system is the possibility of watching a running LINUX kernel in the debugger. Although you cannot set breakpoints, you can still look into internal data structures:

```gdb
(Linux):~$ gdb /usr/src/linux/vmlinux /proc/kcore
```

For compatibility with other systems, you can establish a symbolic link named /dev/core to the (virtual) file /proc/kcore. This file contains a kernel memory image in the 'core' format used by the debugger.

## 2.3.10 /root - the system administrator's home directory

Traditionally, the user root had the home directory /. This led to the practically unavoidable consequence that several files were created in / which made the root directory too large to retain a clear overview of the system. In order to keep this directory small with regard to the number of directory entries, today the /root directory is often used as the system administrator's home directory.

This directory should, however, be located in the root partition to allow the system administrator to log in even if further partitions are mounted. There are login programs which use / automatically as the home directory when the directory specified in the file /etc/passwd is not available, but there are also programs that refuse a login. In this case, the user root would be locked out from the system.

Electronic mail for the user root should be redirected to a normal user; this can be done by creating a file ~/.forward which contains the name of the user who is to receive the mail, a sendmail alias can be created. Similarly, the user root should not be used to read or write news, or to work on the system on a day-by-day basis.

## 2.3.11 /sbin - system programs needed for system start-up

The /sbin directory contains all the programs required for system start-up before the /usr file system is mounted, plus programs only needed by the system administrator. Programs that are also needed by non-privileged users should be stored in either /bin or /usr/bin, to prevent these users from having sbin directories in the search path. Important programs installed in the /sbin directory include, among others:

- The init program, responsible for system start-up. The system administrator can use it to change the runlevel - that is, the mode of operation of the LINUX system – for example, to switch the system into network server mode.

- Programs for file system maintenance and repair, such as example, mkfs, fsck, and fdisk. This group also includes the mkswap and swapon programs. Especially with computers with a small amount of main RAM, it is often necessary to create additional virtual memory before creating or checking file systems.

- Essential network programs, such as ifconfig or route, are used to initialize the network at system start-up and ensure that the /usr partition can be mounted via NFS.

Programs that can be employed by normal users in everyday operation, such as ping, shells, or tar, should be installed in the /bin directory if they are required for system start-up or restoring operations. The /bin and /sbin directories are not separated for reasons of system security. Therefore, these directories can (and should) be readable by all users, and the programs contained in them should be executable. Exceptions are obviously sensible for setuid or setgid programs (see Chapter 4).

## 2.3.12 /tmp - temporary files

This directory is where programs create temporary files. It is, however, not specified how long these files should be kept. On computers with a large amount of memory, the /tmp directory can be located on a RAM disk. The FHS recommends that the /tmp directory should be deleted at every reboot.

In other UNIX systems, it is standard practice for the /tmp directory to be deleted at every system start-up or at given intervals. For the latter, you may want to adapt the script shown in Listing 2.1 to your specific requirements. This shell script deletes files that have not been read during the past three days, and old, empty directories.

```bash
if [ -d /tmp ]; then
  cd /tmp; find -type f -atime +3 -exec rm -f {} \;
  find . ! -name -type d -atime +1 \; -exec rmdir {} > /dev/null 2>&1;
fi
```

Listing 2.1 Deleting the /tmp directory.

Please note that this script was not designed with security in mind and it can induce non-privileged users of the system to delete arbitrary files. The Red Hat distribution contains the tmp program for this purpose, which was developed with regard to security. For your home computer, the simple script is certainly sufficient, but in more complex environments it is definitely not secure enough.

The /tmp directory must be writable for all users, because many programs use it to create their temporary files. Examples are cronab or mail readers when an external editor is called. If /tmp directory is not writable, a great many programs will simply quit, leaving the reason for the crash unclear. For security reasons, the t bit should be set for this directory, so that users can only delete their own files.

It is equally annoying, however, if /tmp directory is full. If your computer is behaving in a strange way, have a look at the contents and access rights of the /tmp directory and the available disk space.

## 2.4 The /usr hierarchy

On many LINUX systems, the /usr file system occupies the lion's share of disk space. This is where most programs that are supplied with a distribution are installed. The same structure as the one described here could (and should) be recreated /usr/local. That is where the system administrator installs all programs needed locally for the computer in addition to what the distribution supplies.

The /usr file system contains data that can be used by different computers but do not need to be write-accessible. This allows the /usr file system to be mounted write-protected via NFS, or with a 'live' file system from a CD. This is an alternative to buying a new hard disk, especially when little hard disk space is available.

For large program packages such as TeX or emacs, no directories should be created directly under /usr, but a new directory under /usr/lib should be used. This is intended to prevent the /usr directory from becoming too large and complex. Table 2.3 shows an overview of the directories usually found under /usr.

| /usr | The /usr directory |
| :--- | :--- |
| - X11R6 | The X Window system |
| - bin | Practically all programs |
| - games | Games |
| - include | Header files for C programs |
| - lib | Libraries and program packages |
| - local | Local installations (initially empty) |
| - sbin | Programs for the system administrator |
| - share | Architecture-independent data |
| - src | Source code of various programs |

Table 2.3 Overview of the /usr hierarchy.

Until all programs have been adapted to the file system hierarchy standard, symbolic links such as shown in Table 2.4 should be established. Once all programs that use a directory of the old, now obsolete, structure have been recompiled, these links can be removed. This is generally the case with today's distributions.

| Old directory | New directory |
| :--- | :--- |
| /usr/adm | /var/adm |
| /usr/preserve | /var/preserve |
| /usr/spool | /var/spool |
| /usr/tmp | /var/tmp |
| /var/spool/locks | /var/lock |

Table 2.4 Compatibility links for /usr and /var.

### 2.4.1 The /usr/X11R6 directory

Release 6 of the X Window system is installed in this directory. This is both the path in which the binary distribution of the XFree86 team is installed and the default path if you want to compile X11R6 yourself. To facilitate system management and installation of additional X programs, and also compatibility with other systems, the symbolic links specified in Table 2.5 can be established.