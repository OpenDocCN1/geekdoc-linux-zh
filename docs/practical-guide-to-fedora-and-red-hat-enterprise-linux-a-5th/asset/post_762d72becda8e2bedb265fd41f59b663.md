
password that passwd puts into this file. When setting up new user accounts manually, run passwd as Superuser to assign a password to a new user.

The last-mod field indicates when the password was last modified. The min is the minimum number of days that must elapse before the password can be changed; the max is the maximum number of days before the password must be changed. The warn specifies how much advance warning (in days) to give the user before the password expires. The account will be closed if the number of days between login sessions exceeds the number of days specified in the inactive field. The account will also be closed as of the date in the expire field. The last field in an entry, flag, is reserved for future use. You can use the Password Info tab in system-config-users ("Modifying a user" on page 556) to modify these fields.

The shadow password file should be owned by root and should not be publicly readable or writable. Setting ownership and permissions this way makes it more difficult for someone to break into the system by identifying accounts without passwords or by using specialized programs that try to match hashed passwords.

A number of conventions exist for creating special shadow entries. An entry of *\** or NP in the password field indicates locked or no password, respectively. No password is different from an empty password, implying that this is an administrative account that no one ever logs in on directly. Occasionally programs will run with the privileges of this account for system maintenance functions. These accounts are set up under the principle of least privilege (page 406).

Entries in the shadow file must appear in the same order as in the passwd file. There must be exactly one shadow entry for each passwd entry.

## /etc/sysconfig

A directory containing a hierarchy of system configuration files. For more information refer to the /usr/share/doc/initscripts\*/sysconfig.txt file.

## /proc

The /proc pseudofilesystem provides a window into the Linux kernel. Through /proc you can obtain information on any process running on your computer, including its current state, memory usage, CPU usage, terminal, parent, and group. You can extract information directly from the files in /proc. An example follows:

```
$ sleep 1000 &
[1] 4567
$ cd /proc/4567
$ ls -l
total 0
dr-xr-xr-x 2 sam sam 0 Jan 25 21:57 attr
-r--r----- 1 sam sam 0 Jan 25 21:57 auxv
-r-----r-- 1 sam sam 0 Jan 25 21:57 cmdline
lrwxrwxrwx 1 sam sam 0 Jan 25 21:57 cwd -> /home/sam
-r--r----- 1 sam sam 0 Jan 25 21:57 environ
lrwxrwxrwx 1 sam sam 0 Jan 25 21:57 exe -> /bin/sleep
dr-x------ 2 sam sam 0 Jan 25 21:57 fd
...
-r--r--r-- 1 sam sam 0 Jan 25 21:57 status
dr-xr-xr-x 3 sam sam 0 Jan 25 21:57 task
-r--r--r-- 1 sam sam 0 Jan 25 21:57 wchan
```

```
$ cat status
  Name:   sleep
  State:  S (sleeping)
  SleepAVG: 78%
  Tgid:   4567
  Pid:    4567
  Ppid:   4548
  TracerPid:    0
  Uid:    500     500     500     500
  Gid:    500     500     500     500
  FDSize: 256
  Groups: 500
  VmPeak:    3584 kB
  VmSize:    3584 kB
  . . .
```

In this example, bash creates a background process (PID 4567) for sleep. Next the user changes directories to the directory in /proc that has the same name as the PID of the subject background process (cd /proc/4567). This directory holds information about the process for which it is named. In this case, it holds information about the sleep process. The ls -l command shows that some entries in this directory are links (cwd is a link to the directory the process was started from, and exe is a link to the executable file that this process is running) and some appear to be ordinary files. All appear to be empty. When you cat one of these pseudofiles (status in the example), you get the output shown. Obviously this is not an ordinary file.

### /sbin/shutdown

A utility that brings the system down (see page 433).

### swap

Even though swap is not a file, swap space can be added and deleted from the system dynamically. Swap space is used by the virtual memory subsystem. When it runs low on real memory (RAM), the system writes memory pages from RAM to the swap space on the disk. Which pages are written and when they are written are controlled by finely tuned algorithms in the Linux kernel. When needed by running programs, these pages are brought back into RAM—a technique called paging (page 1098). When a system is running very short on memory, an entire process may be paged out to disk.

Running an application that requires a large amount of virtual memory may result in the need for additional swap space. If you run out of swap space, you can use mkswap to create a new swap file and swapon to enable it. Normally you use a disk partition as swap space, but you can also use a file. A disk partition provides much better performance than a file.

If you are using a file as swap space, first use df to ensure that the partition has adequate space for the file. In the following sequence of commands, the administrator first uses dd and /dev/zero (page 470) to create an empty file (do not use cp as you may create a file with holes, which may not work) in the working directory. Next mkswap takes as an argument the name of the file created in the first step to set up the swap space. For security reasons, change the file so that it cannot be read from or written to by anyone but root. Use swapon with the same argument to turn the swap file on; then use swapcon -s to confirm that the swap space is available. The final two commands turn off the swap file and remove it:

```
# dd if=/dev/zero of=swapfile bs=1024 count=65536
65536+0 records in
65536+0 records out
67108864 bytes (67 MB) copied, 0.684039 seconds, 98.1 MB/s
# mkswap swapfile
Setting up swapspace version 1, size = 67104 kB
# chmod 600 swapfile
# swapon swapfile
# swapcon -s
Filename		Type		Size	Used	Priority
/dev/sda5	partition	1020088	0	-1
/root/swapfile	file		65528	0	-2
# swapoff swapfile
# rm swapfile
rm: remove regular file 'swapfile'? y
```

### /sys

The /sys pseudofilesystem was added in the Linux 2.6 kernel to make it easy for programs running in kernel space, such as device drivers, to exchange information with programs running in user space. Refer to udev on page 482.

### /usr/share/magic

Most files begin with a unique identifier called a *magic number*. This file is a text database listing all known magic numbers on the system. When you use the file utility, it consults /usr/share/magic to determine the type of a file. Occasionally you may acquire a new tool that creates a new type of file that is unrecognized by the file utility. In this situation you need to update the /usr/share/magic file; refer to the magic man page for details. See also “magic number” on page 1092.

### /var/log

Holds system log files.

### /var/log/messages

Contains messages from daemons, the Linux kernel, and security programs. For example, you will find filesystem full warning messages, error messages from system daemons (NFS, rsyslog, printer daemons), SCSI and IDE disk error messages, and more in messages. Check /var/log/messages periodically to keep informed about important system events. Much of the information displayed on the system console is also sent to messages. If the system experiences a problem and you cannot access the console, check this file for messages about the problem.

### /var/log/secure

Holds messages from security-related programs such as su and the sshd daemon.

## FILE TYPES

Linux supports many types of files. The following sections discuss these types of files:

-   Ordinary files, directories, links, and inodes (discussed next)
-   Symbolic links (page 481)
-   Special files (page 482)
-   FIFO special file (named pipe) (page 483)
-   Sockets (page 483)
-   Block and character devices (page 484)
-   Raw devices (page 485)

## ORDINARY FILES, DIRECTORIES, LINKS, AND INODES

### Ordinary and directory files

An *ordinary* file stores user data, such as textual information, programs, or images, such as a *jpeg* or *tiff* file. A *directory* is a standard-format disk file that stores information, including names, about ordinary files and other directory files.

### Inodes

An *inode* is a *data structure* (page 1078), stored on disk, that defines a file's existence and is identified by an inode number. An inode contains critical information, such as the name of the owner of the file, where it is physically located on the disk, and how many hard links point to it. In addition, SELinux (page 414) stores extended information about files in inodes. A directory relates each of the filenames it stores to an inode.

When you move (*mv*) a file within a filesystem, you change the filename portion of the directory entry associated with the inode that describes the file. You do not create a new inode. If you move a file to another filesystem, *mv* first creates a new inode on the destination filesystem and then deletes the original inode. You can also use *mv* to move a directory recursively, in which case all files in the directory are copied and deleted.

When you make an additional hard link (*ln*, page 214) to a file, you create another reference (an additional filename) to the inode that describes the file. You do not create a new inode.

When you remove (*rm*) a file, you delete the directory entry that describes the file. When you remove the last hard link to a file, the operating system puts all blocks the inode pointed to back in the *free list* (the list of blocks that are available for use on the disk) and frees the inode to be used again.

### The . and .. directory entries

Every directory contains at least *two* entries (., and ..). The . entry is a link to the directory itself. The .. entry is a link to the parent directory. In the case of the root directory, there is no parent and the .. entry is a link to the root directory itself. It is not possible to create hard links to directories.

### Symbolic links

Because each filesystem has a separate set of inodes, you can create hard links to a file only from within the filesystem that holds that file. To get around this limitation, Linux provides *symbolic* links, which are files that point to other files. Files that are linked by a symbolic link do not share an inode. As a consequence, you can create a symbolic link to a file from any filesystem. You can also create a symbolic link to a directory, device, or other special file. For more information refer to "Symbolic Links" on page 216.
