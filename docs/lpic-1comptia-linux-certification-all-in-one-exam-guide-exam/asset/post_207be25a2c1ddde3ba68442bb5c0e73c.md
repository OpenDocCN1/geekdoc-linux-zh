
/opt This directory contains files for some programs you install on the system.

/proc This directory is a little different from the other directories in this list. /proc doesn't actually exist in the file system. Instead, it's a pseudo-file system that is dynamically created whenever it is accessed. It's used to access processes and other system information from the Linux kernel.

Within /proc there is a number of different subdirectories, as shown in Figure 4-4. Notice that each of these subdirectories is identified with a number, not with a name. These numbers correspond to the process ID (PID) number of the associated process running on the system. In Figure 4-5, the top program is being run to display the running processes on the system.

Figure 4-4 Subdirectories of /proc

```
fs2:/proc # ls
1   1087 2728   35  775  9166  925-7  ipcstats  schedstat
4   12068 2840   36  777  9194  6c4b0   irq     scsi
10040 18888 24   39  797  8898    keymaps  self
10056 10861 2521 39  7971 9204  9270   kcore slabinfo
10150 1999 2621 4  79  9485  9289    kpid softirqs
10159 19   27   419 8   8888  9323   kpg_user sgi
10170 1074 2754 4256 38  9230  xtpi  kmsg stat
10179 1937 2795 4487 9540 49/15 asound  keystep swaps
10140 1954 2756 4583 9880 59/9  buddyinfo kpageflags sys
1.  .  2752 5  8888 9888   bus latency_stats sysrq_trigger
2/ 280   2758 584 4   9686 cmdline  loadavg ttyss
1/443 2016 2759 6   9825  9283 config.gz  locks timer_list
1/445 7932 21  680 9549  9/3/7 crypto  modules timer_stats
1/+ 2867 273 988  8243 cryptof  mpt mpt
1/511 2874 297 6876 9686 9246 devices  msr uptime
10058 21  888 635 9888 925/2 devices  mtd version
/4   2427 284 3   9136 9451 dma mounts vmallocinfo
1/0 22   3  70  9145 9253 driver  mpt wstat
1/411 2640 38  71.15 9149 9254 execdomains mtr x86
15  2347 885  73  9118 9426 interrupt8 8s
1/6   2852 81  72  9168 9254 fsystems  pagetypeinfo
/7/05 3258 32  726 9162 9888 1s partitions
810  7493 33  73  9198 9436 interrupts reserve_info
1/98/ 29  84  74  9172 9265 iomen  sched_debug
fs2:/proc #
```

The PID column, on the far-left side of the display, lists the PID number of each process. The actual name of the command used to create the process is displayed in the far-right column of the display. For example, the process associated with the top program itself has a PID of 10178. Therefore, if you were to look in /proc/10178 directory, you could view information about the top process running on the system, as shown in Figure 4-6.

/root This directory is the root user's home directory. Notice that it is located separately from the home directories for other users in /home.

/sbin This directory contains important system management and administration files, such as fdisk, fsck, ifconfig, init, mkfs, shutdown, and halt.

/srv This directory contains subdirectories where services running on the system (such as http and ftpd) save their files.

/sys This directory contains information about the hardware in your system.

/tmp This directory contains temporary files created by you or by the system.

> TIP The system will periodically delete old files out of the /tmp directory. Don't save anything in /tmp that you want to keep!

![](img/fb5404b3ce1e1e1d707f5abc39814a4a_141_1.png)

/usr This directory contains application files. In fact, most of these application files used on your system are saved in a subdirectory of /usr. These subdirectories include those shown in Table 4-3.

Table 4-3 Subdirectories of /usr

| Subdirectory | Contents |
| :--- | :--- |
| bin | Most of your executable programs |
| lib | Library files |
| lib64 | 64-bit library files |
| local | Locally installed software that you created yourself (used to prevent it from being overwritten during a system update) |
| sbin | System administration programs |
| share | Documentation and man page files |

/var This directory contains variable data, including your system log files. Some of the typical subdirectories contained in /var are shown in Table 4-4.

With this structure in mind, let’s next discuss the types of files used by the Linux file system.

## Types of Files Used by Linux

When working with Linux, you need to be aware of the fact that there are a number of different file types used by the file system. This is another area where the Linux file system differs significantly from the Windows file system. With a Windows file system you basically have two entry types in the file system:

- Directories
- Files

Granted, you can have normal files, hidden files, shortcut files, word processing files, executable files, and so on. However, these are all simple variations of the basic Windows file.

On Linux, however, there are a variety of different file types used by the file system. These include the file types listed in Table 4-5.

Table 4-4 Subdirectories of /var

| Subdirectory | Contents |
| :--- | :--- |
| lib | Library files created by various services and applications running on the system |
| log | Log files from your system and from services running on the system |
| spool | Print queues |

Table 4-5 Linux File Types

| File Type | Description |
| :--- | :--- |
| Regular files | These files are similar to those used by the file systems of other operating systems—for example, executable files, word processing files, images, text files, etc. |
| Links | These files are pointers that point to other files in the file system. |
| FIFOs | FIFO stands for First In First Out. These are special files used to move data from one running process on the system to another. A FIFO file is basically a queue where the first chunk of data added to the queue is the first chunk of data removed from the queue. Data can only move in one direction through a FIFO. |
| Sockets | Sockets are similar to FIFOs in that they are used to transfer information between processes. Unlike FIFOs, however, sockets can move data bidirectionally. |

With this introduction to the Linux file system in mind, you're ready to start learning how to complete common file system tasks. Just as with any other operating system, you need to be able to create, copy, and move files and directories in the Linux file system. In this part of this chapter, we're going to spend some time reviewing how this is done.

If you have any experience working with the command line in other operating systems, such as DOS or Windows, you may be thinking that these tasks are trivial in nature. Believe it or not, these tasks can be difficult for many of my students when they are first learning how to use Linux. The key mistake I see is students trying to use Windows (and DOS) commands when working with the file system at the Linux shell prompt. I even catch myself doing this on occasion. I was presenting a demo for students recently and needed to copy some files on a Linux system. Without thinking, I entered copy instead of cp at the shell prompt and, of course, it didn't work. Boy was I red-faced! My students had a great time razzing me about that for the rest of the class!

As with Windows, you can perform file system manipulation tasks either from the shell prompt or from within the Linux GUI. Many who are coming to Linux from a Windows background are tempted to perform these tasks solely using the GUI utilities provided with most distributions.

While these graphical utilities are handy and easy to use, you still need to learn how to do these tasks from the shell prompt. I realize that this goes against standard practice with Windows systems. I've worked with many Windows users who don't know the command prompt even exists on their systems. With Linux, however, you need to first become proficient with shell commands and then use the GUI utilities for convenience. I say this for the following reasons:

- Most employers and coworkers won't take you seriously as a Linux administrator if you can't manage the system from the shell prompt. It just goes with the territory.
- Many Linux systems, especially those deployed as servers, don't run a GUI. Running a GUI environment requires a lot of CPU overhead. Any server admins prefer to allocate those CPU cycles to system services instead of moving the mouse cursor on the screen or running a screensaver. In this situation, you need to know how to do things from the shell prompt.
