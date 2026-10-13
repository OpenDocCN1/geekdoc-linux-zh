depicted in Table 10.1. This table is a generalized example and does not necessarily apply to all possible implementations of a FHS-compliant system.

**TABLE 10.1. GENERALIZED EXAMPLE OF FHS-COMPLIANT DIRECTORY LAYOUT**

|  | Shared | Non-Shared |
|---|---|---|
| Static | `/usr`<br>`/opt` | `/etc`<br>`/boot` |
| Variable | `/var/mail`<br>`/var/spool/news` | `/var/run`<br>`/var/lock` |

# FHS Specifications for the Root Directory

As was outlined in the first section of this chapter, the root directory is the first and only directory at the top level of the tree hierarchy. As such, special considerations are warranted for the root directory. The FHS document states, “The contents of the root filesystem should be adequate to boot, restore, recover, and/or repair the system.” In order to accomplish that goal, the root filesystem must contain the essential components to boot the system, the essential tools to repair the system, and the essential utilities to back up or restore the system while still keeping the root filesystem as small as possible. A small root filesystem is less prone to filesystem errors and lends itself to easier maintenance if something goes wrong.

# Default Directory Layout

A typical installation of OpenLinux creates the root directory with the following files and directories:

```
```text
[root@redrock /]# ls -CF
NetWare/        bru/        initrd/          mnt/        sbin/
auto/           dev/        install@         opt/        tmp/
bin/            etc/        lib/             proc/       usr/
boot/           home/       lost+found/      root/       var/
```
```

Directories are denoted with a trailing forward slash, and symbolic links have a trailing @ symbol when files are listed with the F option. Following is a closer look at each of these directories.

> **Note**
> 
> You might not have all the directories listed and might even have one or two others. Directories are generally created by programs as they are needed, either during program installation or when a program runs for the first time.

# /NetWare

This directory is used as an automatic mount point for NetWare volumes as part of the NetWare client. The automatic mounting of NetWare volumes and NDS trees is discussed at length in Chapter 28, “Using NetWare.”