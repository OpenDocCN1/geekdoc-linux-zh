
resent disk drives (for instance, /dev/sda), partitions (/dev/sda1), mice (/dev/input/mouse0), keyboards (/dev/input/event0), sound cards (/dev/snd/*), serial ports (/dev/ttyS*), and other components.

There are two types of device files: block and character. The former has characteristics of a block of data: It has a finite size, and you can access bytes at any position in the block. The latter behaves like a flow of characters. You can read and write characters, but you cannot seek to a given position and change arbitrary bytes. To find out the type of a given device file, inspect the first letter in the output of `ls -l`. It is either `b`, for block devices, or `c`, for character devices:

```
$ ls -l /dev/sda /dev/ttyS0  
  brw-rw--- 1 root disk     8,   0 Mar 21 08:44 /dev/sda  
  crw-rw--- 1 root dialout 4,  64 Mar 30 08:59 /dev/ttyS0
```

As you might expect, disk drives and partitions use block devices, whereas mouse, keyboard, and serial ports use character devices. In both cases, the programming interface includes device-specific commands that can be invoked through the `ioctl` system call.

### 3.1.2. Unifying File Systems

File systems are a prominent aspect of the kernel. Unix-like systems merge all the file stores into a single hierarchy, which allows users and applications to access data by knowing its location within that hierarchy.

The starting point of this hierarchical tree is called the root, represented by the "/" character. This directory can contain named subdirectories. For instance, the home subdirectory of / is called /home/. This subdirectory can, in turn, contain other subdirectories, and so on. Each directory can also contain files, where the data will be stored. Thus, /home/buxy/Desktop/hello.txt refers to a file named hello.txt stored in the Desktop subdirectory of the buxy subdirectory of the home directory, present in the root. The kernel translates between this naming system and the storage location on a disk.

Unlike other systems, Linux possesses only one such hierarchy, and it can integrate data from several disks. One of these disks becomes the root, and the others are mounted on directories in the hierarchy (the Linux command is called mount). These other disks are then available under the mount points. This allows storing users’ home directories (traditionally stored within /home/) on a separate hard disk, which will contain the buxy directory (along with home directories of other users). Once you mount the disk on /home/, these directories become accessible at their usual locations, and paths such as /home/buxy/Desktop/hello.txt keep working.

There are many file system formats, corresponding to many ways of physically storing data on disks. The most widely known are ext2, ext3, and ext4, but others exist. For instance, VFAT is the file system that was historically used by DOS and Windows operating systems. Linux’s support for VFAT allows hard disks to be accessible under Kali as well as under Windows. In any case, you must prepare a file system on a disk before you can mount it and this operation is known as formatting.

Commands such as mkfs.ext3 (where mkfs stands for Make FileSystem) handle formatting. These commands require, as a parameter, a device file representing the partition to be formatted (for instance, /dev/sda1, the first partition on the first drive). This operation is destructive and should be run only once, unless you want to wipe a filesystem and start fresh.

There are also network filesystems such as NFS, which do not store data on a local disk. Instead, data are transmitted through the network to a server that stores and retrieves them on demand. Thanks to the file system abstraction, you don't have to worry about how this disk is connected, since the files remain accessible in their usual hierarchical way.

### 3.1.3. Managing Processes

A process is a running instance of a program, which requires memory to store both the program itself and its operating data. The kernel is in charge of creating and tracking processes. When a program runs, the kernel first sets aside some memory, loads the executable code from the file system into it, and then starts the code running. It keeps information about this process, the most visible of which is an identification number known as the *process identifier* (PID).

Like most modern operating systems, those with Unix-like kernels, including Linux, are capable of multi-tasking. In other words, they allow the system to run many processes at the same time. There is actually only one running process at any one time, but the kernel divides CPU time into small slices and runs each process in turn. Since these time slices are very short (in the millisecond range), they create the appearance of processes running in parallel, although they are active only during their time interval and idle the rest of the time. The kernel's job is to adjust its scheduling mechanisms to keep that appearance, while maximizing global system performance. If the time slices are too long, the application may not appear as responsive as desired. Too short, and the system loses time by switching tasks too frequently. These decisions can be refined with process priorities, where high-priority processes will run for longer periods and with more frequent time slices than low-priority processes.

**Multi-Processor Systems (and Variants)** The limitation described above, of *only one process running at a time*, doesn't always apply: the actual restriction is that there can be *only one running process per processor core*. Multi-processor, multi-core, or *hyper-threaded* systems allow several processes to run in parallel. The same time-slicing system is used, though, to handle cases where there are more active processes than available processor cores. This is not unusual: a basic system, even a mostly idle one, almost always has tens of running processes.

The kernel allows several independent instances of the same program to run, but each is allowed to access only its own time slices and memory. Their data thus remain independent.

### 3.1.4. Rights Management

Unix-like systems support multiple users and groups and allow control of permissions. Most of the time, a process is identified by the user who started it. That process is only permitted to take actions permitted for its owner. For instance, opening a file requires the kernel to check the process identity against access permissions (for more details on this particular example, see section 3.4.4, “Managing Rights” [page 57]).

## 3.2. The Command Line

By “command line”, we mean a text-based interface that allows you to enter commands, execute them, and view the results. You can run a terminal (a textual screen within the graphical desktop, or the text console itself outside of any graphical interface) and a command interpreter inside it (the shell).

### 3.2.1. How To Get a Command Line

When your system is working properly, the easiest way to access the command line is to run a terminal in your graphical desktop session.

![](img/46e3313ea1bb2892f314630a4f0677b8_77_0.png)

Figure 3.1 Starting GNOME Terminal

For instance, on a default Kali Linux system, GNOME Terminal can be started from the list of favorite applications. You can also type "terminal" while in the Activities screen (the one that gets activated when you move the mouse to the top-left corner) and click on the correct application icon that appears (Figure 3.1, "Starting GNOME Terminal" [page 51]).

In the event that your graphical interface is broken, you can still get a command line on virtual consoles (up to six of them can be accessible through the six key combinations of CTRL+ALT+F1 through CTRL+ALT+F6 — the CTRL key can be omitted if you are already in text mode, outside of Xorg or Wayland's graphical interface). You get a very basic login screen where you enter your login and password before being granted access to the command line with its shell:

```text
Kali GNU/Linux Rolling kali-rolling tty3
kali-rolling login: root
Password:
Last login: Fri Mar 25 12:30:05 EDT 2016 from 192.168.122.1 on pts/2
Linux kali-rolling 4.4.0-kali1-amd4 #1 SMP Debian 4.4.6-1kali1 (2016-03-18) x86_64
The programs included with the Kali GNU/Linux system are free software;
the exact distribution terms for each program are described in the
individual files in /usr/share/doc/*/copyright.

Kali GNU/Linux comes with ABSOLUTELY NO WARRANTY, to the extent
permitted by applicable law.
root@kali-rolling:~#
```

The program handling your input and executing your commands is called a shell (or a command-line interpreter). The default shell provided in Kali Linux is *Bash* (it stands for *Bourne Again Shell*). The trailing `$` or `#` character indicates that the shell is awaiting your input. It also indicates whether Bash recognizes you as a normal user (the former case with the dollar) or as a super user (the latter case with the hash).

### 3.2.2. Command Line Basics: Browsing the Directory Tree and Managing Files

This section only provides a brief overview of the covered commands, all of which have many options not described here, so please refer to the abundant documentation available in their respective manual pages. In penetration tests, you will most often receive shell access to a system after a successful exploit, rather than a graphical user interface. Proficiency with the command line is essential for your success as a security professional.

Once a session is open, the `pwd` command (which stands for *print working directory*) displays your current location in the filesystem. The current directory is changed with the `cd directory` command (`cd` is for *change directory*). When you don't specify the target directory, you are taken to your home directory. When you use `cd -`, you go back to the former working directory (the one in use before the last `cd` call). The parent directory is always called `..` (two dots), whereas the
