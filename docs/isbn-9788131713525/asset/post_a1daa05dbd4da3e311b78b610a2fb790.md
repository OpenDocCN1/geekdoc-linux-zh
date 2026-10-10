
In Chapter 2, “Your First Embedded Experience,” we pointed out that the Linux kernel itself is but a small part of any embedded Linux system. After the kernel has initialized itself, it must mount a root file system and execute a set of developer-defined initialization routines. In this chapter, we examine the details of post-kernel system initialization.

We begin by looking at the root file system and its layout. Next we develop and study a minimal system configuration. Later in this chapter, we add functionality to the minimal system configuration to produce useful example embedded system configurations. We complete the coverage of system initialization by introducing the initial ramdisk, or initrd, and its operation and use. The chapter concludes with a brief look at Linux shutdown logic.

## 6.1 Root File System

In Chapter 5, “Kernel Initialization,” we examined the Linux kernel’s behavior during the initialization process. We made several references to mounting a root file system. Linux, like many other advanced operating systems, requires a root file system to realize the benefits of its services. Although it is certainly possible to use Linux in an environment without a file system, it makes little sense because most of the features and value of Linux would be lost. It would be similar to putting your entire system application into an overloaded device driver or kernel thread.

The root file system refers to the file system mounted at the base of the file system hierarchy, designated simply as `/`. As you will discover in Chapter 9, “File Systems,” even a small embedded Linux system typically mounts several file systems on different locations in the file system hierarchy. The proc file system, introduced in Chapter 9, is an example. It is a special-purpose file system mounted at `/proc` under the root file system. The root file system is simply the first file system mounted at the base of the file system hierarchy.

As you will shortly see, the root file system has special requirements for a Linux system. Linux expects the root file system to contain programs and utilities to boot a system, initialize services such as networking and a system console, load device drivers, and mount additional file systems.

### 6.1.1 FHS: File System Hierarchy Standard

Several kernel developers authored a standard governing the organization and layout of a UNIX file system. The File System Hierarchy Standard (FHS) establishes a minimum baseline of compatibility between Linux distributions and application programs. You'll find a reference to this standard in Section 6.7.1 “Suggestions for Additional Reading” at the end of this chapter. You are encouraged to review the FHS standard for a better background on the layout and rationale of UNIX file system organization.

Many Linux distributions have directory layouts closely matching that described in the FHS standard. The standard exists to provide one element of a common base between different UNIX and Linux distributions. The FHS standard allows your application software (and developers) to predict where certain system elements, including files and directories, can be found on the file system.

### 6.1.2 File System Layout

Where space is a concern, many embedded systems developers create a very small root file system on a bootable device (such as flash memory) and later mount a larger file system from another device, perhaps a hard disk or network NFS server. In fact, it is not uncommon to mount a larger root file system right on top of the original small one. You'll see an example of that when we examine the *initial ramdisk* (*initrd*) later in this chapter.

A simple Linux root file system might contain the following top-level directory entries:

- bin
- dev
- etc
- lib
- sbin
- usr
- var
- tmp

Table 6-1 details the most common contents of each of these root directory entries.

**Table 6-1**  
Top-Level Directory Directories

| Directory | Contents |
|-----------|----------|
| bin       | Binary executables, usable by all users on the system¹ |
| dev       | Device nodes (see Chapter 8, “Device Driver Basics”) |
| etc       | Local system-configuration files |
| lib       | System libraries, such as the standard C library and many others |
| sbin      | Binary executables usually reserved for superuser accounts on the system |
| usr       | A secondary file system hierarchy for application programs, usually read-only |
| var       | Contains variable files, such as system logs and temporary configuration files |
| tmp       | Temporary files |

The very top of the Linux file system hierarchy is referenced by the forward slash character (/) by itself. For example, to list the contents of the root directory, one would type this:

```
$ ls /
```

This produces a listing similar to the following:

```
root@coyote:# ls /
bin dev etc home lib mnt opt proc root sbin tmp usr var
root@coyote:#
```

This directory listing contains directory entries for additional functionality, including /mnt and /proc. Notice that we reference these directory entries preceded by the forward slash, indicating that the path to these top-level directories starts from the root directory.

### 6.1.3 Minimal File System

To illustrate the requirements of the root file system, we have created a minimal root file system. This example was produced on the ADI Engineering Coyote Reference board using an XScale processor. Listing 6-1 is the output from the tree command on this minimal root file system.

**Listing 6-1**  
Contents of Minimal Root File System

```
|-- bin
|   |-- busybox
|   |-- sh -> busybox
|   ...
|-- dev
|   |-- console
|-- etc
|   |-- init.d
|       |-- rcS
|-- lib
|   |-- ld-2.3.2.so
|   |-- ld-linux.so.2 -> ld-2.3.2.so
|   |-- libbc-2.3.2.so
|   |-- libc.so.6 -> libc-2.3.2.so
```

This root configuration makes use of busybox, a popular and aptly named toolkit for embedded systems. In short, busybox is a stand-alone binary that provides support for many common Linux command line utilities. busybox is so pertinent for embedded systems that we devote Chapter 11, “BusyBox,” to this flexible utility.

Notice in our example minimum file system in Listing 6-1 that there are only eight files in five directories. This tiny root file system boots and provides the user with a fully functional command prompt on the serial console. Any commands that have been enabled in busybox² are available to the user.

Starting from /bin, we have the busybox executable and a soft link called sh pointing back to busybox. You will see shortly why this is necessary. The file in /dev is a device node³ required to open a console device for input and output. Although it is not strictly necessary, the rcS file in the /etc/init.d directory is the default initialization script processed by busybox on startup. Including rcS silences the warning message issued by busybox if rcS is missing.

> ² BusyBox commands are covered in Chapter 11.  
> ³ Device nodes are explained in detail in Chapter 8.

The final directory entry and set of files required are the two libraries, GLIBC (libc-2.3.2.so) and the Linux dynamic loader (ld-2.3.2.so). GLIBC contains the standard C library functions, such as printf() and many others that most application programs depend on. The Linux dynamic loader is responsible for loading the binary executable into memory and performing the dynamic linking required by the application’s reference to shared library functions. Two additional soft links are included, ld-linux.so.2 pointing back to ld-2.3.2.so and libc.so.6 referencing libc-2.3.2.so. These links provide version immunity and backward compatibility for the libraries themselves, and are found on all Linux systems.

This simple root file system produces a fully functional system. On the ARM/XScale board on which this was tested, the size of this small root file system was about 1.7MB. It is interesting to note that more than 80 percent of that size is contained within the C library itself. If you need to reduce its size for your embedded system, you might want to investigate the Library Optimizer Tool at http://libraryopt.sourceforge.net/.

### 6.1.4 The Root FS Challenge

The challenge of a root file system for an embedded device is simple to explain. It is not so simple to overcome. Unless you are lucky enough to be developing an embedded system with a reasonably large hard drive or large Flash storage on board, you might find it difficult to fit your applications and utilities onto a single Flash memory device. Although costs continue to come down for Flash storage, there will always be competitive pressure to reduce costs and speed time to market. One of the single largest reasons Linux continues to grow in popularity as an embedded OS is the huge and growing body of Linux application software.

Trimming a root file system to fit into a given storage space requirement can be daunting. Many packages and subsystems consist of dozens or even hundreds of files. In addition to the application itself, many packages include configuration files, libraries, configuration utilities, icons, documentation files, locale files related to internationalization, database files, and more. The Apache web server from the Apache Software Foundation is an example of a popular application often found in embedded systems. The base Apache package from one popular embedded Linux distribution contains 254 different files. Furthermore, they aren’t all simply copied
