
Even with this explanation, it is inconceivable to many that you can pull Windows or DOS off a system and use Linux as the operating system. To avoid this kind of confusion, let's discuss the generic role of an operating system.

All operating systems, whether they be DOS, Windows, Mac OS, Unix, NetWare, or Linux, provide four key functions in the computer system:

- **Application platform**—Applications generally don't access the system hardware directly. Operating systems provide a platform where applications can be run. Operating systems manage and prioritize application access to the system.

- **File storage**—Operating systems provide a means for writing, organizing, and retrieving data from system storage devices.

- **Security**—Most modern operating systems are multiuser systems. They use rules configured by the system administrator to identify who the authorized users of the system are and what they can do within the system.

- **Hardware moderator**—A key role of an operating system is providing applications with easy access to system resources. It provides a means for applications to address a system, place information in RAM, read and write information to the hard disk drive, and communicate with peripherals such as printers, COM ports, or network boards. Instead of having to write code from scratch to do these tasks, most operating systems contain prewritten, reusable routines that the application programmer can use to interact with system hardware. It also provides methods for managing system input and output devices such as the keyboard.

The difference between operating systems is how they are designed and how they fill these roles. As you might guess, some fill these roles better than others.

## Introduction to the Linux User Interface

For an operating system to be useful, it must provide an interface that allows the end user to easily communicate with it. Linux provides two user interfaces:

- **The command-line interface**—The basic Linux interface is the command-line interface. The user communicates with the operating system by entering commands at a shell prompt. A common Linux shell prompt is shown in Figure 2.1.

![](img/c7771e8540507f2b00c088c7a411b57b_38_0.png)

**FIGURE 2.1**

A Linux command-line interface.

- **The X Window System graphical interface**—In a world dominated by graphical user interfaces, a command-line only operating system may face some resistance. There are many computer users in the world today, both end users and system administrators, who have never had to use a command-line interface. To make it easier to use, the XFree86 project developed an X Window system that runs on Linux. Using the base XFree86 system along with a window manager (such as GNOME or KDE), users can interact with the Linux kernel in a graphical environment. The GNOME graphical interface on SUSE Linux is shown in Figure 2.2.

![](img/c7771e8540507f2b00c088c7a411b57b_38_1.png)

**FIGURE 2.2**

A Linux graphical interface.

## An Introduction to the Linux File System

As mentioned earlier in this chapter, one of the key roles filled by an operating system is managing a storage system that allows files to be written and retrieved from storage devices such as floppy disk drives and hard drives.

Linux uses a hierarchical file system much like other operating systems you might be familiar with. Consider the Windows file system shown in Figure 2.3.

![](img/c7771e8540507f2b00c088c7a411b57b_39_0.png)

**FIGURE 2.3**

The Windows file system.

At the top of the Windows file system is the root directory. In this example it is `C:\`.

> **REAL WORLD**
>
> Technically, C: identifies the drive letter assigned to the NTFS partition. The \ indicates the root directory of the file system on that partition.

Files or other directories can exist within the root directory. Sometimes these are called subdirectories. Subdirectories can contain other subdirectories or files. In this example, there is a file named `MyStuff.txt`. It is located in the `MyStuff` directory. `MyStuff` is a subdirectory of the `Temp` directory; which, itself, is a subdirectory of the root directory `\`.

To describe the location of the `MyStuff.txt` file, you prepend the path to the file to its name. In this example, you would use `C:\Temp\MyStuff\MyStuff.txt`.

Linux works in a very similar manner. However, there are some differences you should be aware of. Consider Figure 2.4 as an example.

![](img/c7771e8540507f2b00c088c7a411b57b_40_0.png)

**FIGURE 2.4**

The Linux file system.

Just as with the Windows file system, there is a root directory. Instead of being referenced as `\`, the Linux root directory is referenced as `/`. The root directory contains subdirectories and files. In this example, there is a file named *MyStuff.txt* located in the *MyStuff* directory. This directory is a sub-directory of the *Temp* directory—which is itself a subdirectory of the root directory `/`.

Notice that the only apparent differences, so far, are the absence of a drive letter and the direction of the slash. Windows (and DOS, for that matter) use the back slash character (`\`) in the directory structure. Linux, on the other hand, uses the forward slash (`/`).

There, however, more significant differences between the Windows file system and the Linux file system. Let's investigate, in the sections that follow, some of the most critical aspects of the Linux file system you need to understand to succeed in this course.

### Case Sensitivity

Recall our Windows example: You can reference the file specified as `C:\Temp\MyStuff\MyStuff.txt` by `C:\TEMP\MYSTUFF\MYSTUFF.TXT`, `C:\TEMP\MYSTUFF\MyStuff.txt`, `C:\Temp\MyStuff\MYSTUFF.TXT`, or any other combination of upper- and lower-case characters. File and directory names under Windows (or DOS) are not case sensitive.

Under Linux, however, file and directory names are very case sensitive. In the example presented here, the correct path and file name is `/Temp/MyStuff/MyStuff.txt`. If you try to reference this file as `/TEMP/MYSTUFF/MYSTUFF.TXT` or as `/temp/mystuff/mystuff.txt`, it will fail. According to the standards used to define the Linux file system, these two names point to completely different files and directories.

### Mount Points

The Windows file system uses a drive letter—in the example given, the drive letter is C. Drive letters are used by NTFS and FAT file systems to uniquely identify a partition on the hard drive. There could be multiple partitions on the drive (each with its own drive letter assigned), or there could be one partition that encompasses the entire drive. Each drive letter has its own hierarchical structure underneath it.

Linux, on the other hand, doesn't use drive letters. Like Windows, the Linux file system can use multiple partitions, but instead of assigning a new drive letter to each partition, the Linux file system incorporates each partition within the same hierarchical structure using mount points.

A mount point is simply a directory in the file system that points to a different Linux partition. This partition could be on the same hard drive in the same system, a partition on a different hard drive in the same system, or even a remote file system on a hard drive in a different PC.

> **NOTE**
>
> To mount remote file systems, you must use the Network File System (NFS) service.

When you change to the directory where the mount point is set, the Linux file system takes you to the different partition or file system.

For example, suppose you use your Linux system to edit video footage. The raw files you work on take tremendous amounts of space and you need to add a new 200GB hard drive to your system.

To do this, you would first partition and format the drive. Then you can create a directory in the existing file system where you want to mount the new partition—say, in `/home/rtracy/rawfootage`. You can then use the `mount` command to mount the new hard disk in the file system.

> **REAL WORLD**
>
> To automatically mount the partition every time the system boots, you can place an entry in the `/etc/fstab` file—a file system table. We'll cover the `fstab` file later in the book.

To save a file on the new hard drive, you simply save it to `/home/rtracy/rawfootage` and it will be automatically redirected to the new disk.
