
### Inodes

An inode is a data structure (page 1245), stored on disk, that defines a file's existence and is identified by an inode number. Use `ls` with the `-i` option to display the inode number of a file. An inode contains critical information about a file, such as the UID of the owner, where it is physically located on the disk, access mode, and how many hard links point to it. In addition, SELinux (page 472) stores extended information about files in inodes. Directory files, not inodes, hold filename information. This setup allows an inode to be associated with more than one filename and to be pointed to from more than one directory.

When you move (`mv`) a file, including a directory file, within a filesystem, you change the filename portion of the directory entry associated with the inode that describes the file. You do not create a new inode. If you move a file to another filesystem, `mv` first creates a new inode on the destination filesystem and then deletes the original inode. You can also use `mv` to move a directory recursively from one filesystem to another. In this case `mv` copies the directory and all the files in it and deletes the original directory and its contents.

### Hard Links

When you make an additional hard link (`ln`; page 204) to a file, you add a directory entry that points to the inode that describes the file. You do not create a new inode. It is not possible to create a hard link to a directory.

When you remove (`rm`) a file, you delete the directory entry that describes the file. When you remove the last hard link to a file, the operating system puts all blocks the inode pointed to back in the free list (a list of blocks that are available for use on the disk) and frees the inode to be used again.

### The . and ..

Every directory contains at least two entries (`.`, and `..`). The `.` entry is a link to the directory itself. The `..` entry is a link to the parent directory. In the case of the root directory, there is no parent; the `..` entry is a link to the root directory itself.

### Symbolic Links

Because each filesystem has a separate set of inodes, you can create hard links to a file only from within the filesystem that holds that file. To get around this limitation, Linux provides symbolic links, which are files that point to other files. Files that are linked by a symbolic link do not share an inode. As a consequence, you can create a symbolic link to a file from any filesystem. You can also create a symbolic link to a directory, device, or other special file. For more information refer to “Symbolic Links” on page 206.

## Device Special Files

Device special files (also called device files and special files) represent Linux kernel routines that provide access to an operating system feature. FIFO (first in, first out) special files allow unrelated programs to exchange information. Sockets allow unrelated processes on the same or different systems to exchange information. One type of socket, the UNIX domain socket, is a special file. Symbolic links are another type of special file.

### Device Files

Device files include both block and character special files and represent device drivers that allow the system to communicate with peripheral devices, such as terminals, printers, and hard disks. By convention, device files appear in the `/dev` directory and its subdirectories. Each device file represents a device; hence, the system reads from and writes to the file to read from and write to the device it represents. The following example shows part of a listing for the `/dev` directory:

```bash
$ ls -l /dev
crw-rw----. 1 root video   10, 175 01-25 12:17 agpgart
crw-------. 1 root root   10, 235 01-25 12:12 autofs
drwxr-xr-x. 2 root root   640 01-25 04:17 block
drwxr-xr-x. 2 root root    80 01-25 04:17 bsg
drwxr-xr-x. 3 root root    60 01-25 04:17 bus
lrwxrwxrwx. 1 root root     3 01-25 04:17 cdrom -> sr0
drwxr-xr-x. 2 root root  2760 01-25 12:17 char
crw-------. 1 root root    5,   1 01-25 12:17 console
lrwxrwxrwx. 1 root root    11 01-25 04:17 core -> /proc/kcore
...
brw-rw----. 1 root disk     8,  0 01-25 04:17 sda
brw-rw----. 1 root disk     8,  1 01-25 12:17 sda1
brw-rw----. 1 root disk     8,  2 01-25 04:17 sda2
...
```

The first character of each line is always `-`, `b`, `c`, `l`, or `p`, representing the file type—ordinary (plain), block, character, directory, symbolic link, or named pipe (next), respectively. The next nine characters identify the permissions for the file, followed by the number of hard links and the names of the owner and the group. Where the number of bytes in a file would appear for an ordinary or directory file, a device file shows *major* and *minor* device numbers (page 517) separated by a comma. The rest of the line is the same as for any other `ls -l` listing (page 191).

- **udev**: The `udev` utility manages device naming dynamically. It replaces `devfs` and moves the device-naming functionality from the kernel to userspace. Because devices are added to and removed from a system infrequently, the performance penalty associated with this change is minimal. The benefit of the move is that a bug in `udev` cannot compromise or crash the kernel.

- **/sys**: The `udev` utility is part of the hotplug system (next). When a device is added to or removed from the system, the kernel creates a device name in the `/sys` pseudofilesystem and notifies hotplug of the event, which is received by `udev`. The `udev` utility then creates the device file, usually in the `/dev` directory, or removes the device file from the system. The `udev` utility can also rename network interfaces. See the page at www.kernel.org/pub/linux/utils/kernel/hotplug/udev.html for more information.

- **Hotplug**: The hotplug system allows you to plug a device into a running system and use it immediately. Although hotplug was available in the Linux 2.4 kernel, the 2.6 kernel integrates hotplug with the unified device driver model framework (the *driver model core*) so any bus can report an event when a device is added to or removed from the system. User software can be notified of the event so it can take appropriate action. See linux-hotplug.sourceforge.net for more information.

## FIFO Special File (Named Pipe)

A *FIFO special file*, also called a *named pipe*, represents a pipe: You read from and write to the file to read from and write to the pipe. The term *FIFO* stands for *first in, first out*—the way any pipe works. In other words, the first information you put in one end is the first information that comes out the other end. When you use a pipe line on a command line to send the output of a program to the printer, the printer outputs the information in the same order that the program produced it and sent it to the pipeline.

Unless you are writing sophisticated programs, you will not be working with FIFO special files. However, programs use named pipes for interprocess communication. You can create a pipe using `mkfifo`:

```bash
$ mkfifo AA
$ ls -l AA
prw-rw-rw-      1 sam pubs 0 01-27 17:55 AA
```

The **p** at the left end of the output indicates the file is a pipe.

Both UNIX and Linux systems have included pipes for many generations. Without named pipes, only processes that were children of the same ancestor could use pipes to exchange information. Using named pipes, *any two* processes on a single system can exchange information. When one program writes to a FIFO special file, another program can read from the same file. The programs do not have to run at the same time or be aware of each other's activity. The operating system handles all buffering and information storage. This type of communication is termed *asynchronous* (*async*) because the programs on the opposite ends of the pipe do not have to be synchronized.

## Sockets

Like FIFO special files, UNIX/Linux domain *sockets* allow asynchronous processes that are not children of the same ancestor to exchange information. These sockets are the central mechanism of the interprocess communication that forms the basis of the networking facility. They differ from TCP/IP sockets, which are not represented in the filesystem. When you use networking utilities, pairs of cooperating sockets manage the communication between the processes on the local system and the remote system. Sockets form the basis of such utilities as `ssh` and `scp`.

## Major and Minor Device Numbers

A *major device number* points to a driver in the kernel that works with a class of hardware devices: terminal, printer, tape drive, hard disk, and so on. In the listing of the `/dev` directory on page 516, all the hard disk partitions have a major device number of 8.

A *minor device number* identifies a particular piece of hardware within a class. Although all hard disk partitions are grouped together by their major device number, each has a different minor device number (`sda1` is 1, `sda2` is 2, and so on). This setup allows one piece of software (the device driver) to service all similar hardware yet still be able to distinguish among different physical units.
