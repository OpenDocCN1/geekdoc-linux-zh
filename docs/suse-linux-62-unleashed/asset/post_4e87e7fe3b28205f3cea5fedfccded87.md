
# System Service Tools
CHAPTER 6

System Service Tools

naturally, this isn't convenient to use all the time. It is much better to have the system detect ethernet cards automatically or use yast to configure Linux for a particular card.

Just as insmod installs a module, rmmod removes one (if possible). The modprobe command loads a group of modules, or just the first one to work (as the first ethernet module to work), and depmod determines which other modules on which a given group of modules might depend.

Under SuSE Linux, settings for kernel modules are generally stored in the conf.modules file under the /etc directory. You will find several default settings for such hardware as your printer:

```
alias parport_lowlevel parport_pc
options parport_pc io=0x38 irq=none,none
```

The Alias keyword provides a pointer to a particular module and configuration listed in the conf.modules. In this case, the kernel is instructed to load the parallel-port driver using a starting address of 0x378 to load for any installed hardware. Kernel modules are installed under the /lib/modules/2.2.x directory, where X is the version of the kernel used by the system. For SuSE 6.2, this is the /lib/modules/2.2.10 directory. This directory contains additional directories containing modules for the system's CD-ROM, various filesystems, networking hardware, PC card devices, SCSI devices, video hardware, and miscellaneous devices, as pointers, infrared ports, sound cards, or tape drives.

> Note
For more information about configuring SuSE Linux for sound, see Chapter 30, "Games for SuSE Linux."

# The SuSE Help System

SuSE Linux, like all Linux distributions, includes many pages of documentation. While most Linux users know about the man or GNU info commands to read pages and info documents, new SuSE users may not know about the susehelp command. To start the command, enter the following:

```bash
# susehelp
```

The susehelp command will automatically launch Netscape Navigator if called during an X11 session. If susehelp is started from the console, the lynx text-only browser will be launched. To force the use of lynx even during an X session. To start the command, enter the following:

```bash
# susehelp -nox
```

The first help page displayed (the file index_e.html under the /usr/doc/susehelp directory) is your gateway to getting answers about Linux. The page contains an index listing:

- Package descriptions of software installed on your system
- Text search retrieval of information from program documentation and SuSE documentation
- Information from an on-line support database
- Information directly from SuSE if you have an active Internet connection
- Program documentation included with GNU software installed on your computer (such as info pages)
- Helpful information and step-by-step guides in HOWTO documents
- Information about the X Window System
- Specific documentation provided with selected programs (under the /usr/doc/packages directory)

To get information, click a link on the displayed page. You can then use Navigator or lynx to go back and forth through your system's documents.

# The SuSE Linux File System

The SuSE Linux file system, or directory structure and organization of the files on a typical system, follows most Linux distributions with a few exceptions. This section will examine the file system (as opposed to a filesystem, as ext2) and then highlight the major components of a SuSE Linux hierarchy of directories.

Whereas other proprietary and legacy operating systems, such as Microsoft Windows, use lettered volume names (A:, C; and so on), Linux uses a primary or boot partition mounted at the root of the tree /. Other partitions can be grafted onto the tree at mount points. While new Linux users can create a single Linux partition (besides swap) for the entire file system, it has become customary for certain basic directories, such as /home, to be placed in separate filesystems (partitions) if possible. The reasons for this vary. Perhaps the most compelling are:

- Disk capacity— Disks are extremely limited in storage capacity. Using a single disk for multiple purposes may consume too much space.
- Performance— The root directory has to be searched every time any pathname in UNIX/Linux is opened. If the root directory is cluttered, this will impede performance of the entire system.
- Backup— It’s better to concentrate important and frequently changing data (such as the users of home directories) into a single place so this relatively small amount of data can be backed up more often than massive but seldom changing data.
- User convenience— It’s easier to find things if there are clear guidelines on where to look.

From the point of view of navigating the Linux file hierarchy, it is irrelevant (for the most part) whether a directory is, in fact, a mount point (so that it is on a different partition than its parent directory), an ordinary subdirectory, or a symbolic link.

However, a worthwhile holdover from the days of small disks has fostered well-established customs about the local organization of UNIX-like filesystems. In the fact, the accumulated wisdom of assorted UNIX and Linux administrators over the years has been distilled into something called the Filesystem Hierarchy Standard (FHS), which can be found at http://www.pathname.com/fhs.

One of the FHS is continuity with the past, even when slightly counterintuitive. For instance, as you might have guessed from its name, the /usr top-level directory was used early, among other things, for user home directories on early UNIX systems. Now, however, /usr contains mostly system files, and user home directories are found in /home, except for the root user, whose home directory must be in root partition.

# Organization of the SuSE File System

The root directory (/) is nicely organized and fully featured in comparison with other distributions. This is because / is very clean and only holds the most essential items—only directories. The command ls -p for a freshly installed SuSE system looks like the following:

| | | | |
| :--- | :--- | :--- | :--- |
| cdrom/ | home/ | opt/ | shlib/ |
| ../ | dev/ | lib/ | proc/ |
| etc/ | lost+found/ | root/ | tmp/ |
| boot/ | floppy/ | sbin/ | var/ |

The directory lost+found contains files salvaged by the fsck utility until an impropermount or system failure. A directory of this name should be present at the root of every modifiable filesystem (except NFS and Samba partitions) directories /boot, /dev, and /proc have special roles, which are explained in Chapter 18, “Managing Filesystems”.

In the early stages of the boot sequence, only the root filesystem is available, and therefore nothing outside the root partition should be necessary to start a session for the root user. This sometimes influences the choice of where to put files.

# Essentials of /bin and /sbin

Most of the essential programs for using and maintaining Linux are stored in the /bin and /sbin directories. The bin in the names of these directories comes from the fact that executable programs are binary files.

The /bin directory holds the most commonly used essential user programs, such as the following:

- login
- Shells (bash, tcsh)
- File manipulation utilities (cp, mv, rm, ln, tar)
- Filesystem utilities (dd, df, mount, sync)
- System utilities (uname, hostname, arch)

In addition to these types of programs, the /bin directory also contains other GNU utilities such as gzip and gunzip.

The /sbin directory holds essential maintenance or system programs, such as the following:

- fsck
- fdisk
- mkfs
- shutdown
- bilo
- init

The main difference between the programs stored in /bin and /sbin is that nearly all of the programs in /sbin are executable only by root (one exception is the ifconfig command). By default, the /sbin and /usr/sbin directories are not included in normal users’ PATH.
