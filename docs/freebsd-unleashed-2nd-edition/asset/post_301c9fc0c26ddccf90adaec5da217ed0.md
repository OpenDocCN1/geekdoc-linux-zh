
## CHAPTER 8

## The FreeBSD Filesystem

To understand how FreeBSD operates, it is essential to have a clear idea of how the system manages files as well as the critical differences between FreeBSD’s method and those of other operating systems.

FreeBSD uses the BSD Fast Filesystem (FFS). It is a common misconception that modern BSD Unixes use UFS (Universal or Unix Filesystem, depending on who you ask). In fact, many of the tools discussed in this chapter (such as mount) refer to UFS as the default filesystem type. This isn’t the case. FFS is colloquially called UFS by many, and you can do the same—as long as you remember that the “true” UFS was used only in very early BSD-style Unixes and has been replaced by FFS in FreeBSD.

FFS is the filesystem type commonly used in FreeBSD, OpenBSD, NetBSD, and others, including Mac OS X (whose foundation, called Darwin, is based on FreeBSD and the core BSD distribution). Linux typically uses Ext2FS, Windows NT uses NTFS, and Windows 95/98/Me use VFAT. This information will be useful to know later in this chapter when we discuss mounting filesystems from other operating systems.

> **NOTE**
> A fuller reference and discussion of the filesystem types used in the computing world can be found at `http://www.penguin.cz/~mh1/fs/`.

### The FreeBSD Directory Structure

If you have used any Unix or Unix-like operating system, FreeBSD’s directory structure will undoubtedly look familiar to you (see Figure 8.1).

**IN THIS CHAPTER**

- The FreeBSD Directory Structure
- Monitoring Filesystem Usage
- Mounting and Unmounting FreeBSD Filesystems
- Mounting and Unmounting Filesystems from Other Operating Systems
- Mounting and Unmounting CD-ROM and Floppy-Based Filesystems
- Understanding the /etc/fstab File
- Checking and Repairing Filesystems with fsck
- Setting and Enforcing User Filesystem Quotas

![](img/48eec858cce7dfb89da36a4d40b7daf3_197_0.png)

**FIGURE 8.1** The FreeBSD filesystem, showing part of the hierarchical structure beginning at the root directory (/).

However, there are some key differences between the FreeBSD filesystem and the ones used by Linux, Solaris, and other Unices. For users coming from a Windows or Macintosh background, the directory structure can be extremely cryptic. As with much in the Unix realm, the original reasons for such things as the quirky traditional naming scheme have been lost in the mists of time, but this chapter tries to shed a little light on the FreeBSD filesystem—enough, at least, to help you become familiar with its quirks so you can comfortably use the system.

Table 8.1 lists the key elements of the FreeBSD filesystem. If you issue a `ls /` command, you will see the top-level view of the FreeBSD filesystem, including the listed items and probably a few more which may vary depending on your specific installation. Directories are indicated with a following slash (/), symbolic links with an at (@) sign, and executables with an asterisk (*).

**TABLE 8.1** Key Elements of the FreeBSD Filesystem

| Directory | Purpose |
| :--- | :--- |
| **bin/** | Statically linked binaries are contained here. These can be used even when you're doing an emergency boot and don't have access to any dynamically linked programs or any filesystems other than /. |
| **boot/** | This directory contains the kernel, which is the master executable of the system. The kernel manages all the devices and handles networking, along with a host of other tasks. See Chapter 16, “Kernel Configuration,” for more information. /boot also has configuration files and executables that are used during boot. |
| **compat&** | This is a symlink to directory structures which provide compatibility with other operating systems, such as Linux. |
| **dev/** | This is a special directory. Files in here are mostly devices, which are special file types that give programs an interface into any devices the kernel supports. |
| **etc/** | Long ago, this was merely a directory for random files that didn't fit elsewhere. It is now where most systemwide configuration files go, including your user (password) databases and startup scripts. |
| **home&** | This is possibly a plain directory or a symbolic link to `/usr/home`, depending on your installation. All regular users' home directories are contained here. |
| **mnt/** | An empty directory that's provided for your convenience as a mount point if you need to mount another disk. |
| **modules/** | Loadable kernel modules are stored here. |
| **proc/** | Contains the process filesystem (procfs) and is an interface to the process table. It's used for convenience by some programs but is not essential to the operation of the system (it can safely be unmounted). |
| **root/** | The root user's home directory. It's not in `/home` for security reasons so that it will be available during an emergency boot. |
| **sbin/** | Contains system binaries that are statically linked. These programs differ from the ones in `/bin` in that they generally alter the system's behavior, whereas the `/bin` programs are simply user tools. |
| **stand/** | Contains a set of hard-linked programs that provide a "mini-FreeBSD" environment during system installation and emergencies when running in standalone mode. The only program you will likely be interested in is `sysinstall`, which was covered in Chapter 2, "Installing FreeBSD." |
| **sys&** | A link to the kernel sources (if you installed them). |
| **tmp/** | Contains temporary files. Any user can write files into this directory. |
| **usr/** | The gateway to the rest of the system, including dynamically linked programs, user files, and programs you installed yourself. In upcoming chapters, you'll spend most of your time here. |
| **var/** | Contains variable files. These include runtime files used by programs, log files, spool directories, and other items that change with the normal operation of the system. |

There are some important differences between the FreeBSD directory structure and that of similar operating systems, such as Linux. FreeBSD's structure is tightly controlled, and the clearest rule is that "anything installed by the administrator goes into /usr/local." Although other systems might allow user-installed programs the freedom to install files wherever they want, FreeBSD maintains strict structural guidelines in its ported programs and packages (see "Introduction to Packages," in Chapter 14, "Installing Additional Software"). Although a program might, by default, put its libraries in /var/lib and its configuration files into /etc, FreeBSD patches (modifies) the installation scripts so that the files would go into `/usr/local/lib` and `/usr/local/etc`, respectively. In fact, all configuration files for any software you might install will go into `/usr/local/etc`. If the program installs a startup script to be launched on boot, the script is placed in `/usr/local/etc/rc.d`. Anything in that directory is run at boot time, after the scripts in the analogous `/etc/rc.d` (the base system's startup scripts) are run.

The advantage of a structure this carefully controlled is that a FreeBSD system is relatively easy to maintain, and it's especially easy to re-create on a new machine (if you're upgrading to new hardware, for instance). Theoretically, you could copy the `/usr/local` directory tree from one machine to another, and everything would work the same on both machines. This is a risky proposition, however, and any such operation is likely to hit any number of unforeseen snags. Still, this kind of system portability is an ideal toward which FreeBSD strives.

An obvious disadvantage of the FFS controlled structure, though, is that if you're trying to port a program from Linux or Solaris to FreeBSD, you might experience some pain in fixing the expected paths. For instance, if you have programs written in Python on Linux, in which the Python interpreter is installed as `/usr/bin/python`, the programs will not run on FreeBSD because Python is not part of the base installation and are therefore installed as `/usr/local/bin/python`. You can easily fix this problem for one or two files, but migrating an installation with hundreds of such programs can quickly become painful. In the interest of cross-platform compatibility, it may turn out to be simplest to violate FreeBSD's structural guidelines by making the symbolic link `/usr/bin/python` to point to `/usr/local/bin/python`.

You can find a more detailed description of FreeBSD's filesystem by entering `man hier`.

### Monitoring Filesystem Usage

The idea of mount points is an aspect of Unix-style operating systems that is quite foreign to Windows users. In Windows/DOS, each disk in your system is assigned a drive letter (such as C:), and each drive has its own independent filesystem. For example, a machine with two hard drives and a CD-ROM drive might have C:, D:, and E: drives that the user can switch between. In Unix, there is only one systemwide directory structure, and all disks in the system are mounted at different points in the structure. An appropriate analogy would be that a Windows system resembles an orchard, with a row of similar trees, whereas a Unix system is more like a single large tree, with smaller trees grafted onto its trunk and branches. All the grafted elements on the Unix "tree" form a single hierarchical structure (see Figure 8.2).
