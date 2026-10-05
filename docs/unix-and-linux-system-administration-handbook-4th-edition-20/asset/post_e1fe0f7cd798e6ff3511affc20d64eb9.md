
## Table 6.2 Standard directories and their contents

| Pathname | OS* | Contents |
| --- | --- | --- |
| /bin | All | Core operating system commands^b |
| /boot | LS | Kernel and files needed to load the kernel |
| /dev | All | Device entries for disks, printers, pseudo-terminals, etc. |
| /etc | All | Critical startup and configuration files |
| /home | All | Default home directories for users |
| /kernel | S | Kernel components |
| /lib | All | Libraries, shared libraries, and parts of the C compiler |
| /media | LS | Mount points for filesystems on removable media |
| /mnt | LSA | Temporary mount points, mounts for removable media |
| /opt | LSA | Optional software packages (not consistently used) |
| /proc | LS | Information about all running processes |
| /root | | Home directory of the superuser (often /) |
| /sbin | All | Commands needed for minimum system operation |
| /stand | H | Stand-alone utilities, disk formatters, diagnostics, etc. |
| /tmp | All | Temporary files that may disappear between reboots |
| /usr | All | Hierarchy of secondary files and commands |
| /usr/bin | All | Most commands and executable files |
| /usr/include | All | Header files for compiling C programs |
| /usr/lib | | Libraries; also, support for standard programs |
| /usr/lib64 | L | 64-bit libraries on 64-bit Linux |
| /usr/local | All | Software you write or install; mirrors structure of **usr** |
| /usr/sbin | All | Less essential commands for administration and repair |
| /usr/share | All | Items that might be common to multiple systems |
| /usr/share/man | All | On-line manual pages |
| /usr/src | LSA | Source code for nonlocal software (not widely used) |
| /usr/tmp | All | More temporary space (preserved between reboots) |
| /var | All | System-specific data and configuration files |
| /var/adm | | Varies: setup records, strange administrative bits |
| /var/log | LSA | Various log files |
| /var/spool | All | Spooling directories for printers, mail, etc. |
| /var/tmp | All | More temporary space (preserved between reboots) |

a = Linux, S = Solaris, H = HP-UX, A = AI.
b. On HP-UX and AI, **/bin** is a symbolic link to **/usr/bin**.
c. The distinguishing characteristic of commands in **/sbin** is usually linked with "static" versions of the system libraries and therefore don't have many dependencies on other parts of the system.

## 6.4 FILE TYPES

Most filesystem implementations define seven types of files. Even when developers add something new and wonderful to the file tree (such as process information under **/proc**), it must be made to look like one of these seven types.

# Chapter 6

# The Filesystem

- Regular files
- Directories
- Character device files
- Block device files
- Local domain sockets
- Named pipes (FIFOs)
- Symbolic links

You can determine the type of an existing file with **ls -ld**. The first character of the ls output indicates the type. For example, the following command demonstrates that **/usr/include** is a directory:

```
$ -ld /usr/include
(d)rwxr-xr-x 27 root 4096 Jul 15 20:57 /usr/include
```

**ls** uses the codes shown in Table 6.3 to represent the various types of files.

## Table 6.3 File-type encoding by ls

| File type | Symbol | Removed by |
|---|---|---|
| Regular file | d | rm |
| Directory | r | rmdir, -r |
| Character device file | c | mknod | rm |
| Block device file | b | mknod | rm |
| Local domain socket | s | socket(2) | rm |
| Named pipe | p | mknod | rm |
| Symbolic link | l | ln -s | rm |

Table 6.3 shows, **rm** is the universal tool for deleting files. But how would you delete a file name, say, **rm -f**? It's a legitimate filename under most filesystems, but **rm -f** doesn't work because **rm** interprets the -f as a flag. The answer is to refer to the file by a longer pathname (such as **/-f**) or to use **rm --** argument to tell it that everything that follows is a filename and not an option (i.e., **rm -- f**).

Filenames that contain special characters present a similar problem since producing these names from the keyboard can be impossible. In this situation, you can use shell globbing (pattern matching) to identify the files. When you use pattern matching, it's a good idea to get in the habit of using the -i option to **rm** to confirm the deletion of each file. This feature protects you against accidentally deleting "good" files that your pattern inadvertently matches. For example, to delete a file named **foo<Control-D>bar**, you could use

```
$ ls
foo? foose kde-root
$ rm -i foo*
rm: remove 'foo\004bar?' y
rm: remove 'foose?' n
```

## Directories

Note that the filesystem is a directory, and directories are files too. The content of a directory file is a list of filenames and their corresponding inode numbers. You can see the contents of a directory using the **ls** command.

The type of a directory is indicated by a **d** in the **ls -ld** output. For example:

```
$ ls -ld /etc
drwxr-xr-x 25 root root 4096 Oct 12 14:20 /etc
```

Directories also contain special entries: `.` which refers to the directory itself, and `..` which refers to the parent directory. The root directory (/) has only the `.` entry.

## Regular files

Regular files are the most common type of file. They contain any data, whether text, binary, or executable code. There is no special meaning to the content of a regular file; it is simply a sequence of bytes.

## Character and block device files

Device files communicate with the hardware. When the kernel makes a request to a character or block device file, it simply passes the request to the appropriate driver. It is important to distinguish device files from device drivers, however. The files are just interfaces.

Character device files allow their associated drivers to do their own input buffering.. device files are used by drivers that handle I/O in chunks and wait the kernel to perform buffering. In fact, a few types of hardware were represented by both character and block device files, but that configuration is unusual today.

Device files are characterized by two numbers, the major and minor device numbers. The major device number tells the kernel which file to, and the minor device number typically tells the driver which physical unit to address. For example, major device number 4 on a Linux system identifies the serial driver. The first serial port (/dev/tty0) would have device number 4 and minor device number 0.

Drivers can interpret the minor device numbers that are passed to them in whatever they please. For example, tape drivers use the minor device number to determine whether the tape should be rewound when the device is closed.

In the distant past, /dev was a generic directory and the device files within it were created and removed with. A script called MAKED helped standardize the work of creating device files for common pieces of equipment.

Unfortunately, this crude system was ill-equipped to deal with the endless sea of drivers and device types that have appeared over the last few decades. It also facilitated all sorts of potential configuration mismatches: device files that referred to actual device, devices inaccessible because they had no device, and so on.

These days, most systems implement take a more active role in the configuration of its device files. In Solaris, for example, the /dev and /devices are fully virtualized. On Linux distributions, /dev is a standard directory, but the udev daemon manages the files within it.

![img/579ec8c67772f31a844bbb71a197_0.png]
