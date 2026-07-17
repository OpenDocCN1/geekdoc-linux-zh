![](Image00000.jpg)

Linux Tutorials- Herong's Tutorial Examples![](Image00002.jpg)1.20, 2020Dr. Herong Yang© 2020 Dr. Herong Yang. All rights reserved.This book is a collection of notes and sample codes written by the author while he was learning Linux systems. Topics include using network configuration and security firewall; managing Linux file systems; installing CentOS systems; using SELinux (Security-Enhanced Linux) system; DNF/YUM software package manager; managing MySQL server; developing Python and PHP scripts; using GCC C/C++ compilers; managing vsftpd - Very Secure FTP daemon; running Conda - Environment and Package Manager. Updated in 2020 (Version 1.20) with SELinux tutorials. For latest updates and free sample chapters, visit http://www.herongyang.com/Linux.Table of Contents[About This Book](#text00003.html_a2N6)[Introduction to Linux Systems](#text00004.html_a2N7)["uname" - Display System Information](#text00005.html_a2N8)["free" - Display Free and Used Memory](#text00006.html_a2N9)[Process Management](#text00007.html_a2NA)["ps" - Display Current Processes](#text00008.html_a2NB)["jobs" - Manage Background Jobs](#text00009.html_a2NC)["tmux" - Terminal Multiplexer](#text00010.html_a2ND)[Linux File Systems](#text00011.html_a2NE)["df" - Display Free Space of File System](#text00012.html_a2NF)[Mount USB Drive as File System](#text00013.html_a2NG)["fdisk" - Format Disk Partitions](#text00014.html_a2NH)["dd" - Copy Data from/to Storage Devices](#text00015.html_a2NJ)[Use "dd" Command to Test I/O Speed](#text00016.html_a2NK)["hdparm" - Hard Disk Parameters](#text00017.html_a2NM)["du" - Display Disk Usage of Directories](#text00018.html_a2NN)[Mount Windows NTFS File System](#text00019.html_a2NP)[W95 Ext'd (LBA) Partition](#text00020.html_a2NR)[File System Types, IDs and Formats](#text00021.html_a2NS)[Installing CentOS](#text00022.html_a2NT)[Create CentOS Bootable USB](#text00023.html_a2NU)[Install CentOS from Bootable USB](#text00024.html_a2NV)[Install CentOS by Deleting Existing Partition](#text00025.html_a2NW)[SELinux - Security-Enhanced Linux](#text00026.html_a2NX)[What Is SELinux (Security-Enhanced Linux)](#text00027.html_a2NY)[SELinux Configuration and Status on CentOS](#text00028.html_a2NZ)[What Is SELinux User](#text00029.html_a2P0)[What Is SELinux Role](#text00030.html_a2P1)[What Is SELinux Type](#text00031.html_a2P2)[What Is SELinux Domain](#text00032.html_a2P3)[SELinux Policy Rule](#text00033.html_a2P4)[What Is SELinux Boolean](#text00034.html_a2P5)[SELinux Related Tools](#text00035.html_a2P6)[SELinux Error Messages](#text00036.html_a2P7)[SELinux Related Terminologies](#text00037.html_a2P8)[Network Connection on CentOS](#text00038.html_a2P9)[Setup Ethernet Connection on CentOS](#text00039.html_a2PA)[Network Firewall Tools on CentOS](#text00040.html_a2PB)["firewalld" and "firewall-cmd" on CentOS](#text00041.html_a2PC)["nftables" and "nft" on CentOS](#text00042.html_a2PD)["iptables" Command on CentOS](#text00043.html_a2PE)["nmap" - Network Mapper on CentOS](#text00044.html_a2PF)[Monitor Network Services on CentOS](#text00045.html_a2PG)[Software Package Manager on CentOS - DNF and YUM](#text00046.html_a2PH)[What Is DNF](#text00047.html_a2PJ)[What Is YUM](#text00048.html_a2PK)[Install and Manage Java Packages on CentOS](#text00049.html_a2PM)[Install and Manage Perl Packages on CentOS](#text00050.html_a2PN)[Install "git-core" for GitHub Packages on CentOS](#text00051.html_a2PP)[Running Apache Web Server (httpd) on Linux Systems](#text00052.html_a2PR)[Verify Apache Web Server "httpd"](#text00053.html_a2PS)[Running PHP Scripts on Linux Systems](#text00054.html_a2PT)[Install and Manage PHP Packages on CentOS](#text00055.html_a2PU)["php -i" - Dump PHP Environment Information](#text00056.html_a2PV)[Install and Manage PHP Modules on CentOS](#text00057.html_a2PW)[Files Used in PHP "include" Statements](#text00058.html_a2PX)[Publish PHP Scripts on Apache Web Server](#text00059.html_a2PY)[Dump PHP/Apache Environment Information](#text00060.html_a2PZ)[Apache PHP file_put_contents() Permission Denied](#text00061.html_a2R0)[SELinux Security Context on /var/www/html](#text00062.html_a2R1)[Migrate Old Scripts to New PHP Release](#text00063.html_a2R2)[Running MySQL Database Server on Linux Systems](#text00064.html_a2R3)[Install MySQL Database Server on CentOS](#text00065.html_a2R4)[Manage MySQL Server 'mysqld' on CentOS](#text00066.html_a2R5)[Set MySQL Server "root" Password on CentOS](#text00067.html_a2R6)[MySQL Server File Locations on CentOS](#text00068.html_a2R7)[MySQL Server Data Backups on CentOS](#text00069.html_a2R8)[MySQL Server Log Files on CentOS](#text00070.html_a2R9)[MySQL Server Socket Connection on CentOS](#text00071.html_a2RA)[MySQL Server TCP/IP Connection on CentOS](#text00072.html_a2RB)[Open Firewall for MySQL Server on CentOS](#text00073.html_a2RC)["Server sent charset unknown to the client" Error](#text00074.html_a2RD)[Performance of Inserting Integers to MySQL Database](#text00075.html_a2RE)[Performance Comparison of Inserting Integers vs. Strings](#text00076.html_a2RF)[Running Python Scripts on Linux Systems](#text00077.html_a2RG)[Install and Manage Python Engine on CentOS](#text00078.html_a2RH)["pip/pip3" Python Package Manager](#text00079.html_a2RJ)[Install MySQL Connector/Python on CentOS](#text00080.html_a2RK)[Install Python 2 Engine on CentOS](#text00081.html_a2RM)[vsftpd - Very Secure FTP Daemon](#text00082.html_a2RN)[Install vsftpd on CentOS](#text00083.html_a2RP)[vsftpd Server Configuration](#text00084.html_a2RR)[Setup FTP Sub-Directory for Local Users](#text00085.html_a2RS)[Test FTP Access Locally on CentOS](#text00086.html_a2RT)[Test FTP Access Remotely on CentOS](#text00087.html_a2RU)[Support FTP Over TLS on CentOS](#text00088.html_a2RV)[Disable SSH Access for FTP Users](#text00089.html_a2RW)[GCC - C/C++ Compiler on Linux Systems](#text00090.html_a2RX)[Install GCC C/C++ Compilers](#text00091.html_a2RY)["g++ --verbose" - GCC Compiler Steps and Settings](#text00092.html_a2RZ)["g++ -I..." and CPATH Environment Variable](#text00093.html_a2S0)["g++ -l..." to Link with Library Files](#text00094.html_a2S1)["g++ -c" and "ar src" to Build Static Library](#text00095.html_a2S2)["g++ -shared" to Build Dynamic Library](#text00096.html_a2S3)["ldd" - Dynamic Library Dependency Checker](#text00097.html_a2S4)["make" - Manage Program Build Process](#text00098.html_a2S5)[Conda - Environment and Package Manager](#text00099.html_a2S6)[What Is Conda](#text00100.html_a2S7)[Install Miniconda 3](#text00101.html_a2S8)[Introduction to Conda Environment](#text00102.html_a2S9)[References](#text00103.html_a2SA)Keywords: Linux, CentOS, macOS, Tutorials[Linux Tutorials - Herong's Tutorial Examples](#text00002.html_a2N5)∟ About This BookThis section provides some detailed information about this book - Linux Tutorials - Herong's Tutorial Examples.Title: Linux Tutorials - Herong's Tutorial ExamplesAuthor: Dr. Herong Yang - Contact by email via herong_yang@yahoo.com.Category: ProgrammingVersion/Edition: 1.20, 2020Number of pages in PDF format: 157Description: This book is a collection of notes and sample codes written by the author while he was learning Linux systems. Topics include using network configuration and security firewall; managing Linux file systems; installing CentOS systems; using SELinux (Security-Enhanced Linux) system; DNF/YUM software package manager; managing MySQL server; developing Python and PHP scripts; using GCC C/C++ compilers; managing vsftpd - Very Secure FTP daemon; running Conda - Environment and Package Manager. Updated in 2020 (Version 1.20) with SELinux tutorials.Keywords: C/C++, File System, Linux, MySQL, PHP, Python, SELinux, Unix.Copyright:

*   This book is under Copyright © 2020 Dr. Herong Yang. All rights reserved.
*   Material in this book may not be published, broadcasted, rewritten or redistributed in any form.
*   Code examples are provided as-is, with no warranty of any kind.

Revision history:

*   Version 1.20, 2020\. Added SELinux tutorials.
*   Version 1.00, 2019\. Completed first edition.

Web version: [http://www.herongyang.com/Linux](http://www.herongyang.com/Linux) - Provides free sample chapters, latest updates and readers' comments. The Web version of this book has been viewed a total of:

*   0 times as of December 2019.

PDF/EPUB version: [http://www.herongyang.com/Linux/PDF-Full-Version.html](http://www.herongyang.com/Linux/PDF-Full-Version.html) - Provides information on how to obtain the full version of this book in PDF, EPUB, or other format.[Linux Tutorials - Herong's Tutorial Examples](#text00002.html_a2N5)∟ Introduction to Linux SystemsProvides introductions and tutorial on Linux operating systems. Topics include 'uname' to display operating system information.["uname" - Display System Information](#text00005.html_a2N8)["free" - Display Free and Used Memory](#text00006.html_a2N9)Takeaways:

*   "uname” command can be used to display operating system information.

[Linux Tutorials - Herong's Tutorial Examples](#text00002.html_a2N5)∟ [Introduction to Linux Systems](#text00004.html_a2N7)∟ "uname" - Display System InformationProvides a tutorial example on how to display operating system information using the 'uname' command on Linux systems.The first thing you should do on a new Linux computer is to gather its system information as shown in this tutorial.1\. The most commonly used command to display Linux operating system information is the "uname" command.(on my CentOS 8 computer)
centos8$ uname -mprsv
Linux 4.18.0-147.el8.x86_64
   #1 SMP Wed Dec 4 21:51:45 UTC 2019 x86_64 x86_64

(on my CentOS 6 computer)
centos6$ uname -mprsv
Linux 2.6.32-696.20.1.el6.i686 #1 SMP Fri Jan 26 18:13:32 UTC 2018
   i686 i686 i386 GNU/Linux i386

(on my macOS 10 computer)
macos$ uname -mnprsv
Darwin 16.7.0 Darwin Kernel Version 16.7.0:
   Sun Jun  2 20:26:31 PDT 2019; root:xnu-3789.73.50~1/RELEASE_X86_64
   x86_64 i386
2\. On most Linux systems, the operating system information is accessible via a special file called /proc/version. You can use the "cat" command to display it:(on my CentOS 8 computer)
centos8$ cat /proc/version
Linux version 4.18.0-147.el8.x86_64
  (mockbuild@kbuilder.bsys.centos.org)
  (gcc version 8.3.1 20190507 (Red Hat 8.3.1-4) (GCC))
  #1 SMP Wed Dec 4 21:51:45 UTC 2019

(on my CentOS 6 computer)
centos6$ cat /proc/version
Linux version 2.6.32-696.20.1.el6.i686
  (mockbuild@x86_64_01.bsys.centos.org)
  (gcc version 4.4.7 20120313 (Red Hat 4.4.7-18) (GCC))
  #1 SMP Fri Jan 26 18:13:32 UTC 2018
3\. The CPU architecture is a key parameter when installing Linux systems and applications. You can use the "arch" command to display it:  
(on my CentOS 8 computer)
centos8$ arch
x86_64

(on my CentOS 6 computer)
centos6$ arch
i686

(on my macOS 10 computer)
macOS$ arch
i386
[Linux Tutorials - Herong's Tutorial Examples](#text00002.html_a2N5)∟ [Introduction to Linux Systems](#text00004.html_a2N7)∟ "free" - Display Free and Used MemoryProvides a tutorial example on how to display free and used memory information using the 'free' command on Linux systems.Another important information about your Linux system is the memory. You can use the "free" command to display memory statistics including free and used memory sizes. Here are some examples of "free" command output on my CentOS computer.1\. Display memory information using "free" with default options. The memory counts are displayed in kibibytes (1,024 bytes). Note that a kibibyte (1,024 bytes) is slightly different than a kilobyte (1,000 bytes).herong$ free
           total     used     free   shared  buff/cache   available
Mem:     7789220  2047412   677256   297448     5064552     5145248
Swap:    8085500        0  8085500
2\. To control the unit, you can use "free -b|k|m|g" options.herong$ free -m
           total     used     free   shared  buff/cache   available
Mem:        7606     1999      661      290        4945        5024
Swap:       7895        0     7895
3\. Or you can use "free -h" to display counts in human readable formats.  
herong$ free -h
           total     used     free   shared  buff/cache   available
Mem:       7.4Gi    2.0Gi    661Mi    290Mi       4.8Gi       4.9Gi
Swap:      7.7Gi       0B    7.7Gi
The output columns are defined as:

*   total - Total installed memory (MemTotal and SwapTotal in /proc/meminfo)
*   used - Used memory (calculated as total - free - buffers - cache)
*   free - Unused memory
*   shared - Memory used (mostly) by tmpfs
*   buffers - Memory used by kernel buffers (Buffers in /proc/meminfo)
*   cache Memory used by the page cache and slabs
*   buff/cache - Sum of buffers and cache
*   available - Estimation of how much memory is available for starting new applications, without swapping. Unlike the data provided by the cache or free fields, this field takes into account page cache and also that not all reclaimable memory slabs will be reclaimed due to items being in use

[Linux Tutorials - Herong's Tutorial Examples](#text00002.html_a2N5)∟ Process ManagementProvides introductions and tutorial on managing processes on Linux systems. Topics include 'ps' to display processes; 'jobs' and other commands to manage background jobs; 'tmux' tool to manage multiple shells and keep them in background.["ps" - Display Current Processes](#text00008.html_a2NB)["jobs" - Manage Background Jobs](#text00009.html_a2NC)["tmux" - Terminal Multiplexer](#text00010.html_a2ND)Takeaways:

*   "ps” command can be used to display processes running on the system.
*   "jobs" command can be used to display your background jobs that are running with inputs detached from keyboards.
*   "ctrl-z" can be used to stop a foreground job and send it to the background.
*   "bg" command can be used to resume a background job.
*   "fg" command can be used to bring a background job to the foreground.
*   "tmux" tool can be used to manage multiple shells in a single terminal window.
*   "tmux" tool automatically keeps its shells running when the terminal is disconnected.

[Linux Tutorials - Herong's Tutorial Examples](#text00002.html_a2N5)∟ [Process Management](#text00007.html_a2NA)∟ "ps" - Display Current ProcessesProvides a tutorial example on how to use 'ps' command to display current process on the system.What Is Process? - A process is a unit of work that is currently running in the operating system. A process has the following basic properties:

*   PID - A number that identifies the process.
*   UID - The user ID who owns the process.
*   Command - The command that initiated the process.
*   Time - The elapse time since the starting moment of the process.
*   Priority - A number that indicates the execution priority of the process comparing to other processes.
*   TTY (or Teletype) - A termainl device attached to the process to handle input and output.

You can use the "ps" command to display current processes and their properties. Here are some examples:1\. Display processes associated with the current terminal session using the "ps" command with default options.herong$ ps
  PID TTY          TIME CMD
 1171 pts/1    00:00:00 sleep
 1172 pts/1    00:00:00 ps
31723 pts/1    00:00:00 bash
2\. Display processes in long format using the "ps -l" command.herong$ ps -l
F S   UID   PID  PPID  C PRI  NI ADDR SZ WCHAN  TTY          TIME CMD
0 S  1000  1195 31723  0  80   0 -  1820 hrtime pts/1    00:00:00 sleep
0 R  1000  1213 31723  0  80   0 - 11191 -      pts/1    00:00:00 ps
0 S  1000 31723 31720  0  80   0 -  6271 -      pts/1    00:00:00 bash
3\. Display processes owned by myself or another user using the "ps -u" command.herong$ ps -u
USER       PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
herong     878  0.0  0.0   9800  2624 pts/0    S+   04:37   0:00 less
herong    1344  0.0  0.0  57184  3792 pts/1    R+   05:17   0:00 ps -u
herong    1345  0.0  0.0   9528  2192 pts/1    S+   05:17   0:00 more
herong   29872  0.0  0.0  24700  5372 pts/0    Ss   Aug24   0:00 -bash
herong   31723  0.0  0.0  25084  5704 pts/1    Ss   02:29   0:00 -bash
...

herong$ ps -u joe
...
4\. Display all processes on the system in long format using the "ps -el" command:$ ps -el
F S   UID   PID  PPID  C PRI  NI ADDR SZ WCHAN  TTY       TIME CMD
4 S     0     1     0  0  80   0 - 61833 -      ?     00:03:09 systemd
1 S     0     2     0  0  80   0 -     0 -      ?     00:00:01 kthreadd
1 I     0     3     2  0  60 -20 -     0 -      ?     00:00:00 rcu_gp
1 I     0     4     2  0  60 -20 -     0 -      ?     00:00:00 rcu_par_gp
1 I     0     8     2  0  60 -20 -     0 -      ?     00:00:00 mm_percpu_wq
1 S     0     9     2  0  80   0 -     0 -      ?     00:00:00 ksoftirqd/0
1 I     0    10     2  0  80   0 -     0 -      ?     00:02:42 rcu_sched
...
[Linux Tutorials - Herong's Tutorial Examples](#text00002.html_a2N5)∟ [Process Management](#text00007.html_a2NA)∟ "jobs" - Manage Background JobsProvides a tutorial example on how to use 'jobs' command to display background jobs, which are processes with input detached the keyboard. You can start a background job by adding the 'ampersand' sign to the end of the commmad.What Is Background Job? - A background job is a process with its input being detached from the keyboard device. Its output may still be attached to the screen.A foreground job is a process with its input being attached to the keyboard device. When you enter a command at the shell prompt to start a process, it will be started as a foreground job by default. The keyboard will be occupied by this foreground job until it is terminated. So you can only executed 1 process job at any time.If you want start a process as a background job to keep the keyboard free for the next process, you use the following 2 options:1\. Adding "&" at the end of the command line. This will start the process as a background job immediately. For example, the following command starts a process (ID=40120) as a background job (#=1).herong$ sleep 100000 &
[1] 40120
2\. Press "ctrl-z" during the execution of a foreground job. This will stop the foreground job and make it as a background job and keep it as stopped.herong$ sleep 50000
ctrl-z
[2]+  Stopped                 sleep 50000
If you want to see a list of your own background jobs, you can use the "jobs" command:herong$ jobs
[1]-  Running                 sleep 100000 &
[2]+  Stopped                 sleep 50000
If you want to resume a stopped job in the background, you can use the "bg #" command:herong$ bg 2
[2]+ sleep 50000 &

herong$ jobs
[1]-  Running                 sleep 100000 &
[2]+  Running                 sleep 50000 &
If you want to bring a background job to the foreground, you can use the "fg" command:herong$ fg 2
sleep 100000
One nice about running a command in the background is that it will to run, even if your shell session gets disconnected/closed.[Linux Tutorials - Herong's Tutorial Examples](#text00002.html_a2N5)∟ [Process Management](#text00007.html_a2NA)∟ "tmux" - Terminal MultiplexerProvides a tutorial example on how to use 'tmux' tool to manage multiple shells as windows and panes in a single terminal. 'tmux' automatically keeps all shells running when the terminal is disconnected.What Is "tmux"? - "tmux" is a terminal multiplexer. It lets you switch easily between several programs in one terminal, detach them (they keep running in the background) and reattach them to a different terminal.Here is the official description of "tmux" from its manual page:tmux is a terminal multiplexer: it enables a number of terminals to be
created, accessed, and controlled from a single screen.  tmux may be
detached from a screen and continue running in the background, then later
reattached.

When tmux is started it creates a new session with a single window and
displays it on screen.  A status line at the bottom of the screen shows
information on the current session and is used to enter interactive
commands.

A session is a single collection of pseudo terminals under the management
of tmux.  Each session has one or more windows linked to it.  A window
occupies the entire screen and may be split into rectangular panes,
each of which is a separate pseudo terminal (the pty(4) manual page
documents the technical details of pseudo terminals).  Any number of tmux
instances may connect to the same session, and any number of windows may
be present in the same session.  Once all sessions are killed, tmux exits.

Each session is persistent and will survive accidental disconnection
(such as ssh(1) connection timeout) or intentional detaching (with the
‘C-b d’ key strokes).  tmux may be reattached using:

      $ tmux attach

In tmux, a session is displayed on screen by a client and all sessions
are managed by a single server.  The server and each client are separate
processes which communicate through a socket in /tmp.
"tmux" is a nice tool that reduces the number of remote "ssh" sessions, saves time on trying to push processes to the background manually to prevent be killed by connection timeouts. Here is what I tried on my CentOS computer.1\. Install "tmux":herong$ sudo dnf install tmux

Installed:
 tmux-2.7-1.el8.x86_64
2\. Use "tmux" command to start a new "tmux" session, which starts a shell as the first pane in the first window of the "tmux" session.herong$ tmux
(in a child shell in "tmux")

herong$ exit
(back to the original shell)
3\. Use the following hot keys to control its windows and tabs:ctrl-b, %     split the screen in half from left to right
ctrl-b, "     split the screen in half from top to bottom
ctrl-b, array_key  switch to the pane in different directions
ctrl-b, c    create a new window
ctrl-b, 0|1|... switch to a given window
ctrl-b, d     detach from tmux, leaving it running in the background
...
ctrl-b, ?     display all hot keys
4\. Use "tmux ls|attach" to list and reattach to a detached or disconnected tmux session.herong$ tmux ls
0: 1 windows (created Tue Aug 25 20:16:44 2020) [122x42]

herong$ tmux attach
(old tmux is displayed again)
[Linux Tutorials - Herong's Tutorial Examples](#text00002.html_a2N5)∟ Linux File SystemsProvides introductions and tutorial on Linux file systems. Topics include 'df' to see disk free spaces of mounted file systems; 'mount' to connect to USB drive file systems; 'fdisk' to list partitions and file system types; 'dd' to copy data and test I/O speed; 'hdparm' to manage hard disk parameters.["df" - Display Free Space of File System](#text00012.html_a2NF)[Mount USB Drive as File System](#text00013.html_a2NG)["fdisk" - Format Disk Partitions](#text00014.html_a2NH)["dd" - Copy Data from/to Storage Devices](#text00015.html_a2NJ)[Use "dd" Command to Test I/O Speed](#text00016.html_a2NK)["hdparm" - Hard Disk Parameters](#text00017.html_a2NM)["du" - Display Disk Usage of Directories](#text00018.html_a2NN)[Mount Windows NTFS File System](#text00019.html_a2NP)[W95 Ext'd (LBA) Partition](#text00020.html_a2NR)[File System Types, IDs and Formats](#text00021.html_a2NS)Takeaways:

*   "df” command can be used to display free spaces of mounted file systems.
*   "mount" command can be used to bring file system partitions online. "umount" command can be used to bring them offline.
*   "fdisk -l " command can be used to list file system partitions and their format types of a given storage device.
*   "dd" command can be used to copy data as continuous blocks of bytes from one device to another bypassing file system structures.
*   "dd" command can also be used to test I/O (Input and Output) speed of a given storage device.
*   "hdparm" command can be used to to gather hard disk identification information and get/set its individual parameters.

[Linux Tutorials - Herong's Tutorial Examples](#text00002.html_a2N5)∟ [Linux File Systems](#text00011.html_a2NE)∟ "df" - Display Free Space of File SystemProvides a tutorial example on how to use 'df' command to display free spaces of mounted file systems on Linux systems.To see free spaces of mounted file systems, you can use the "df" command. Here are some sample outputs of the "df" command on my CentOS 8 computer.1\. Display free spaces of all mounted file systems using "df":herong$ df

Filesystem          1K-blocks    Used Available Use% Mounted on
devtmpfs              3875992       0   3875992   0% /dev
tmpfs                 3894608       0   3894608   0% /dev/shm
tmpfs                 3894608   18192   3876416   1% /run
tmpfs                 3894608       0   3894608   0% /sys/fs/cgroup
/dev/mapper/cl-root  52403200 6279684  46123516  12% /
/dev/mapper/cl-home  40813088  609176  40203912   2% /home
/dev/sda6              999320  148068    782440  16% /boot
tmpfs                  778920    1168    777752   1% /run/user/42
tmpfs                  778920    6960    771960   1% /run/user/1000
2\. Display free spaces in unit of Megabyte of all mounted file systems using "df -m":herong$ df -m

Filesystem          1M-blocks  Used Available Use% Mounted on
devtmpfs                 3786     0      3786   0% /dev
tmpfs                    3804     0      3804   0% /dev/shm
tmpfs                    3804    18      3786   1% /run
tmpfs                    3804     0      3804   0% /sys/fs/cgroup
/dev/mapper/cl-root     51175  6133     45043  12% /
/dev/mapper/cl-home     39857   595     39262   2% /home
/dev/sda6                 976   145       765  16% /boot
tmpfs                     761     2       760   1% /run/user/42
tmpfs                     761     7       754   1% /run/user/1000
3\. Display free spaces in unit of Gigabyte of all mounted file systems using "df --block-size=1G":herong$ df --block-size=1G

Filesystem          1G-blocks  Used Available Use% Mounted on
devtmpfs                    4     0         4   0% /dev
tmpfs                       4     0         4   0% /dev/shm
tmpfs                       4     1         4   1% /run
tmpfs                       4     0         4   0% /sys/fs/cgroup
/dev/mapper/cl-root        50     6        44  12% /
/dev/mapper/cl-home        39     1        39   2% /home
/dev/sda6                   1     1         1  16% /boot
tmpfs                       1     1         1   1% /run/user/42
tmpfs                       1     1         1   1% /run/user/1000
[Linux Tutorials - Herong's Tutorial Examples](#text00002.html_a2N5)∟ [Linux File Systems](#text00011.html_a2NE)∟ Mount USB Drive as File SystemProvides a tutorial example on how to mount the formatted partition of a USB drive on a Linux system as a file system.If you have a USB drive, you can insert it into a USB socket on your Linux system, and follow this tutorial to mount it as a new file system.1\. Check existing SCSI disk devices represented as /dev/sd* files:herong$ ls -l /dev/sd*

brw-rw----. 1 root disk 8,  0 Mar 26 21:17 /dev/sda
brw-rw----. 1 root disk 8,  1 Mar 26 21:17 /dev/sda1
brw-rw----. 1 root disk 8,  2 Mar 26 21:17 /dev/sda2
brw-rw----. 1 root disk 8,  5 Mar 26 21:17 /dev/sda5
brw-rw----. 1 root disk 8,  6 Mar 26 21:17 /dev/sda6
brw-rw----. 1 root disk 8,  7 Mar 26 21:17 /dev/sda7
2\. Insert the USB drive in a USB socket. And check SCSI disk devices again. Since USB drives are considered as SCSI disk devices on Linux system. You will see more devices are detected and represented as /dev/sd* files. In my example below, I see /dev/sdb representing the USB as a single storage as a whole, and /dev/sdb1 representing the first FAT32 formatted partition.herong$ ls -l /dev/sd*

brw-rw----. 1 root disk 8,  0 Mar 26 21:17 /dev/sda
brw-rw----. 1 root disk 8,  1 Mar 26 21:17 /dev/sda1
brw-rw----. 1 root disk 8,  2 Mar 26 21:17 /dev/sda2
brw-rw----. 1 root disk 8,  5 Mar 26 21:17 /dev/sda5
brw-rw----. 1 root disk 8,  6 Mar 26 21:17 /dev/sda6
brw-rw----. 1 root disk 8,  7 Mar 26 21:17 /dev/sda7
brw-rw----. 1 root disk 8, 16 Apr  4 02:25 /dev/sdb
brw-rw----. 1 root disk 8, 17 Apr  4 02:25 /dev/sdb1
3\. Find a mounting point on the root file system on my CentOS 8 computer, and mount the USB formatted partition device, /dev/sdb1\. You may see different mounting points on other Linux systems. By the way, you can not mount /dev/sdb, because it is not a formatted file system.herong$ ls -l /
lrwxrwxrwx.   1 root root    7 May 10  2019 bin -> usr/bin
dr-xr-xr-x.   6 root root 4096 Mar 26 21:18 boot
drwxr-xr-x.  20 root root 3700 Apr  4 08:25 dev
drwxr-xr-x. 144 root root 8192 Mar 30 07:37 etc
drwxr-xr-x.   3 root root   20 Mar 26 17:11 home
lrwxrwxrwx.   1 root root    7 May 10  2019 lib -> usr/lib
drwxr-xr-x.   2 root root    6 May 10  2019 media
drwxr-xr-x.   2 root root    6 May 10  2019 mnt
drwxr-xr-x.   2 root root    6 May 10  2019 opt
...

herong$ ls -l /media
total 0

herong$ sudo mount /dev/sdb1 /media
4\. Verify the formatted partition of the USB drive as a mounted file system:herong$ df

Filesystem          1K-blocks    Used Available Use% Mounted on
...
/dev/sdb1             7813124 1146116   6667008  15% /media
5\. Check the "System Volume Information" folder, which usually exists on the formatted partition of any USB drive.  
herong$ ls -l "/media/System Volume Information"

total 256
-rwxrwxrwx  1 herong  staff  76 Apr  2 20:43 IndexerVolumeGuid
-rwxrwxrwx  1 herong  staff  12 Apr  2 20:43 WPSettings.dat
6\. Remember to umount the USB file system before taking the USB drive out of the USB socket to avoid any data damage.herong$ sudo umount /dev/sdb1

(or)
herong$ sudo umount /media
Now I am ready to use /media to copy files from and to the USB drive.[Linux Tutorials - Herong's Tutorial Examples](#text00002.html_a2N5)∟ [Linux File Systems](#text00011.html_a2NE)∟ "fdisk" - Format Disk PartitionsProvides a tutorial example on how to manage disks, including USB drives, partitions and formats on Linux systems.If you want to manage partitions of storage devices like hard disks and USB drives, you need to learn how to use the "fdisk (format disk)" command as shown in this tutorial.1\. List of storage devices using "ls -l /dev/sd?" command. The "?" wildcard stands for 1 character to exclude partitions on each devices.herong$ ls -l /dev/sd?

brw-rw----. 1 root disk 8,  0 Mar 26 21:17 /dev/sda
brw-rw----. 1 root disk 8, 16 Apr  4 02:25 /dev/sdb
brw-rw----. 1 root disk 8, 32 Apr  4 08:02 /dev/sdc
brw-------. 1 root root 8, 48 Apr  4 08:25 /dev/sdd
2\. List partitions on first hard disk storage device using "fdisk -l" command. I see 5 partitions with different formats.herong$ sudo fdisk -l /dev/sda

Disk /dev/sda: 931.5 GiB, 1000204886016 bytes, 1953525168 sectors
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 4096 bytes
I/O size (minimum/optimal): 4096 bytes / 4096 bytes
Disklabel type: dos
Disk identifier: 0x2f50ca78

Device     Boot      Start        End    Sectors   Size Id Type
/dev/sda1  *          2048  167776255  167774208    80G  7 HPFS/NTFS/exFAT
/dev/sda2        167776256 1953523711 1785747456 851.5G  f W95 Ext'd (LBA)
/dev/sda5        167778304 1748721663 1580943360 753.9G  7 HPFS/NTFS/exFAT
/dev/sda6       1748723712 1750820863    2097152     1G 83 Linux
/dev/sda7       1750822912 1953523711  202700800  96.7G 8e Linux LVM
3\. List partitions on a USB storage device using "fdisk -l" command. I see one partition with W95 FAT32 format, with is compatible with Windows computers.herong$ sudo fdisk -l /dev/sdc

Disk /dev/sdc: 7.5 GiB, 8021606400 bytes, 15667200 sectors
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disklabel type: dos
Disk identifier: 0x04030201

Device     Boot Start      End  Sectors  Size Id Type
/dev/sdc1       10392 15667199 15656808  7.5G  c W95 FAT32 (LBA)
[Linux Tutorials - Herong's Tutorial Examples](#text00002.html_a2N5)∟ [Linux File Systems](#text00011.html_a2NE)∟ "dd" - Copy Data from/to Storage DevicesProvides a tutorial example on how to copy continuous blocks of data bytes from or to storage devices using the 'dd' command. File system structures can be bypassed.If you want to copy data as continuous blocks of bytes from one device to another, you can use the "dd (data duplicator)" command as shown in this tutorial. If device names are used in "dd" commands, file system structures are not respected.1\. Copy data from a raw device. This will read data continuously from the device without respecting the partition and format structures.(copy the first block (512 bytes) from a USB drive)
herong$ sudo dd count=1 if=/dev/sdb of=one-block
1+0 records in
1+0 records out
512 bytes copied, 6.1976e-05 s, 8.3 MB/s
2\. Copy data to a raw device. This will write data continuously to the device and whipping out the partition and format structures. This command is very dangerous. One typo in the device name could damage the MBR (Master Boot Record) of the hard disk, which is represented as /dev/sda.(copy CentOS 8 DVD image to a USB drive)
herong$ sudo dd if=CentOS-8.1.1911-x86_64-boot.iso of=/dev/sdb

(copy a backup file in TAR (Tape ARchiving) format to a tape device )
herong$ sudo dd if=backup.tar of=/dev/sdc

(copy 1 GB of '0' to the beginning of a tape device)
(this is a good way to remove sensitive data on old tapes)
herong$ sudo dd if=/dev/zero of=/dev/sdc bs=64k count=16k
[Linux Tutorials - Herong's Tutorial Examples](#text00002.html_a2N5)∟ [Linux File Systems](#text00011.html_a2NE)∟ Use "dd" Command to Test I/O SpeedProvides a tutorial example on how to test I/O speed of hard disk and USB drives using the 'dd' command with different block sizes.The "dd (data duplicator)" command can also be used to measure I/O (Input/Output) speed of a given storage device.Tests on my CentOS 8.0 computer1\. Test input (writing) speed of the internal hard disk. I see that bigger block size (bs) is more efficient when writing to the hard disk.herong$ pwd
/home/herong

herong$ dd if=/dev/zero of=one-giga bs=64k count=16k
16384+0 records in
16384+0 records out
1073741824 bytes (1.1 GB, 1.0 GiB) copied, 0.255833 s, 4.2 GB/s

herong$ dd if=/dev/zero of=one-giga bs=1k count=1024k
1048576+0 records in
1048576+0 records out
1073741824 bytes (1.1 GB, 1.0 GiB) copied, 1.98674 s, 540 MB/s

herong$ ls -l one*
-rw-rw-r--. 1 herong herong 1073741824 Apr  5 03:23 one-giga
2\. Test output (reading) speed of the internal hard disk. I see that bigger block size (bs) is more efficient when reading from the hard disk. I also see that reading is two times slower than writing, which is a little surprise to me.herong$ dd if=one-giga of=/dev/null bs=64k count=16k
16384+0 records in
16384+0 records out
1073741824 bytes (1.1 GB, 1.0 GiB) copied, 0.113039 s, 9.5 GB/s

herong$ dd if=one-giga of=/dev/null bs=1k count=1024k
1048576+0 records in
1048576+0 records out
1073741824 bytes (1.1 GB, 1.0 GiB) copied, 1.18922 s, 903 MB/s
3\. Test input (writing) speed of a USB drive. I see that the input speed on USB drive is about the same as the hard disk with block size of 1 KB, which is a little surprise to me.(USB drive is mounted on /media)
herong$ df /dev/sdc1
Filesystem     1K-blocks    Used Available Use% Mounted on
/dev/sdc1        7813124 1146116   6667008  15% /media

herong$ cd /media

herong$ sudo dd if=/dev/zero of=one-giga bs=64k count=16k
16384+0 records in
16384+0 records out
1073741824 bytes (1.1 GB, 1.0 GiB) copied, 0.937841 s, 1.1 GB/s

herong$ sudo dd if=/dev/zero of=one-giga bs=1k count=1024k
1048576+0 records in
1048576+0 records out
1073741824 bytes (1.1 GB, 1.0 GiB) copied, 2.12935 s, 504 MB/s
4\. Test output (reading) speed of the same USB drive. I see that the output speed on USB drive is about the same as the hard disk for both large and small block sizes, which is a little surprise to me.herong$ dd if=one-giga of=/dev/null bs=64k count=16k
16384+0 records in
16384+0 records out
1073741824 bytes (1.1 GB, 1.0 GiB) copied, 0.115699 s, 9.3 GB/s

herong$ dd if=one-giga of=/dev/null bs=1k count=1024k
1048576+0 records in
1048576+0 records out
1073741824 bytes (1.1 GB, 1.0 GiB) copied, 1.13126 s, 949 MB/s
Tests on my macOS 10 computer1\. Test input (writing) speed of the internal hard disk. I see that the input speed of my macOS hard disk is much slower that my CentOS computer.herong$ pwd
/Users/herong

herong$ dd if=/dev/zero of=one-giga bs=64k count=16k
16384+0 records in
16384+0 records out
1073741824 bytes transferred in 0.741450 secs (1,448,164,705 bytes/sec)

herong$ dd if=/dev/zero of=one-giga bs=1k count=1024k
1048576+0 records in
1048576+0 records out
1073741824 bytes transferred in 4.046084 secs (265,378,040 bytes/sec)
2\. Test output (reading) speed of the internal hard disk. I see that the output speed is much faster than input speed, which makes sense.herong$ dd if=one-giga of=/dev/null bs=64k count=16k
16384+0 records in
16384+0 records out
1073741824 bytes transferred in 0.218341 secs (4,917,726,275 bytes/sec)

herong$ dd if=one-giga of=/dev/null bs=1k count=1024k
1048576+0 records in
1048576+0 records out
1073741824 bytes transferred in 2.320591 secs (462,701,888 bytes/sec)
3\. Test input (writing) speed of the same USB drive. I see that the input speed on the same USB drive on macOS is about 200 times slower than than CentOS. I think the main cause of the speed drop is the USB to USB-C cable used to connect the USB drive.(USB drive is auto mounted on /Volumes/NO NAME)
herong$ df
Filesystem    512-blocks      Used Available Capacity Mounted on
...
/dev/disk3s1    15626248   2294808  13331440    15%   /Volumes/NO NAME

herong$ cd '/Volumes/NO NAME'

herong$ sudo dd if=/dev/zero of=one-giga bs=64k count=16k
16384+0 records in
16384+0 records out
1073741824 bytes transferred in 214.298787 secs (5,010,490 bytes/sec)

herong$ sudo dd if=/dev/zero of=one-giga bs=1k count=1024k
1048576+0 records in
1048576+0 records out
1073741824 bytes transferred in 208.157021 secs (5,158,326 bytes/sec)
4\. Test output (reading) speed of the same USB drive. I see that the output speed on USB drive is about 600 times faster than the input speed, which is a big surprise to me.herong$ dd if=one-giga of=/dev/null bs=64k count=16k
16384+0 records in
16384+0 records out
1073741824 bytes transferred in 0.353298 secs (3,039,196,314 bytes/sec)

herong$ dd if=one-giga of=/dev/null bs=1k count=1024k
1048576+0 records in
1048576+0 records out
1073741824 bytes transferred in 2.318289 secs (463,161,373 bytes/sec)
[Linux Tutorials - Herong's Tutorial Examples](#text00002.html_a2N5)∟ [Linux File Systems](#text00011.html_a2NE)∟ "hdparm" - Hard Disk ParametersProvides a tutorial example on how to use the 'hdparm' command to gather hard disk identification information and get/set individual parameters. 'hdparm' command does not work on normal USB drives.If you want to see and change hard disk parameters, you can use the "hdparm" command as shown in this tutorial.1\. Get hard disk identification information in a compact format with the "hdparm -i" command.herong$ sudo hdparm -i /dev/sda

/dev/sda:
 Model=WDC WD10EZEX-xxxxxx, FwRev=01.01A01, SerialNo=WD-xxxxxx
 Config={ HardSect NotMFM HdSw>15uSec SpinMotCtl Fixed DTR>5Mbs FmtGapReq }
 RawCHS=16383/16/63, TrkSize=0, SectSize=0, ECCbytes=0
 BuffType=unknown, BuffSize=unknown, MaxMultSect=16, MultSect=16
 CurCHS=16383/16/63, CurSects=16514064, LBA=yes, LBAsects=1953525168
 IORDY=on/off, tPIO={min:120,w/IORDY:120}, tDMA={min:120,rec:120}
 PIO modes:  pio0 pio3 pio4
 DMA modes:  mdma0 mdma1 mdma2
 UDMA modes: udma0 udma1 udma2 udma3 udma4 *udma5
 AdvancedPM=no WriteCache=enabled
 Drive conforms to: Reserved:  ATA/ATAPI-1,2,3,4,5,6,7
2\. Get hard disk identification information in a detailed format with the "hdparm -I" command. I see lot of useful information.herong$ sudo hdparm -I /dev/sda

/dev/sda:
ATA device, with non-removable media
  Model Number:       WDC WD10EZEX-xxxxxx
  Serial Number:      WD-xxxxxx
  Firmware Revision:  01.01A01
  Transport:          Serial, SATA 1.0a, SATA II Extensions, ...
Standards:
  Used: unknown (minor revision code 0x001f)
  Supported: 9 8 7 6 5
  Likely used: 9
Configuration:
  Logical    max  current
  cylinders  16383  16383
  heads    16  16
  sectors/track  63  63
  --
  CHS current addressable sectors:    16514064
  LBA    user addressable sectors:   268435455
  LBA48  user addressable sectors:  1953525168
  Logical  Sector size:                   512 bytes
  Physical Sector size:                  4096 bytes
  device size with M = 1024*1024:      953869 MBytes
  device size with M = 1000*1000:     1000204 MBytes (1000 GB)
  cache/buffer size  = unknown
  Nominal Media Rotation Rate: 7200
Capabilities:
  LBA, IORDY(can be disabled)
  Queue depth: 32
  Standby timer values: spec'd by Standard, with device specific minimum
  R/W multiple sector transfer: Max = 16  Current = 16
  DMA: mdma0 mdma1 mdma2 udma0 udma1 udma2 udma3 udma4 *udma5
       Cycle time: min=120ns recommended=120ns
  PIO: pio0 pio1 pio2 pio3 pio4
       Cycle time: no flow control=120ns  IORDY flow control=120ns
Commands/features:
  Enabled  Supported:
     *  SMART feature set
        Security Mode feature set
     *  Power Management feature set
     *  Write cache
     *  Look-ahead
     *  Host Protected Area feature set
     *  WRITE_BUFFER command
     *  READ_BUFFER command
     ...
Security:
  Master password revision code = 65534
    supported
  not  enabled
  not  locked
    frozen
  not  expired: security count
    supported: enhanced erase
  122min for SECURITY ERASE UNIT. 122min for ENHANCED SECURITY ERASE UNIT.
Logical Unit WWN Device Identifier: 5001xxxxxx
  NAA    : 5
  IEEE OUI  : 0014ee
  Unique ID  : xxxxxx
Checksum: correct
3\. Get detailed identification information of a USB drive. I don't see any useful information. So "hdparm" command is not design for all types of storage devices.herong$ sudo hdparm -I /dev/sdb

/dev/sdb:
SG_IO: bad/missing sense data, sb[]:  f0 00 05 00 00 00 00 14 ...

ATA device, with non-removable media
Standards:
  Likely used: 1
Configuration:
  Logical    max  current
  cylinders  0  0
  heads    0  0
  sectors/track  0  0
  --
  Logical/Physical Sector size:           512 bytes
  device size with M = 1024*1024:           0 MBytes
  device size with M = 1000*1000:           0 MBytes
  cache/buffer size  = unknown
Capabilities:
  IORDY not likely
  Cannot perform double-word IO
  R/W multiple sector transfer: not supported
  DMA: not supported
  PIO: pio0
3\. Get the read-only flag of a USB drive using the "hdparm -r" command.herong$ sudo hdparm -r /dev/sdb

/dev/sdb:
readonly      =  0 (off)
4\. Set the read-only flag of a USB drive using the "hdparm -r 1" command.herong$ sudo hdparm -r 1 /dev/sdb

/dev/sdb:
 setting readonly to 1 (on)
 readonly      =  1 (on)
5\. Verify the read-only flag of a USB drive. I see that the read-only flag on the USB drive is not working.(mount the only partition of the USB drive)
herong$ sudo mount /dev/sdb1 /media

herong$ cd /media

(create a new file on USB driver)
herong$ sudo touch test.txt

herong$ ls -l test.txt
-rwxr-xr-x. 1 root root    0 Apr  1 05:38 test.txt

herong$ sudo hdparm -r /dev/sdb
/dev/sdb:
 readonly      =  1 (on)
[Linux Tutorials - Herong's Tutorial Examples](#text00002.html_a2N5)∟ [Linux File Systems](#text00011.html_a2NE)∟ "du" - Display Disk Usage of DirectoriesProvides a tutorial example on how to use 'du' command to display disk usage of any given directories on Linux systems.To see how much disk space is used by a given directory, you can use the "du" command. Here are some sample outputs of the "du" command on my CentOS 8 computer.1\. Display disk usage of my home directory using "du":herong$ $ du ~
124876  ./ftp/files
124876  ./ftp
124880  ./work/pytorch
0  ./work/r
124884  ./work
4  ./.cache/pip/http/6/8/c/5/e
4  ./.cache/pip/http/6/8/c/5
4  ./.cache/pip/http/6/8/c
...
104  ./.cache/pip/http/c
592  ./.cache/pip/http
596  ./.cache/pip
0  ./.cache/matplotlib/tex.cache
28  ./.cache/matplotlib
624  ./.cache
0  ./.config/matplotlib
0  ./.config
4  ./.keras
250420  .
2\. Display disk usage without any sub-directory entries using "du -d 0":herong$ du -d 0
250420  .
3\. Display disk usage in human readable units using "du -h":herong$ du -d 0 -h
245M  .
4\. Display disk usage in units of KB, MB, or GB using "du -k|m|g":herong$ du -d 0 -k
250420  .
[Linux Tutorials - Herong's Tutorial Examples](#text00002.html_a2N5)∟ [Linux File Systems](#text00011.html_a2NE)∟ Mount Windows NTFS File SystemProvides a tutorial example on how to mount Windows NTFS (New Technology File System) file systems on Linux systems.If you have a hard disk partition formatted in Windows NTFS (New Technology File System) format, you may need to install addition device driver to mount it on Linux systems. Here is what I did to mount a NTFS partition on my CentOS 8 computer.1\. Check disk partitions and their formats. The output shows that partition /dev/sda5 uses NTFS format.herong$ sudo fdisk -l /dev/sda

Disk /dev/sda: 900.0 GiB
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 4096 bytes
I/O size (minimum/optimal): 4096 bytes / 4096 bytes
Disklabel type: dos

Device     Boot      Start        End    Sectors   Size Id Type
/dev/sda1  *          2048  167776255  167774208    80G  7 HPFS/NTFS/exFAT
/dev/sda2        167776256 1953523711 1785747456 851.5G  f W95 Ext'd (LBA)
/dev/sda5        167778304 1748721663 1580943360 753.9G  7 HPFS/NTFS/exFAT
/dev/sda6       1748723712 1750820863    2097152     1G 83 Linux
/dev/sda7       1750822912 1953523711  202700800  96.7G 8e Linux LVM
2\. Try to mount it with default options. I am getting the "unknown filesystem type 'ntfs'" error.herong$ sudo mount /dev/sda5 /mnt
mount: /mnt: unknown filesystem type 'ntfs'.

herong$ sudo mount -t ntfs /dev/sda5 /mnt
mount: /mnt: unknown filesystem type 'ntfs'.
3\. Search Internet NTFS driver for CentOS and found "ntfs-3g" package.4\. Try to install "ntfs-3g" package with the "dnf" tool. But not available in CentOS package repository.herong$ sudo dnf search ntfs
No matches found.

herong$ sudo dnf search ntfs-3g
No matches found.
5\. Get the source code of ntfs-3gherong$ wget https://tuxera.com/opensource/ntfs-3g_ntfsprogs-2017.3.23.tgz

herong$ tar zxvf ntfs-3g_ntfsprogs-2017.3.23.tgz
6\. Compile and install it. "Make" and "GCC" are required.herong$ cd ntfs-3g_ntfsprogs-2017.3.23

herong$ ./configure
checking build system type... x86_64-unknown-linux-gnu
checking host system type... x86_64-unknown-linux-gnu
checking target system type... x86_64-unknown-linux-gnu
...
configure: creating ./config.status
config.status: creating Makefile
config.status: creating include/Makefile
...
You can type now 'make' to build ntfs-3g.

herong$ make
(some warnings)
...

herong$ make install
...
libtool: install: /usr/bin/install -c .... /usr/local/bin/ntfs-3g.probe
libtool: install: /usr/bin/install -c .... /bin/ntfs-3g
libtool: install: /usr/bin/install -c .... /bin/lowntfs-3g
...
7\. Mount the NTFS partition again with "ntfs-3g" drive:herong$ sudo mount -t ntfs-3g /dev/sda5 /mnt
The disk contains an unclean file system (0, 0).
The file system wasn't safely closed on Windows. Fixing.

herong$ df
...
/dev/sda5           790471676 416858252 373613424  53% /mnt
Cool. I can read my old files on the Windows disk on my CentOS computer now![Linux Tutorials - Herong's Tutorial Examples](#text00002.html_a2N5)∟ [Linux File Systems](#text00011.html_a2NE)∟ W95 Ext'd (LBA) PartitionProvides a quick introduction on W95 Ext'd LBA (Windows 95 Extended Logical Block Addressing) Partition, which is actually a container to hold sub-partitions.If you are using a hard disk create from a Windows computer, you may see a special partition with the "W95 Ext'd (LBA)" type. W95 Ext'd (LBA) stands for Windows 95 Extended Logical Block Addressing."W95 Ext'd LBA" is not a file system partition. It is actually a container to hold sub-partitions. On Windows systems, a hard disk can only be divided up to 4 partitions. "W95 Ext'd LBA" technology allows you create more sub-partitions from those 4 primary partitions.If you see a hard disk that has more than 4 partitions, or you see a partition index higher than 4, you know that "W95 Ext'd LBA" is used on the hard disk.For example, I have the following partitions on my CentOS computer:herong$ sudo fdisk -l /dev/sda

Disk /dev/sda: 900.0 GiB
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 4096 bytes
I/O size (minimum/optimal): 4096 bytes / 4096 bytes
Disklabel type: dos

Device     Boot      Start        End    Sectors   Size Id Type
/dev/sda1  *          2048  167776255  167774208    80G  7 HPFS/NTFS/exFAT
/dev/sda2        167776256 1953523711 1785747456 851.5G  f W95 Ext'd (LBA)
/dev/sda5        167778304 1748721663 1580943360 753.9G  7 HPFS/NTFS/exFAT
/dev/sda6       1748723712 1750820863    2097152     1G 83 Linux
/dev/sda7       1750822912 1953523711  202700800  96.7G 8e Linux LVM
The output tells me that:

*   The hard disk has only 2 primary partitions /dev/sda1 and /dev/sda2.
*   /dev/sda1 has 80 GB in Windows NTFS format with the boot sector to serve my Windows system
*   /dev/sda2 has 850 GB in "W95 Ext'd LBA" format and contains 3 sub-partitions: /dev/sda5, /dev/sda6 and /dev/sda7.
*   /dev/sda5 is sub-partition with 753 GB in Windows NTFS format.
*   /dev/sda6 is sub-partition with 1 GB in Linux format to hold Linux /root files.
*   /dev/sda7 is sub-partition with 96 GB in Linux LVM format to server my Linux system.

So do not try to mount "W95 Ext'd LBA" formatted /dev/sda2 to Linux system, it is not a true file system.[Linux Tutorials - Herong's Tutorial Examples](#text00002.html_a2N5)∟ [Linux File Systems](#text00011.html_a2NE)∟ File System Types, IDs and FormatsProvides a list of commonly used File System formats and their identification codes on Linux systemsIf you receive a storage device from a friend, you may have trouble to mount its partitions on your Linux computer. This is because the storage device could be created with a file system format, which is not recognized by the Linux computer.To help you dealing with this situation, here is a list of commonly used File System formats and handling suggestions.1\. Linux - "Linux (ID: 83)" is used to identify some old Linux native file systems, like xiafs, ext2, ext3, reiserfs, etc. It may still be used to hold the /root files on todays Linux systems, like CentOS.2\. Linux LVM - "Linux LVM (ID: 8e)" is used to identify the Linux LVM (Logical Volume Manager) partition. It is used on CentOS systems as the main file system.3\. Linux Swap - "Linux Swap (ID: 82)" is used to identify the Linux swap partition.4\. FAT16 - "FAT16 (ID: 6)" is used to identify the 16-bit FAT (File Allocation Table) partition, which is used by old DOS (Disk Operating System) computers. Most Linux systems supports FAT16 by default.5\. NTFS - "NTFS (ID: 7)" is used to identify the NTFS (New Technology File System) partition, which is used by old Windows NT computers. You may need to install "ntfs-3g" device driver to support it.6\. HPFS - "HPFS (ID: 7)" is used to identify the HPFS (New Technology File System) partition, which is an IFS (Installable File System) used by old OS/2 computers. You need to install special device drivers to support it.7\. exFAT - "exFAT (ID: 7)" is used to identify the exFAT (Extended File Allocation Table) partition, which is used by old Windows Vista computers. You may need to install "fuse-exfat" device driver to support it.8\. W95 Ext'd LBA - "W95 Ext'd LBA (ID: f)" is used to identify the Windows 95 Extended LBA (Logical Block Addressing) partition. Note that "W95 Ext'd LBA" is not a file system partition. It is actually a container to hold sub-partitions. On Windows systems, a hard disk can only be divided up to 4 partitions. "W95 Ext'd LBA" technology allows you create more sub-partitions from those 4 primary partitions.9\. OpenBSD - "OpenBSD (ID: a6)" is used to identify the OpenBSD (Open Berkeley Software Distribution) partition, which is used by OpenBSD computers. You need to install special device drivers to support it.10\. Mac OS-X - "Mac OS-X (ID: a8)" is used to identify the Mac OS-X partition, which is used by Mac OS-X computers. You need to install special device drivers to support it.[Linux Tutorials - Herong's Tutorial Examples](#text00002.html_a2N5)∟ Installing CentOSProvides tutorial examples on installing CentOS Linux system. Topics include downloading CentOS ISO image file; copying image file with 'dd' command to create bootable USB drive; installing CentOS from bootable USB drive.[Create CentOS Bootable USB](#text00023.html_a2NU)[Install CentOS from Bootable USB](#text00024.html_a2NV)[Install CentOS by Deleting Existing Partition](#text00025.html_a2NW)Takeaways:

*   You can download CentOS ISO image and create a bootable USB drive using the "dd" command on a macOS computer.
*   Installing CentOS system from a Bootable USB drive is straightforward, if you have enough free space on the hard disk.
*   You can use the built-in hard disk tool delete existing partitions to free up space during the CentOS installation process.

[Linux Tutorials - Herong's Tutorial Examples](#text00002.html_a2N5)∟ [Installing CentOS](#text00022.html_a2NT)∟ Create CentOS Bootable USBProvides a tutorial example on how to download the full CentOS ISO image file and create a bootable USB drive on a macOS computer.CentOS 8 is the latest release of the CentOS system, which is the open source version of RHEL (Red Hat Enterprise Linux). If you want to try it, you can follow what I did as described below to down the CentOS 8.1 ISO image file and create a bootable USB drive.1\. Go to CentOS download Website at [https://wiki.centos.org/Download](https://wiki.centos.org/Download) . I see a list of CentOS 8, 7, and 6 download options.2\. Click "mirrors" button next to "CentOS 8.1 (1911)" I see a list of download mirror sites.3\. Select a mirror site near you, like http://centos.les.net/. I see two ISO image files: CentOS-8.1.1911-x86_64-boot.iso, and CentOS-8.1.1911-x86_64-dvd1.iso. They are for computers with an x86_64 CPU architecture.

*   *-boot.iso is much smaller and contains only the bootable CentOS 8 kernel. When installing CentOS 8 with *-boot.iso, additional system and application packages needed to be downloaded on the fly.
*   *-dvd1.iso is much larger and contains all system packages and basic application packages. You can install CentOS 8 with *-dvd1.iso without download anything from the Internet.

4\. Click "CentOS-8.1.1911-x86_64-dvd1.iso" and save it to my macOS computer. I select CentOS-8.1.1911-x86_64-dvd1.iso, because it matches the CPU architecture x86_64 of the Lenovo computer I want to install CentOS on. You can select ISO files for other architectures by going to the parent directory on the mirror site.5\. Wait until the download is completed, which may take some time.6\. Copy "CentOS-8.1.1911-x86_64-dvd1.iso" to a USB drive using the "dd" command on my macOS computer. You can also do this by using "Etcher" or "Rufus" ISO tools, which is much safer than the "dd" command.(list file systems on storage devices)
macOS$ df
/dev/disk1           29% 1024263 4293943016    0%   /
/dev/disk2s1          3%       0          0  100%   /Volumes/NO NAME

(copy ISO file to the USB drive, /dev/disk2, not the file system)
(large block size of 64k is more efficient and take less time)
sudo dd if=CentOS-8.1.1911-x86_64-dvd1.iso of=/dev/disk2 bs=64k
7\. Label this USB drive as "CentOS 8.1 Bootable".See the next tutorial on how to boot from this USB drive and install CentOS on any computer.[Linux Tutorials - Herong's Tutorial Examples](#text00002.html_a2N5)∟ [Installing CentOS](#text00022.html_a2NT)∟ Install CentOS from Bootable USBProvides a tutorial example on how to install CentOS operating system from a CentOS bootable USB drive on a Lenovo computer.After creating the CentOS bootable USB drive, you can follow this tutorial to try it on Lenovo computer.1\. Power off the Lenovo computer and remove all USB drives.2\. Insert the "CentOS Bootable" USB drive to Lenovo computer and turn the power back on.3\. Wait for the CentOS installation screen after the computer finishing booting from the USB drive. If it is still booting from the internal hard disk, you need to change the BIOS book sequence to make sure USB drive is listed before internal hard disk. BIOS setting is accessible by pressing F10 at the beginning of the boot process.4\. Select "Install CentOS Linux" from the installation screen. I see the language selection screen.5\. Select "English" from the installation screen and click "Continue". I see the installation summary screen.6\. Click "Begin Installation", if you want to take the default configuration and there is enough free space on the hard disk. I see the root user setting screen.7\. Enter a new password for the root user, and create a new user "herong" with administrator privilege.8\. Take out the USB drive and reboot the computer. I see CentOS 8 running on my computer!.Cool. Installing CentOS 8 is so easy!![](Image00003.jpg)Install CentOS Linux System[Linux Tutorials - Herong's Tutorial Examples](#text00002.html_a2N5)∟ [Installing CentOS](#text00022.html_a2NT)∟ Install CentOS by Deleting Existing PartitionProvides a tutorial example on how to delete existing hard disk partition to free up space to install CentOS system on Lenovo computers.If you don't have enough free space (un-partitioned space) on the hard disk, CentOS installation program will force you to select which existing partition to delete to free up space for the new CentOS system. Here is what I did on my second Lenovo computer.1\. Boot the computer from the CentOS bootable USB drive.2\. Continue the installation process until the installation summary screen. I see that the "Installation Destination" in the system section is highlighted with a warning.2\. Click on "Installation Destination" link. I see the "Installation Destination" configuration page with two storage devices listed: the internal hard disk and the bootable USB. The hard disk is fully partitioned with only 2.55 MB free space left.3\. Select the internal hard disk as the installation destination. And check the "I would like to make additional space available" checkbox.4\. Click "Done" button. I see a warning message saying that there is not space to install CentOS. But I can use the built-in space reclaim tool to shrink or delete existing partitions.5\. Click "Reclaim Space". I see 3 partitions on my hard disk listed.6\. Select the third partition, which has junk data on it. And click "Delete" to free up enough space for the CentOS system.7\. Click "Reclaim Space" again to go back to the installation summary screen.8\. Click "Begin Installation" to finish the installation process.![](Image00004.jpg)Install CentOS by Deleting Hard Disk Partition[Linux Tutorials - Herong's Tutorial Examples](#text00002.html_a2N5)∟ SELinux - Security-Enhanced LinuxProvides introductions and tutorial on SELinux (Security-Enhanced Linux). Topics include introduction of SELinux basic concepts; User, Role, Domain, Type, Class, and Boolean; Type Enforcement policy rule syntax and database; making changes to SELiunx policy rules; using SELinux related tools.[What Is SELinux (Security-Enhanced Linux)](#text00027.html_a2NY)[SELinux Configuration and Status on CentOS](#text00028.html_a2NZ)[What Is SELinux User](#text00029.html_a2P0)[What Is SELinux Role](#text00030.html_a2P1)[What Is SELinux Type](#text00031.html_a2P2)[What Is SELinux Domain](#text00032.html_a2P3)[SELinux Policy Rule](#text00033.html_a2P4)[What Is SELinux Boolean](#text00034.html_a2P5)[SELinux Related Tools](#text00035.html_a2P6)[SELinux Error Messages](#text00036.html_a2P7)[SELinux Related Terminologies](#text00037.html_a2P8)Takeaways:

*   SELinux is a security architecture for Linux® systems that allows administrators to have more control over who can access the system.
*   A SELinux User is an abstract concept that represents a group of real users on the Linux system as security subject in SELinux system.
*   A SELinux Role is an abstract concept that represents a set of permissions grouped together for a specific functional role.
*   A SELinux Type is an abstract concept that represents a set of files/directories grouped together, so that security policy can be applied at the group level instead of individually at files/directories level.
*   A SELinux Domain is an abstract concept that represents a set of running processes grouped together, so that security policy can be applied at the group level instead of individually at process level.
*   A SELinux Type Enforcement policy rule is defined in a form of 'allow "source" on "target" of "class" with "permissions"'.
*   A SELinux Boolean is a Boolean flag that can be added to one or more SELinux policy rules to turn on or turn off those rules.
*   "semanage" command is used to configure certain elements of SELinux policy without requiring modification to or recompilation from policy source.
*   "seinfo" command is used to print out SELinux policy information.
*   "sesearch" - SELinux policy rule search tool.
*   SELinux error messages are logged in the /var/log/messages file.

[Linux Tutorials - Herong's Tutorial Examples](#text00002.html_a2N5)∟ [SELinux - Security-Enhanced Linux](#text00026.html_a2NX)∟ What Is SELinux (Security-Enhanced Linux)Provides a quick introduction on SELinux (Security-Enhanced Linux), which is made of two components: Security Server and Policy Database. They work together to provide security services to any subject who wants to access a given object on the Linux system.What Is SELinux (Security-Enhanced Linux)? - SELinux is a security architecture for Linux® systems that allows administrators to have more control over who can access the system. It was originally developed by the United States National Security Agency (NSA) as a series of patches to the Linux kernel using Linux Security Modules (LSM).SELinux is made of two components: SELinux Security Server and SELinux Policy Database. They work together to provide security services to any subject who wants to access a given object on the Linux system as shown below (source: mit.edu):![](Image00005.jpg)SELinux - Access Permission Decision ProcessWhen a subject, (for example, an application), attempts to access an object (for example, a file), the policy enforcement server in the kernel checks an access vector cache (AVC), where subject and object permissions are cached. If a decision cannot be made based on data in the AVC, the request continues to the security server, which looks up the security context of the application and the file in a matrix. Permission is then granted or denied, with an avc: denied message detailed in /var/log/messages if permission is denied. The security context of subjects and objects is applied from the installed policy, which also provides the information to populate the security server's matrix.When SELinux is running and enforced, your Linux system will have two levels of security controls running together, which will cause you mores confusions, but give you a more secure environment.

*   Linux Default Access Control - A DAC (Discretionary Access Control) type of permission system based an access control matrix of ownerships (User, Group, and Other) and access types (Read, Write, and Execute).
*   SELinux Access Control - A MAC (Mandatory Access Control) type of permission system based on explicit access rules stored a policy database.

So a user may the permission to read a file by the Linux Default Access Control, but still gets rejected by the SELinux Access ControlFor more information, see "USING SELINUX" guide at [https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/8/html/using_selinux/index](https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/8/html/using_selinux/index) .[Linux Tutorials - Herong's Tutorial Examples](#text00002.html_a2N5)∟ [SELinux - Security-Enhanced Linux](#text00026.html_a2NX)∟ SELinux Configuration and Status on CentOSProvides a tutorial example on how to view the current SELinux configuration by looking at the /etc/sysconfig/selinux file, and the current SELinux status by running the /usr/sbin/sestatus command.If you are running a CentOS 8 system, SELinux is installed and running by default. You can view the current configuration of SELinux by looking at the /etc/sysconfig/selinux file. Here is what I have on my CentOS 8 computer:herong$ more /etc/sysconfig/selinux

# This file controls the state of SELinux on the system.

# SELINUX= can take one of these three values:
#     enforcing - SELinux security policy is enforced.
#     permissive - SELinux prints warnings instead of enforcing.
#     disabled - No SELinux policy is loaded.
SELINUX=enforcing

# SELINUXTYPE= can take one of these three values:
#     targeted - Targeted processes are protected,
#     minimum - Modification of targeted policy. Only selected processes
#         are protected.
#     mls - Multi Level Security protection.
SELINUXTYPE=targeted
So I am running SELinux in "enforcing" mode on "targeted" processes.If you want to view the current status SELinux, you can run the "/usr/sbin/sestatus" command:herong$ /usr/sbin/sestatus -v

SELinux status:                 enabled
SELinuxfs mount:                /sys/fs/selinux
SELinux root directory:         /etc/selinux
Loaded policy name:             targeted
Current mode:                   enforcing
Mode from config file:          enforcing
Policy MLS status:              enabled
Policy deny_unknown status:     allowed
Memory protection checking:     actual (secure)
Max kernel policy version:      31

Process contexts:
Current context:                unconfined_u:unconfined_r:unconfined_t:s0-s0:c0.c1023
Init context:                   system_u:system_r:init_t:s0

File contexts:
Controlling terminal:           unconfined_u:object_r:user_devpts_t:s0
/etc/passwd                     system_u:object_r:passwd_file_t:s0
/etc/shadow                     system_u:object_r:shadow_t:s0
/bin/bash                       system_u:object_r:shell_exec_t:s0
/bin/login                      system_u:object_r:login_exec_t:s0
/bin/sh                         system_u:object_r:bin_t:s0 -> system_u:object_r:shell_exec_t:s0
/sbin/agetty                    system_u:object_r:getty_exec_t:s0
/sbin/init                      system_u:object_r:bin_t:s0 -> system_u:object_r:init_exec_t:s0
/usr/sbin/sshd                  system_u:object_r:sshd_exec_t:s0
[Linux Tutorials - Herong's Tutorial Examples](#text00002.html_a2N5)∟ [SELinux - Security-Enhanced Linux](#text00026.html_a2NX)∟ What Is SELinux UserProvides a quick introduction on what is SELinux User, and a tutorial example on how to view the current SELinux User mapping, as well as change SELinux User mapping for a specific user.There are several basic concepts used by SELinux: SELinux User, SELinux Role, SELinux Domain, and SELinux Type. Together, they are used to define SELinux security policies in the form of:  "SELinux Users"
    can play
      "SELinux Roles"
        can go to
          "SELinux Domains"
            have access to
              "SELinux Types"
What Is SELinux User? A SELinux User is an abstract concept that represents a group of real users on the Linux system as security subject in SELinux system. By default, SELinux has the following pre-defined SELinux users:

*   guest_u - Intended for users with the lowest privilege. A guest_u user has no access to networking, no script execution privileges in /home, nor can make use of sudo or su commands to gain higher privileges.
*   root - Intended for the root user with the highest privilege.
*   staff_u - Intended for users that need to perform both non-administrative and administrative tasks. A staff_u user have access to GUI, to networking, and to the use of the sudo command to gain privileges.
*   sysadm_u - Intended for users who perform only administrative tasks. A sysadm_u user can perform all tasks like a staff_u user, plus he/she can use also the su command.
*   system_u - Intended for special users to run system services.
*   unconfined_u - Intended for users with hardly any restrictions except for specificaly targeted services.
*   user_u - Intended for regular users with no special privileges.
*   xguest_u - Similar to guest_u user. A xguest_u user has the sample privilege as a guest_u user, plus he/she can access to GUI and to the network, but only via the Firefox browser.

Here is what I did on my CentOS 8 computer to see how Linux users are mapped to SELinux users. And to change the mapping for "john" to ban him using the Internet.1\. To see how Linux users are mapped to SELinux users, use the "semanage login -l". By default, all users are mapped to the "unconfined_u" SELinux User on CentOS 8 system. So everyone can use the Internet.herong$ sudo semanage login -l

Login Name           SELinux User         MLS/MCS Range        Service

__default__          unconfined_u         s0-s0:c0.c1023       *
root                 unconfined_u         s0-s0:c0.c1023       *
2\. To add new entry that maps "john" to the guest_u SELinux user, use the "semanage login -a" command.herong$ sudo semanage login -a -s guest_u john

herong$ sudo semanage login -l
Login Name           SELinux User         MLS/MCS Range        Service
__default__          unconfined_u         s0-s0:c0.c1023       *
john                 guest_u              s0                   *
root                 unconfined_u         s0-s0:c0.c1023       *
3\. To verify the change, ask "john" to login and try the ping command. He will get a "Permission denied" error.john$ ping google.com

ping: socket: Permission denied
4\. To remove the SELinux user entry for "john", use the "semanage login -d" command.herong$ sudo semanage login -d -s guest_u john
[Linux Tutorials - Herong's Tutorial Examples](#text00002.html_a2N5)∟ [SELinux - Security-Enhanced Linux](#text00026.html_a2NX)∟ What Is SELinux RoleProvides a quick introduction on what is SELinux Role, and a tutorial example on how to view what SELinux Roles are permitted for each SELinux User, as well as change my current SELinux Role.In the last tutorial, we learned what is SELinux User. Now let's take a look at SELinux Role.What Is SELinux Role? A SELinux Role is an abstract concept that represents a set of permissions grouped together for a specific functional role. This gives the system the flexibility to associate multiple roles to a single user. So SELinux system is RBAC (Role-Based Access Control) system.By default, SELinux has the following pre-defined SELinux roles:

*   guest_r - The guest user role, which has the lowest privilege.
*   user_r - The regular user role, which is meant to only allow user applications and other non-privileged objects.
*   staff_r - Similar to the user_r role, but might be allowed to receive more system information than a regular user. This role is mostly given to users that should be allowed to switch towards other roles.
*   sysadm_r - System administrative role; this is a very powerful role as it is allowed most target objects.
*   system_r - System role, not meant to be switched to directly.
*   unconfined_r - The unrestricted user role.
*   xguest_r - Similar to the guest_r role, but can access to GUI.

Here is what I did on my CentOS 8 computer to see what SELinux Roles are permitted for a specific SELinux User. And to change the SELinux Role of a given SELinux User.1\. To see what SELinux Roles are permitted for each SELinux user, use the "semanage user -l".herong$ sudo semanage user -l

                Labeling   MLS/       MLS/                          
SELinux User    Prefix     MCS Level  MCS Range        SELinux Roles

guest_u         user       s0         s0               guest_r
root            user       s0         s0-s0:c0.c1023   staff_r sysadm_r system_r unconfined_r
staff_u         user       s0         s0-s0:c0.c1023   staff_r sysadm_r system_r unconfined_r
sysadm_u        user       s0         s0-s0:c0.c1023   sysadm_r
system_u        user       s0         s0-s0:c0.c1023   system_r unconfined_r
unconfined_u    user       s0         s0-s0:c0.c1023   system_r unconfined_r
user_u          user       s0         s0               user_r
xguest_u        user       s0         s0               xguest_r
2\. To find out what is my SELinux User and what SELinux Role I am playing, user the "id" command. Notice that my SELinux User and my SELinux Role are listed as the first 2 fields in the "context" attribute. The other fields represent SELinux Type, security level, and security category.herong$ id

uid=1000(herong) gid=1000(herong) groups=1000(herong),10(wheel) \
   context=unconfined_u:unconfined_r:unconfined_t:s0-s0:c0.c1023
3\. To change my current SELinux Role from "unconfined_r" to "system_r", use the "newrole -r system_r" command. This is allowed because both "system_r" and "unconfined_r" roles are associated with permitted for "unconfined_u" user according the output of "semanage user -l".herong$ newrole -r system_r
Note that you may need to install "policycoreutils-newrole" to use the "newrole" command.[Linux Tutorials - Herong's Tutorial Examples](#text00002.html_a2N5)∟ [SELinux - Security-Enhanced Linux](#text00026.html_a2NX)∟ What Is SELinux TypeProvides a quick introduction on what is SELinux Type, and a tutorial example on how to view what SELinux Types assigned to files/directories, as well as change SELinux Types on files/directories.In previous tutorials, we learned what is SELinux User and what is SELinux Role. We also learned what SELinux Role a SELinux User can play. Now let's take a look at SELinux Type.What Is SELinux Type? A SELinux Type is an abstract concept that represents a set of files/directories grouped together, so that security policy can be applied at the group level instead of individually at files/directories level.By default, SELinux has a long list of pre-defined SELinux types. Some of them are listed below:default_t
bin_t
boot_t
device_t
etc_t
httpd_log_t
lib_t
man_t
mnt_t
public_content_t
shell_exec_t
sysfs_t
tmp_t
usr_t
var_lib_t
var_t

removable_device_t
sound_device_t
tape_device_t
tty_device_t

home_root_t
auth_home_t
config_home_t
mail_home_t

user_home_t
user_tmp_t

...
When a new file or directory is created, SELinux will assign it to a default SELinux Type according a set of pre-defined settings.The SELinux Type assigned to a file/directory is stored in its context attribute as the third field, In the example below, file "/home/herong/myfile" is assigned to the "user_home_t" SELinux type.herong$ stat ~/myfile
  File: /home/herong/myfile
  Size: 0           Blocks: 0          IO Block: 4096   regular empty file
Device: fd02h/64770d  Inode: 6680        Links: 1
Access: (0664/-rw-rw-r--)  Uid: ( 1000/  herong)   Gid: ( 1000/  herong)

Context: unconfined_u:object_r:user_home_t:s0

Access: 2020-09-12 04:50:12.558518507 -0400
Modify: 2020-09-12 04:50:12.558518507 -0400
Change: 2020-09-12 04:50:12.558518507 -0400
The SELinux context attribute of a file is also called SELinux file label. The process of assigning a SELinux type to a file is called SELinux File Labeling.The SELinux file context (file label) stores the complete security information for a file in 5 fields as shown below:SELinux File Context =
  user:role:type:level:category
There are several ways to view and manage SELinux Types on files and directories:1\. View file/directory contexts using "ls -Z" command.herong$ ls -Z ~/myfile

unconfined_u:object_r:user_home_t:s0 /home/herong/myfile
2\. Change the SELinux Type of file/directory using "chcon -t" command.herong$ chcon -t user_tmp_t ~/myfile

herong$ ls -Z ~/myfile
unconfined_u:object_r:user_tmp_t:s0 /home/herong/myfile
3\. View SELinux default file context settings:herong$ sudo semanage fcontext -l

SELinux fcontext     type             Context

/                    directory        system_u:object_r:root_t:s0
/.*                  all files        system_u:object_r:default_t:s0
/[^/]+               regular file     system_u:object_r:etc_runtime_t:s0
/\.autofsck          regular file     system_u:object_r:etc_runtime_t:s0
/afs                 directory        system_u:object_r:mnt_t:s0
/bacula(/.*)?        all files        system_u:object_r:bacula_store_t:s0
/bin                 all files        system_u:object_r:bin_t:s0
/bin/.*              all files        system_u:object_r:bin_t:s0
/bin/alsaunmute      regular file     system_u:object_r:alsa_exec_t:s0
/bin/bash            regular file     system_u:object_r:shell_exec_t:s0
/bin/tcsh            regular file     system_u:object_r:shell_exec_t:s0

/boot                all files        system_u:object_r:boot_t:s0
/boot/.*             all files        system_u:object_r:boot_t:s0
/dev                 directory        system_u:object_r:device_t:s0
/dev/(misc/)?agpgart character device system_u:object_r:agp_device_t:s0
/dev/(misc/)?psaux   character device system_u:object_r:mouse_device_t:s0
...

/home/[^/]+/.+       all files        unconfined_u:object_r:user_home_t:s0
...
4\. Check for files/directories that have different SELinux types than default. It will print the ~/myfile with the SELinux type change I did earlier.herong$ sudo fixfiles check ~

Would relabel /home/herong/myfile from unconfined_u:object_r:user_tmp_t:s0 \
   to unconfined_u:object_r:user_home_t:s0
5\. Restore SELinux types on files/directories to default:herong$ sudo fixfiles restore ~/myfile

herong$ ls -Z ~/myfile
unconfined_u:object_r:user_home_t:s0 /home/herong/myfile
[Linux Tutorials - Herong's Tutorial Examples](#text00002.html_a2N5)∟ [SELinux - Security-Enhanced Linux](#text00026.html_a2NX)∟ What Is SELinux DomainProvides a quick introduction on what is SELinux Domain, which is an abstract concept that represents a set of running processes grouped together, so that security policy can be applied at the group level instead of individually at process level.In previous tutorials, we learned what is SELinux User, what is SELinux Role and what is SELinux type. Now let's take a look at SELinux Domain.What Is SELinux Domain? A SELinux Domain is an abstract concept that represents a set of running processes grouped together, so that security policy can be applied at the group level instead of individually at process level.By default, SELinux has a long list of pre-defined SELinux domains. Some of them are listed below:accountsd_t
alsa_t
auditd_t
avahi_t
boltd_t
chronyd_t
colord_t
crond_t
cupsd_t
dnsmasq_t
firewalld_t
fsdaemon_t
ftpd_t
fwupd_t
gssproxy_t
httpd_t
init_t
irqbalance_t
kernel_t
ksmtuned_t
lsmd_t
mcelog_t
modemmanager_t
mysqld_t
policykit_t
rngd_t
rpcbind_t
rtkit_daemon_t
sshd_t
syslogd_t
system_dbusd_t
systemd_logind_t
systemd_machined_t
tuned_t
udev_t
unconfined_t
virtd_t
xdm_t
xdm_t
When a new process is created, SELinux will assign it to a default SELinux Domain according a set of pre-defined settings.The SELinux Domain assigned to a process is stored in its context attribute as the third field. In the example below, process "bash" is assigned to the "unconfined_t" SELinux domain.herong$ ps -Z | grep bash

unconfined_u:unconfined_r:unconfined_t:s0-s0:c0.c1023 20713 pts/1 00:00:00 bash
The SELinux context attribute of a process is also called SELinux process label. The process of assigning a SELinux type to a file is called SELinux Process Labeling.The SELinux process context (process label) stores the complete security information for a process in 5 fields as shown below:SELinux Process Context =
  user:role:domain:level:category
Actually, SELinux Domain can be viewed as a special case of SELinux Type, if we consider a SELinux Type as representation of a group of resources. Files and processes are just two different types of resources.[Linux Tutorials - Herong's Tutorial Examples](#text00002.html_a2N5)∟ [SELinux - Security-Enhanced Linux](#text00026.html_a2NX)∟ SELinux Policy RuleProvides a quick introduction on SELinnux Policy rules and how to use 'sesearch' command to review them.In previous tutorials, we learned 4 most important entities of in the SELinux system: User, Role, Domain and Type. They are used to define SELinux security policies in a hierarchical form of:  "SELinux Users"
    can play
      "SELinux Roles"
        can go to
          "SELinux Domains"
            have access to
              "SELinux Types"
Now let's look at the bottom part of the SELinux security policy hierarchy, which is also called Type Enforcement policy:"SELinux Domains"
  have access to
    "SELinux Types"
The SELinux Type Enforcement policy is actually a set of policy rules in the form similar to:allow "source" on "target" of "class" with "permissions"

where:
  source - A SELinux Domain
  target - A SELinux Domain or Type
  permissions - A list of actions permitted
  class - A SELinux Class acting as a subset of targets
Below is an example of a SELinux policy rule retrieved by the "sesearch" command:herong$ sesearch --allow --source httpd_t --target httpd_log_t --class file

allow httpd_t httpd_log_t:file { append create getattr ioctl lock open ... };
The above policy rule tells us that Any process in the "httpd_t" SELinux Domain has "append create getattr ioctl lock open ..." permissions on "file" SELinux Class of the "httpd_log_t" SELinux Type.Let's verify what processes are in the "httpd_t" SELinux Domain:herong$ ps -eZ | grep httpd_t

system_u:system_r:httpd_t:s0     3427 ?        00:02:43 php-fpm
system_u:system_r:httpd_t:s0     3428 ?        00:03:01 httpd
Can these processes append new log entries to the httpd "access-log" file? The answer is yes, because it is of the "httpd_log_t" SELinux Type:herong$ sudo ls -Z /var/log/httpd/access_log

system_u:object_r:httpd_log_t:s0 /var/log/httpd/access_log
Can a "httpd_t" process create new files in the "/var/www/html" directory? The answer is no, because "create" permission is not listed in the related policy rule: 
herong$ sudo ls -dZ /var/www/html
  system_u:object_r:httpd_sys_content_t:s0 /var/www/html

herong$ sesearch --allow --source httpd_t --target httpd_sys_content_t --class dir
  allow httpd_t httpd_sys_content_t:dir { getattr ioctl lock open read search };
The SELinux Type Enforcement policy rules are also called "allow" rules in the SELinux Policy Database. You can get a list of all "allow" rules using the "sesearch --allow" command:herong$ sesearch --allow | more
allow NetworkManager_etc_rw_t NetworkManager_etc_rw_t:filesystem associate;
allow NetworkManager_etc_t NetworkManager_etc_t:filesystem associate;
allow NetworkManager_exec_t NetworkManager_exec_t:filesystem associate;
allow NetworkManager_log_t NetworkManager_log_t:filesystem associate;
allow NetworkManager_log_t tmp_t:filesystem associate;
allow NetworkManager_log_t tmpfs_t:filesystem associate;
...
[Linux Tutorials - Herong's Tutorial Examples](#text00002.html_a2N5)∟ [SELinux - Security-Enhanced Linux](#text00026.html_a2NX)∟ What Is SELinux BooleanProvides a quick introduction on SELinux Boolean, which is a Boolean flag that can be added to one or more SELinux policy rules to turn on or turn off those rules.What Is SELinux Boolean? - A SELinux Boolean is a Boolean flag that can be added to one or more SELinux policy rules to turn on or turn off those rules.By default, SELinux has a long list of pre-defined SELinux Booleans. You can use the "semanage boolean -l" to see them and their current settings:herong$ sudo semanage boolean -l
SELinux boolean           State  Default Description

abrt_anon_write           (off  ,  off)  Allow abrt to anon write
abrt_handle_event         (off  ,  off)  Allow abrt to handle event
antivirus_can_scan_system (off  ,  off)  Allow antivirus to can scan system
antivirus_use_jit         (off  ,  off)  Allow antivirus to use jit
auditadm_exec_content     (on   ,   on)  Allow auditadm to exec content
authlogin_radius          (off  ,  off)  Allow authlogin to radius
authlogin_yubikey         (off  ,  off)  Allow authlogin to yubikey
boinc_execmem             (on   ,   on)  Allow boinc to execmem
...
httpd_can_network_connect (off  ,  off)  Allow httpd to can network connect
...
If a SELinux policy rule is controlled by a SELinux Boolean, The boolean flag will be listed at the end of the rule. For the following policy rule says that a "httpd_t" process can "name_connect" on "port_type:tcp_socket" type only when "httpd_can_network_connect" Boolean is True.herong$ sesearch --allow --source httpd_t | grep 'httpd_can_network_connect '

allow httpd_t port_type:tcp_socket name_connect; [ httpd_can_network_connect ]:True
There are several ways to manage SELinux Boolean settings:semanage boolean -l
  To list all Booleans and their settings

getsebool -a
  To list all Booleans and their settings

setsebool boolean_name on
  To turn on a given Boolean

setsebool -P abrt_anon_write on
  To turn on a given Boolean and save the change permanently

togglesebool boolean_name
  To toggle a given Boolean
[Linux Tutorials - Herong's Tutorial Examples](#text00002.html_a2N5)∟ [SELinux - Security-Enhanced Linux](#text00026.html_a2NX)∟ SELinux Related ToolsProvides quick introductions of commonly used tools related SELinux.There are several important tools that allows to manage the SELinux system:1\. "semanage" - SELinux Policy Management tool.herong$ semanage -h
...
semanage is used to configure certain elements of SELinux policy without
requiring modification to or recompilation from policy source.

positional arguments:
  import     Import local customizations
  export     Output local customizations
  login      Manage login mappings between linux users and SELinux Users
  user       Manage SELinux Users (Roles and levels for an SELinux User)
  port       Manage network port type definitions
  ibpkey     Manage infiniband ibpkey type definitions
  ibendport  Manage infiniband end port type definitions
  interface  Manage network interface type definitions
  module     Manage SELinux policy modules
  node       Manage network node type definitions
  fcontext   Manage file context mapping definitions
  boolean    Manage booleans to selectively enable functionality
  permissive Manage process type enforcement mode
  dontaudit  Disable/Enable dontaudit rules in policy
...
2\. "seinfo" - SELinux policy information tool. "seinfo" is not included in the default CentOS 8 system. You need to install the 'setools-console' package to use it.herong$ seinfo
bash: seinfo: command not found...
Install package 'setools-console' to provide command 'seinfo'? [N/y] n

herong$ sudo dnf install setools-console
...
Installed:
  setools-console-4.2.2-2.el8.x86_64    

herong$ seinfo -h
...
Component Queries:
  -a [ATTR], --attribute [ATTR]  Print type attributes.
  -b [BOOL], --bool [BOOL]       Print Booleans.
  -c [CLASS], --class [CLASS]    Print object classes.
  -r [ROLE], --role [ROLE]       Print roles.
  -t [TYPE], --type [TYPE]       Print types.
  -u [USER], --user [USER]       Print users.
...
3\. "sesearch" - SELinux policy rule search tool. "sesearch" is not included in the default CentOS 8 system. You need to install the 'setools-console' package to use it.herong$ sesearch -h
usage: sesearch [-h] [--version] [-v] [--debug] [-A] [--allow] [--allowxperm]
    [--auditallow] [--auditallowxperm] [--dontaudit]
    [--dontauditxperm] [--neverallow] [--neverallowxperm] [-T]
    [--type_change] [--type_member] [--role_allow] [--role_trans]
    [--range_trans] [-s SOURCE] [-t TARGET] [-c TCLASS] [-p PERMS]
    [-x XPERMS] [-D DEFAULT] [-b BOOL] [-eb] [-ep] [-ex] [-ds]
    [-dt] [-rs] [-rt] [-rc] [-rd] [-rb]
    [policy]
4\. "newrole" - Run a shell with a new SELinux role. "newrole" is not included in the default CentOS 8 system. You need to install the 'policycoreutils-newrole' package to use it.herong$ newrole
bash: newrole: command not found...
Install package 'policycoreutils-newrole' to provide command 'newrole'? [N/y]

herong$ sudo dnf install policycoreutils-newrole
...
policycoreutils-newrole-2.9-9.el8.x86_64      

Installed:
  policycoreutils-newrole-2.9-9.el8.x86_64    

herong$ newrole
USAGE: newrole [ -r role ] [ -t type ] [ -l level ] [ -p ] [ -V ] [ -- args ]
5\. "fixfiles" - Fix file SELinux security contexts.herong$ man fixfiles

   fixfiles [-v] [-F] [-f] relabel
   fixfiles [-v] [-F] { check | restore | verify } dir/file ...
   fixfiles [-v] [-F] [-B | -N time ] { check | restore | verify }
   fixfiles [-v] [-F] -C PREVIOUS_FILECONTEXT { check | restore | verify }
   fixfiles [-F] [-B] onboot
...       
[Linux Tutorials - Herong's Tutorial Examples](#text00002.html_a2N5)∟ [SELinux - Security-Enhanced Linux](#text00026.html_a2NX)∟ SELinux Error MessagesProvides a quick introduction on SELinux error messages, which are recorded in the /var/log/messages file. You can get more detailed information about the error and some suggested solutions.By default, SELinux error messages are logged in the /var/log/messages file.Here are some examples of SELinux error messages I found on my CentOS 8 computer.1\. httpd/php-fpm failed to run a PHP script file due to incorrect SELinux type. The error message suggest you to run "sealert" to get more detailed information.herong$ sudo cat /var/log/messages | grep SELinux | more  
...
SELinux is preventing /usr/sbin/php-fpm from read access
  on the file test.php. For complete SELinux messages run:
  sealert -l 06a19151-14d3-4930-9e18-4c0f06963350

herong$ sealert -l 06a19151-14d3-4930-9e18-4c0f06963350
SELinux is preventing /usr/sbin/php-fpm from read access on file test.php.

*****  Plugin catchall_boolean (89.3 confidence) suggests   *****

If you want to allow httpd to read user content
Then you must tell SELinux about this by enabling the
  'httpd_read_user_content' boolean.

Do
  setsebool -P httpd_read_user_content 1

Additional Information:
Source Context                system_u:system_r:httpd_t:s0
Target Context                unconfined_u:object_r:user_home_t:s0
Target Objects                test.php [ file ]
Source                        php-fpm
Source Path                   /usr/sbin/php-fpm
Host                          localhost.localdomain
Source RPM Packages           
Target RPM Packages           
Policy RPM                    selinux-policy-3.14.3-20.el8.noarch
Selinux Enabled               True
Policy Type                   targeted
Enforcing Mode                Enforcing
...
2\. httpd/php-fpm failed to run a PHP script file that tries to run the "curl" interface. The suggested solution is pretty accurate.herong$ sudo cat /var/log/messages | grep SELinux | more  
...
setroubleshoot[24609]: SELinux is preventing /usr/bin/curl from name_connect
  access on the tcp_socket port 80\. For complete SELinux messages run:
  sealert -l 8bb769b4-02ca-4f9e-ac41-ffe7e6a95d45

herong$ sealert -l 8bb769b4-02ca-4f9e-ac41-ffe7e6a95d45
SELinux is preventing /usr/bin/curl from name_connect access on the
  tcp_socket port 443.

*****  Plugin catchall_boolean (24.7 confidence) suggests   *****

If you want to allow httpd to can network connect
Then you must tell SELinux about this by enabling the
   'httpd_can_network_connect' boolean.

Do
setsebool -P httpd_can_network_connect 1

Additional Information:
Source Context                system_u:system_r:httpd_t:s0
Target Context                system_u:object_r:http_port_t:s0
Target Objects                port 443 [ tcp_socket ]
Source                        curl
Source Path                   /usr/bin/curl
Port                          443
Host                          localhost.localdomain
Source RPM Packages           curl-7.61.1-11.el8.x86_64
Target RPM Packages           
Policy RPM                    selinux-policy-3.14.3-20.el8.noarch
...
[Linux Tutorials - Herong's Tutorial Examples](#text00002.html_a2N5)∟ [SELinux - Security-Enhanced Linux](#text00026.html_a2NX)∟ SELinux Related TerminologiesProvides a list of commonly used terminologies related SELinux.Here are some commonly used terminologies related to SELinux:

*   ACL (Access Control List) - A list of permissions associated with an object. For example, the "rw-rw-r--" is an ACL associated with a file in my home directory: "-rw-rw-r-- . 1 herong herong 0 Sep 12 04:50 myfile". It says "herong" as the owner can read and write, users in "herong" group can read and write, and other users can read.
*   AVC (Access Vector Vache) - A cache where subject and object permissions are stored for fast access.
*   DAC (Discretionary Access Control) - A type of permission system that is based on ACL (Access Control List) associated with each and every objects. Linux default security used DAC.
*   MAC (Mandatory Access Control) - A type of permission system that is based on a set of explicit security policies stored in a database. SELinux uses MAC.
*   MCS (Multi-Category Security) - The ability for a permission system to associated different categories (for example: Core, Utility, Add-on) of securities to information objects.
*   MLS (Multi-Level Security) - The ability for a permission system to associated different levels (for example: Unclassified, Confidential, Secret, Top Secret) of securities to information objects. Security levels are having hierarchical relations. Higher security levels are usually have less permitted actions.
*   SELinux User - An abstract concept that represents a group of real users on the Linux system as security subject in SELinux system.
*   SELinux Role - An abstract concept that represents a set of permissions grouped together for a specific functional role.
*   SELinux Type - An abstract concept that represents a set of files/directories grouped together, so that security policy can be applied at the group level instead of individually at files/directories level.
*   SELinux Domain - An abstract concept that represents a set of running processes grouped together, so that security policy can be applied at the group level instead of individually at process level.
*   SELinux Class - An abstract concept that represents a subset of SELinux Types based on the nature of the targeted resource, like "file", "dir", "socket", etc.

[Linux Tutorials - Herong's Tutorial Examples](#text00002.html_a2N5)∟ Network Connection on CentOSProvides introductions and tutorial on network configuration and firewall on CentOS systems. Topics include introduction of Ethernet connection with auto DHCP configuration; 'ifconfig' to view current network configuration; 'firewalld' daemon and 'firewall-cmd' CLI as firewall frontend tools; 'nftables' daemon and 'nft' CLI as firewall backend tools; 'nmap' as network scanner; 'netstat' as network activity monitor.[Setup Ethernet Connection on CentOS](#text00039.html_a2PA)[Network Firewall Tools on CentOS](#text00040.html_a2PB)["firewalld" and "firewall-cmd" on CentOS](#text00041.html_a2PC)["nftables" and "nft" on CentOS](#text00042.html_a2PD)["iptables" Command on CentOS](#text00043.html_a2PE)["nmap" - Network Mapper on CentOS](#text00044.html_a2PF)[Monitor Network Services on CentOS](#text00045.html_a2PG)Takeaways:

*   Ethernet connection setting can be automatically done with DHCP (Dynamic Host Configuration Protocol) service from the local network on CentOS systems.
*   "ifconfig" command can be used to view the current network configuration on all network interfaces on CentOS systems.
*   "firewalld" daemon and "firewall-cmd" CLI (Command Line Interface) are the frontend tools to manage network firewall on CentOS systems.
*   "nftables" daemon and "nft" CLI (Command Line Interface) are the backend tools to manage network firewall on CentOS systems.
*   "iptables" command is replaced by "nftables" daemon and "nft" CLI on CentOS 8 systems.
*   "nmap (Network Mapper)” is a network exploration tool and security scanner.
*   "netstat (Network Status)” is a network activity monitor tool.

[Linux Tutorials - Herong's Tutorial Examples](#text00002.html_a2N5)∟ [Network Connection on CentOS](#text00038.html_a2P9)∟ Setup Ethernet Connection on CentOSProvides a tutorial example on how to review and troubleshoot Ethernet connection on CentOS 8 systems.If you are running a CentOS system on a desktop computer, it is most likely having an Ethernet connection to the local network. Here is what I did to review and setup the Ethernet connection on my CentOS 8 computer.1\. Make sure the computer is connected with an Ethernet cable to the local network. You should see two lights next to the Ethernet port. If one of them is blinking, then there are some data activities between your computer and the network.2\. Review Ethernet connection settings from the desktop screen.

*   Click the Ethernet icon on the top-right corner of the screen.
*   Click to open "Wired" connection line. You should see the Network settings screen.
*   Click the switch to turn it on.
*   Click the settings icon. You should see Wired connection details.

3\. Read the Wired connection details. By default, your IP address, default route (gateway), DNS are dynamically configured by the DHCP (Dynamic Host Configuration Protocol) service from the local network. There is no need to change them.Link Speed: 100 Mb/s
IPv4 Address: 192.168.1.100
Hardware Address: ...
Default Route: 192.168.1.1
DNS: 192.168.1.1
![](Image00006.jpg)Ethernet Network Setup on CentOS4\. You can also verify the Ethernet connection with the "ifconfig" command:herong$ ifconfig
eno1: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
    inet 192.168.1.100  netmask 255.255.255.0  broadcast 192.168.1.255
    inet6 fe80::...:fe80  prefixlen 64  scopeid 0x20<link>
    ether 39:39:...  txqueuelen 1000  (Ethernet)
    RX packets 1162982  bytes 311120747 (296.7 MiB)
    RX errors 0  dropped 61365  overruns 0  frame 0
    TX packets 247671  bytes 58741459 (56.0 MiB)
    TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0
    device interrupt 20  memory 0xf7c00000-f7c20000
5\. Verify the Internet connection using the "ping" command:herong$ ping bing.com
PING bing.com (204.79.197.200) 56(84) bytes of data.
64 bytes from a-0001.a-msedge.net (204.79.197.200): icmp_seq=1 ttl=118 time=21.1 ms
64 bytes from a-0001.a-msedge.net (204.79.197.200): icmp_seq=2 ttl=118 time=20.9 ms
...
64 bytes from a-0001.a-msedge.net (204.79.197.200): icmp_seq=9 ttl=118 time=20.8 ms
^C
--- bing.com ping statistics ---
9 packets transmitted, 9 received, 0% packet loss, time 18ms
rtt min/avg/max/mdev = 20.658/21.993/30.929/3.163 ms
6\. Check the following if the "ping" command fails:

*   Check the Ethernet cable connections at both ends.
*   Change the Ethernet cable to a new one.
*   Move your computer to different Ethernet jacket.
*   Verify local network gateway firewall settings. Make sure your IP address or MAC address is not blocked on the blacklist.

7\. If you have trouble connecting to the Internet during CentOS installation, you can download the *-dvd1.iso version to install CentOS from the ISO image without Internet connection.[Linux Tutorials - Herong's Tutorial Examples](#text00002.html_a2N5)∟ [Network Connection on CentOS](#text00038.html_a2P9)∟ Network Firewall Tools on CentOSProvides quick descriptions on 3 major network firewall tools, 'firewalld/fireall-cmd', 'nftables/nft', and 'iptables' on CentOS 8 systems.After connecting your CentOS system to the Internet, you need to review and revise firewall settings to protect your system.CentOS system uses a number tools to manage the network firewall. Here are 3 major ones:1\. "firewalld" and "fireall-cmd" - A firewall daemon and a CLI (Command Line Interface) works together as a frontend tool to manage the network firewall. "firewalld" uses "nftables/iptables" as the backend engine.2\. "nftables" and "nft" - A firewall daemon and a CLI (Cammand Line Interface) works together as a backend engine for packet filtering and classification. "nftables" uses "/etc/nftables" directory to store its rules. "nftables" is installed on CentOS 8 by default to replace "iptables".3\. "iptables" - A basic administration tool for IPv4/IPv6 packet filtering and NAT (Network Address Translation) in the Linux kernel. "iptables" uses "/usr/sbin/iptables" to store its rules. "iptables" is now replaced by "nftables" on CentOS 8 systems.Here is diagram that shows how firewalld, nftables/iptables and other tools are related to each other (source: https://firewalld.org).![](Image00007.jpg)CentOS Firewall Tools - firewalld and nftables/iptables[Linux Tutorials - Herong's Tutorial Examples](#text00002.html_a2N5)∟ [Network Connection on CentOS](#text00038.html_a2P9)∟ "firewalld" and "firewall-cmd" on CentOSProvides a tutorial example on how to use 'firewalld' daemon and 'firewall-cmd' CLI to manage network firewall on CentOS 8 systems."firewalld" is a service daemon that works together with the "firewall-cmd" CLI (Command Line Interface) to form a front-end tool for the "nftables/iptables" tool to control the Internet traffic. Here is what I did to ensure that "firewalld" and "firewall-cmd" are working on my CentOS 8 computer.1\. Make sure that I have the latest version of "firewalld" installed with the "dnf info" command:herong$ sudo dnf info firewalld

Installed Packages
Name         : firewalld
Version      : 0.7.0
Release      : 5.el8
Architecture : noarch
Size         : 1.9 M
Source       : firewalld-0.7.0-5.el8.src.rpm
Repository   : @System
From repo    : anaconda
Summary      : A firewall daemon with D-Bus interface providing a dynamic firewall
URL          : http://www.firewalld.org
License      : GPLv2+
Description  : firewalld is a firewall service daemon that provides a dynamic customizable
             : firewall with a D-Bus interface.
2\. Make sure that "firewalld" service is running with the "systectl status" command:herong$ sudo systemctl status firewalld

 firewalld.service - firewalld - dynamic firewall daemon
   Loaded: loaded (/usr/lib/systemd/system/firewalld.service; enabled;
            vendor preset: enabled)
   Active: active (running)
     Docs: man:firewalld(1)
 Main PID: 1360 (firewalld)
    Tasks: 3 (limit: 26213)
   Memory: 34.4M
   CGroup: /system.slice/firewalld.service
3\. Check to see which security zone is active on each network interface with the "firewall-cmd" command. I see "public" zone of security rules applied on the Ethernet interface.herong$ sudo firewall-cmd --get-active-zones

public
  interfaces: eno1
4\. Check to see what security rules are defined in the "public" zone. I see two TCP ports, 80 and 3306, are open for incoming traffic. Other ports used by "cockpit", "dhcpv6-client", and "ssh" services are also open.herong$ sudo firewall-cmd --zone=public --list-all

public (active)
  target: default
  icmp-block-inversion: no
  interfaces: eno1
  sources:
  services: cockpit dhcpv6-client ssh
  ports: 80/tcp 3306/tcp
  protocols:
  masquerade: no
  forward-ports:
  source-ports:
  icmp-blocks:
  rich rules:
5\. Add a new rule to open TCP port 8080 for Tomcat server. The first command allows all IP addresses from the Internet to access port 8080. The second command saves the change permanently.herong$ sudo firewall-cmd --zone=public --add-port=8080/tcp
herong$ sudo firewall-cmd --runtime-to-permanent
6\. Add a new rule to open all ports for a given IP address.herong$ sudo firewall-cmd --zone=public --add-source=192.168.1.11
herong$ sudo firewall-cmd --runtime-to-permanent
7\. Turn on traffic forward and a forward rule:herong$ sudo firewall-cmd --zone=external --add-masquerade
herong$ sudo firewall-cmd --zone=public --add-forward-port=port=8888:\
   proto=tcp:toport=80:toaddr=192.168.1.201
herong$ sudo firewall-cmd --runtime-to-permanent
8\. Add a pre-defined service, which contains IP ports used by the service. For example, opening "http" service is the same as opening port 80.herong$ sudo firewall-cmd --zone=public --add-service=http

herong$ sudo firewall-cmd --zone=public --list-services
cockpit dhcpv6-client http ssh

herong$ sudo firewall-cmd --runtime-to-permanent
9\. Add new rich rules, which are basically "iptable" rules.# reject incoming traffic from the guest computer
firewall-cmd --add-rich-rule="rule family='ipv4' source address='192.168.1.100' reject"

# allow my computer to access the MySQL database at port 3306
firewall-cmd --add-rich-rule='rule family="ipv4" source address="192.168.1.11" \
   port protocol="tcp" port="3306" accept'

# allow local computers to access the "http" service at port 80
firewall-cmd --add-rich-rule='rule family="ipv4" source address="192.168.1.0/24" \
  service name="http" accept'

# verify changes
firewall-cmd --zone=public --list-all
  public (active)
    target: default
    icmp-block-inversion: no
    interfaces: eno1
    sources:
    services: cockpit dhcpv6-client http ssh
    ports: 80/tcp 3306/tcp
    protocols:
    masquerade: no
    forward-ports:
    source-ports:
    icmp-blocks:
    rich rules:
    rule family="ipv4" source address="192.168.1.0/24" service name="http" accept

# save changes
firewall-cmd --runtime-to-permanent
[Linux Tutorials - Herong's Tutorial Examples](#text00002.html_a2N5)∟ [Network Connection on CentOS](#text00038.html_a2P9)∟ "nftables" and "nft" on CentOSProvides a tutorial example on how to use 'nftables' daemon and 'nft' CLI to manage network firewall on CentOS 8 systems.The best tool to manage the network firewall on CentOS systems is the "firewall-cmd" frontend tool. But if you want to use the backend tool, you can follow this tutorial to use the "nftables" daemon and "nft" command.1\. Make sure that I have the latest version of "nftables" installed with the "dnf info" command:herong$ sudo dnf info nftables

Installed Packages
Name         : nftables
Epoch        : 1
Version      : 0.9.0
Release      : 14.el8
Architecture : x86_64
Size         : 848 k
Source       : nftables-0.9.0-14.el8.src.rpm
Repository   : @System
From repo    : anaconda
Summary      : Netfilter Tables userspace utilities
URL          : http://netfilter.org/projects/nftables/
License      : GPLv2
Description  : Netfilter Tables userspace utilities.
2\. Make sure that "nftables" service is running with the "systectl status" command:herong$ sudo systemctl status nftables
nftables.service - Netfilter Tables
   Loaded: loaded (/usr/lib/systemd/system/nftables.service; disabled;
           vendor preset: disabled)
   Active: inactive (dead)
     Docs: man:nft(8)

herong$ sudo systemctl enable nftables
Created symlink /etc/systemd/system/multi-user.target.wants/nftables.service ...

herong$ sudo systemctl start nftables

herong$ sudo systemctl status nftables
nftables.service - Netfilter Tables
  Loaded: loaded (/usr/lib/systemd/system/nftables.service; enabled; ...
  Active: active (exited)
    Docs: man:nft(8)
 Process: 5226 ExecStart=/sbin/nft -f /etc/sysconfig/nftables.conf
Main PID: 5226 (code=exited, status=0/SUCCESS)
3\. List all rule tables with the "nft" command.herong$ sudo nft list tables

table ip filter
table ip6 filter
table bridge filter
table ip security
table ip raw
table ip mangle
table ip nat
table ip6 security
table ip6 raw
table ip6 mangle
table ip6 nat
table bridge nat
table inet firewalld
table ip firewalld
table ip6 firewalld
4\. List all rules in the "ip/firewalld" table with the "nft" command.herong$ sudo nft list table ip firewalld | more

table ip firewalld {
  chain nat_PREROUTING {
    type nat hook prerouting priority -90; policy accept;
    jump nat_PREROUTING_ZONES
  }

  chain nat_PREROUTING_ZONES {
    iifname "virbr0" goto nat_PRE_libvirt
    iifname "eno1" goto nat_PRE_public
    goto nat_PRE_public
  }

  chain nat_POSTROUTING {
    type nat hook postrouting priority 110; policy accept;
    jump nat_POSTROUTING_ZONES
  }

  chain nat_POSTROUTING_ZONES {
    oifname "virbr0" goto nat_POST_libvirt
    oifname "eno1" goto nat_POST_public
    goto nat_POST_public
  }

  chain nat_PRE_public {
  ...
As you can see, the syntax of firewall security rules used by "nft" is more complicated than the "firewall-cmd".[Linux Tutorials - Herong's Tutorial Examples](#text00002.html_a2N5)∟ [Network Connection on CentOS](#text00038.html_a2P9)∟ "iptables" Command on CentOSProvides a tutorial example on how to use 'iptables' daemon CLI to manage network firewall on older CentOS systems.The best tool to manage the network firewall on CentOS systems is the "firewall-cmd" frontend tool. But if you want to use the backend tool, you can follow this tutorial to use the "iptables" command.1\. Make sure that I have the latest version of "iptables" installed with the "dnf info" command:herong$ sudo dnf info iptables

Installed Packages
Name         : iptables
Version      : 1.8.2
Release      : 16.el8
Architecture : x86_64
Size         : 2.3 M
Source       : iptables-1.8.2-16.el8.src.rpm
Repository   : @System
From repo    : anaconda
Summary      : Tools for managing Linux kernel packet filtering capabilities
URL          : http://www.netfilter.org/
License      : GPLv2 and Artistic 2.0 and ISC
Description  : The iptables utility controls the network packet filtering code in the
             : Linux kernel. If you need to set up firewalls and/or IP masquerading,
             : you should either install nftables or this package.
             :
             : Note: This package contains the nftables-based variants of iptables and
             : ip6tables, which are drop-in replacements of the legacy tools.
2\. Check all chains of security rules with the "iptables" command:herong$ sudo iptables --list

Chain INPUT (policy ACCEPT)
target     prot opt source               destination
ACCEPT     udp  --  anywhere             anywhere             udp dpt:domain
ACCEPT     tcp  --  anywhere             anywhere             tcp dpt:domain
ACCEPT     udp  --  anywhere             anywhere             udp dpt:bootps
ACCEPT     tcp  --  anywhere             anywhere             tcp dpt:bootps

Chain FORWARD (policy ACCEPT)
target     prot opt source               destination
ACCEPT     all  --  anywhere             anywhere

Chain OUTPUT (policy ACCEPT)
target     prot opt source               destination
ACCEPT     udp  --  anywhere             anywhere             udp dpt:bootpc
3\. Append new rules to make my computer more secure. Remember that "iptable" rules are compared sequentially. If a match is found, it will take the action and quit.# allow to visit google.com Website
herong$ sudo iptables -A OUTPUT -p tcp -d google.com -j ACCEPT

# stop going out to any HTTP Websites
herong$ sudo iptables -A OUTPUT -p tcp --dport 80 -j DROP

# stop going out to any HTTPS Websites
herong$ sudo iptables -A OUTPUT -p tcp --dport 443 -j DROP

# allow me to come in with SSH connection from my laptop
herong$ sudo iptables -A INPUT -p tcp -s 192.168.1.11 --dport 22 -j ACCEPT

# allow local computers access the Web server
herong$ sudo iptables -A INPUT -p tcp --src-range 192.168.1.2-192.168.1.100 --dport 80 -j ACCEPT

# stop everyone to come in with SSH connection
herong$ sudo iptables -A INPUT -p tcp -s 0.0.0.0/0 --dport 22 -j DROP

# stop everyone to come in on any ports
herong$ sudo iptables -A INPUT -j DROP
4\. Save changes made in "iptables" permanently:herong$ sudo /sbin/iptables-save
Note that "iptables" daemon is running on older CentOS systems instead of "firealld". You can check its status with the "service" command:herong$ sudo service iptables status

Table: filter
Chain INPUT (policy ACCEPT)
num  target     prot opt source               destination
...

Chain FORWARD (policy ACCEPT)
num  target     prot opt source               destination
...

Chain OUTPUT (policy ACCEPT)
num  target     prot opt source               destination
...
[Linux Tutorials - Herong's Tutorial Examples](#text00002.html_a2N5)∟ [Network Connection on CentOS](#text00038.html_a2P9)∟ "nmap" - Network Mapper on CentOSProvides a tutorial example on how to install and use 'nmap' (Network Mapper), as a network exploration tool and security scanner on CentOS systems.Another useful tool is called, "nmap (Network Mapper)”, which is a network exploration tool and security scanner. Here is the full description of "nmap":Nmap (“Network Mapper”) is an open source tool for network exploration and security auditing. It was designed to rapidly scan large networks, although it works fine against single hosts. Nmap uses raw IP packets in novel ways to determine what hosts are available on the network, what services (application name and version) those hosts are offering, what operating systems (and OS versions) they are running, what type of packet filters/firewalls are in use, and dozens of other characteristics. While Nmap is commonly used for security audits, many systems and network administrators find it useful for routine tasks such as network inventory, managing service upgrade schedules, and monitoring host or service uptime.The output from Nmap is a list of scanned targets, with supplemental information on each depending on the options used. Key among that information is the “interesting ports table”. That table lists the port number and protocol, service name, and state. The state is either open, filtered, closed, or unfiltered. Open means that an application on the target machine is listening for connections/packets on that port. Filtered means that a firewall, filter, or other network obstacle is blocking the port so that Nmap cannot tell whether it is open or closed. Closed ports have no application listening on them, though they could open up at any time. Ports are classified as unfiltered when they are responsive to Nmap's probes, but Nmap cannot determine whether they are open or closed. Nmap reports the state combinations open|filtered and closed|filtered when it cannot determine which of the two states describe a port. The port table may also include software version details when version detection has been requested. When an IP protocol scan is requested (-sO), Nmap provides information on supported IP protocols rather than listening ports.In addition to the interesting ports table, Nmap can provide further information on targets, including reverse DNS names, operating system guesses, device types, and MAC addresses.Here is what I did to install and use it on my CentOS 8 computer:1\. Check the availability of "nmap":herong$ dnf info nmap

Available Packages
Name         : nmap
Epoch        : 2
Version      : 7.70
Release      : 5.el8
Architecture : x86_64
Size         : 5.8 M
Source       : nmap-7.70-5.el8.src.rpm
Repository   : AppStream
Summary      : Network exploration tool and security scanner
URL          : http://nmap.org/
License      : Nmap
Description  : Nmap is a utility for network exploration or security auditing.
               ...
2\. Install of "nmap":herong$ sudo dnf install nmap

Dependencies resolved.
...
Installed:
 nmap-2:7.70-5.el8.x86_64

Complete!
3\. Scan localhost on TCP connections:herong$ sudo nmap -sT -O localhost

Starting Nmap 7.70 ( https://nmap.org ) at 2020-03-30 08:12 EDT
Nmap scan report for localhost (127.0.0.1)
Host is up (0.00020s latency).
Other addresses for localhost (not scanned): ::1
Not shown: 995 closed ports
PORT     STATE SERVICE
22/tcp   open  ssh
80/tcp   open  http
111/tcp  open  rpcbind
631/tcp  open  ipp
3306/tcp open  mysql
Device type: general purpose
Running: Linux 3.X
OS CPE: cpe:/o:linux:linux_kernel:3
OS details: Linux 3.7 - 3.10
Network Distance: 0 hops
4\. Scan localhost on UDP connections:herong$ sudo nmap -sU -O localhost

Starting Nmap 7.70 ( https://nmap.org ) at 2020-03-30 08:13 EDT
Nmap scan report for localhost (127.0.0.1)
Host is up (0.000022s latency).
Other addresses for localhost (not scanned): ::1
Not shown: 998 closed ports
PORT     STATE         SERVICE
111/udp  open          rpcbind
5353/udp open|filtered zeroconf
Warning: OSScan results may be unreliable because we could not find
   at least 1 open and 1 closed port
Device type: remote management|phone|general purpose|webcam|storage-misc
Network Distance: 0 hops
5\. Scan a remote computer with "-A -T4" (Aggressive level 4 timing: aggressive),herong$ nmap -A -T4 192.168.1.100

Starting Nmap 7.70 ( https://nmap.org ) at 2020-03-30 07:39 EDT
Nmap scan report for 192.168.1.100
Host is up (0.00018s latency).
Not shown: 996 closed ports

PORT     STATE SERVICE VERSION
22/tcp   open  ssh     OpenSSH 8.0 (protocol 2.0)
| ssh-hostkey:
|   3072 d4:33:...:6e:29 (RSA)
|   256 77:87:...:36:6e (ECDSA)
|_  256 e5:51:...:ec:6a (ED25519)

80/tcp   open  http    Apache httpd 2.4.37 ((centos))
| http-methods:
|_  Potentially risky methods: TRACE
|_http-server-header: Apache/2.4.37 (centos)
|_http-title: ...

111/tcp  open  rpcbind 2-4 (RPC #100000)
| rpcinfo:
|   program version   port/proto  service
|   100000  2,3,4        111/tcp  rpcbind
|_  100000  2,3,4        111/udp  rpcbind

3306/tcp open  mysql?
| fingerprint-strings:
|   DNSStatusRequestTCP:
|     8.0.17
|     mysql_native_password
|     packets out of order
...

1 service unrecognized despite returning data. If you know the
service/version, please submit the following fingerprint
at https://nmap.org/cgi-bin/submit.cgi?new-service :
SF-Port3306-TCP:V=7.70%I=7%D=3/30%Time=5E81DA9C%P=x86_64-redhat-linux-gnu%
...

Service detection performed.
Nmap done: 1 IP address (1 host up) scanned in 27.99 seconds
[Linux Tutorials - Herong's Tutorial Examples](#text00002.html_a2N5)∟ [Network Connection on CentOS](#text00038.html_a2P9)∟ Monitor Network Services on CentOSProvides a tutorial example on how to use different tools, netstat (Network Status), lsof (List of Open Files), ss (Socket Statistics), to monitor network services on CentOS systems.With network firewall configured, the next task is to monitor network services. Here are the tools you can use on CentOS 8 systems:1\. /etc/services - Network service list file which contains service names and their default IP ports.herong$ sudo cat /etc/services | more

# Network services, Internet style
# IANA services version: last updated 2016-07-08
# The Well Known Ports are those from 0 through 1023.
# The Registered Ports are those from 1024 through 49151
# The Dynamic and/or Private Ports are those from 49152 through 65535

tcpmux          1/tcp                           # TCP port service multiplexer
tcpmux          1/udp                           # TCP port service multiplexer
rje             5/tcp                           # Remote Job Entry
rje             5/udp                           # Remote Job Entry
echo            7/tcp
echo            7/udp
discard         9/tcp           sink null
discard         9/udp           sink null
systat          11/tcp          users
systat          11/udp          users
daytime         13/tcp
daytime         13/udp
qotd            17/tcp          quote
qotd            17/udp          quote
chargen         19/tcp          ttytst source
chargen         19/udp          ttytst source
ftp-data        20/tcp
ftp-data        20/udp
ftp             21/tcp
ftp             21/udp          fsp fspd
ssh             22/tcp                          # The Secure Shell (SSH) Protocol
ssh             22/udp                          # The Secure Shell (SSH) Protocol
telnet          23/tcp
telnet          23/udp
...
2\. List currently active Internet connections with the "netstat (Network Status)" command:herong$ netstat -atu

Active Internet connections (servers and established)
Proto Recv-Q Send-Q Local Address           Foreign Address         State
tcp        0      0 0.0.0.0:sunrpc          0.0.0.0:*               LISTEN
tcp        0      0 localhost.locald:domain 0.0.0.0:*               LISTEN
tcp        0      0 0.0.0.0:ssh             0.0.0.0:*               LISTEN
tcp        0      0 localhost:ipp           0.0.0.0:*               LISTEN
tcp        0    208 localhost.localdoma:ssh 192.168.1.11:49256      ESTABLISHED
tcp        0      0 localhost.localdoma:ssh 192.168.1.11:49600      ESTABLISHED
tcp6       0      0 [::]:sunrpc             [::]:*                  LISTEN
tcp6       0      0 [::]:http               [::]:*                  LISTEN
tcp6       0      0 [::]:ssh                [::]:*                  LISTEN
tcp6       0      0 localhost:ipp           [::]:*                  LISTEN
tcp6       0      0 [::]:mysqlx             [::]:*                  LISTEN
tcp6       0      0 [::]:mysql              [::]:*                  LISTEN
udp        0      0 localhost.locald:domain 0.0.0.0:*
udp        0      0 0.0.0.0:bootps          0.0.0.0:*
udp        0      0 localhost.locald:bootpc 0.0.0.0:*
udp        0      0 0.0.0.0:sunrpc          0.0.0.0:*
udp        0      0 0.0.0.0:37044           0.0.0.0:*
udp        0      0 localhost:323           0.0.0.0:*
udp        0      0 0.0.0.0:mdns            0.0.0.0:*
udp6       0      0 [::]:sunrpc             [::]:*
udp6       0      0 localhost:323           [::]:*
udp6       0      0 [::]:45574              [::]:*
udp6       0      0 [::]:mdns               [::]:*
3\. List Of Open Files (lsof) related to IP connections with the "lsof" command:herong$ sudo lsof -i

COMMAND     PID    USER   FD   TYPE  DEVICE NODE NAME
systemd       1    root  436u  IPv4   16254  TCP *:sunrpc (LISTEN)
systemd       1    root  437u  IPv4   16255  UDP *:sunrpc
systemd       1    root  438u  IPv6   16256  TCP *:sunrpc (LISTEN)
systemd       1    root  439u  IPv6   16257  UDP *:sunrpc
rpcbind    1206     rpc    4u  IPv4   16254  TCP *:sunrpc (LISTEN)
rpcbind    1206     rpc    5u  IPv4   16255  UDP *:sunrpc
rpcbind    1206     rpc    6u  IPv6   16256  TCP *:sunrpc (LISTEN)
rpcbind    1206     rpc    7u  IPv6   16257  UDP *:sunrpc
avahi-dae  1248   avahi   12u  IPv4   29292  UDP *:mdns
avahi-dae  1248   avahi   13u  IPv6   29293  UDP *:mdns
avahi-dae  1248   avahi   14u  IPv4   29294  UDP *:37044
avahi-dae  1248   avahi   15u  IPv6   29295  UDP *:45574
chronyd    1251  chrony    5u  IPv4   26492  UDP localhost:323
chronyd    1251  chrony    6u  IPv6   26493  UDP localhost:323
NetworkMa  1451    root   22u  IPv4  994410  UDP localhost.localdomain:bootpc
sshd       1483    root    5u  IPv4   32847  TCP *:ssh (LISTEN)
sshd       1483    root    7u  IPv6   32849  TCP *:ssh (LISTEN)
dnsmasq    2174 dnsmasq    3u  IPv4   34607  UDP *:bootps
dnsmasq    2174 dnsmasq    5u  IPv4   34610  UDP localhost.localdomain:domain
dnsmasq    2174 dnsmasq    6u  IPv4   34611  TCP localhost.localdomain:domain (LISTEN)
sshd       2941    root    5u  IPv4 1007861  TCP localhost.localdomain:ssh
                                                 ->192.168.1.11:49600 (ESTABLISHED)
sshd       2945  herong    5u  IPv4 1007861  TCP localhost.localdomain:ssh
                                                 ->192.168.1.11:49600 (ESTABLISHED)
mysqld     3392   mysql   32u  IPv6  557420  TCP *:mysql (LISTEN)
mysqld     3392   mysql   34u  IPv6  556565  TCP *:mysqlx (LISTEN)
cupsd      6882    root    9u  IPv6   59565  TCP localhost:ipp (LISTEN)
cupsd      6882    root   10u  IPv4   59566  TCP localhost:ipp (LISTEN)
httpd     14246  apache    4u  IPv6  291420  TCP *:http (LISTEN)
httpd     14247  apache    4u  IPv6  291420  TCP *:http (LISTEN)
httpd     14248  apache    4u  IPv6  291420  TCP *:http (LISTEN)
httpd     19007    root    4u  IPv6  291420  TCP *:http (LISTEN)
4\. Dump socket statistics with the "ss" command:herong$ sudo ss -lntu

Netid State  Recv-Q Send-Q     Local Address:Port  Peer Address:Port
udp   UNCONN 0      0          192.168.122.1:53         0.0.0.0:*
udp   UNCONN 0      0         0.0.0.0%virbr0:67         0.0.0.0:*
udp   UNCONN 0      0     192.168.1.100%eno1:68         0.0.0.0:*
udp   UNCONN 0      0                0.0.0.0:111        0.0.0.0:*
udp   UNCONN 0      0                0.0.0.0:37044      0.0.0.0:*
udp   UNCONN 0      0              127.0.0.1:323        0.0.0.0:*
udp   UNCONN 0      0                0.0.0.0:5353       0.0.0.0:*
udp   UNCONN 0      0                   [::]:111         [::]:*
udp   UNCONN 0      0                  [::1]:323         [::]:*
udp   UNCONN 0      0                   [::]:45574       [::]:*
udp   UNCONN 0      0                   [::]:5353        [::]:*
tcp   LISTEN 0      128              0.0.0.0:111        0.0.0.0:*
tcp   LISTEN 0      32         192.168.122.1:53         0.0.0.0:*
tcp   LISTEN 0      128              0.0.0.0:22         0.0.0.0:*
tcp   LISTEN 0      5              127.0.0.1:631        0.0.0.0:*
tcp   LISTEN 0      128                 [::]:111         [::]:*
tcp   LISTEN 0      128                    *:80             *:*
tcp   LISTEN 0      128                 [::]:22          [::]:*
tcp   LISTEN 0      5                  [::1]:631         [::]:*
tcp   LISTEN 0      70                     *:33060          *:*
tcp   LISTEN 0      128                    *:3306           *:*
[Linux Tutorials - Herong's Tutorial Examples](#text00002.html_a2N5)∟ Software Package Manager on CentOS - DNF and YUMProvides introductions and tutorial examples about Software Package Manager on CentOS systems. Topics include introductions of DNF (Dandified YUM) and YUM (Yellowdog Update Modified); installing Java.[What Is DNF](#text00047.html_a2PJ)[What Is YUM](#text00048.html_a2PK)[Install and Manage Java Packages on CentOS](#text00049.html_a2PM)[Install and Manage Perl Packages on CentOS](#text00050.html_a2PN)[Install "git-core" for GitHub Packages on CentOS](#text00051.html_a2PP)Takeaways:

*   DNF, also called Dandified YUM, is the next generation of YUM (Yellowdog Update Modified) software package manager for RPM (RedHat Package Manager) based Linux distributions.
*   YUM (Yellowdog Update Modified) is a software package manager for RPM (RedHat Package Manager) based Linux distributions.
*   You can use "dnf search keyword" to search for packages with a given keyword.
*   You can use "sudo dnf install package_name" to install a software package.

[Linux Tutorials - Herong's Tutorial Examples](#text00002.html_a2N5)∟ [Software Package Manager on CentOS - DNF and YUM](#text00046.html_a2PH)∟ What Is DNFProvides a quick introduction on DNF (also called Dandified YUM), which is the next generation of YUM (Yellowdog Update Modified) software package manager for RPM (RedHat Package Manager) based Linux distributions.What Is DNF? - DNF, also called Dandified YUM, is the next generation of YUM (Yellowdog Update Modified) software package manager for RPM (RedHat Package Manager) based Linux distributions.Here is the description of DNF from its manual page: "DNF is the next upcoming major version of YUM, a package manager for RPM-based Linux distributions. It roughly maintains CLI compatibility with YUM and defines a strict API for extensions and plugins."You can get a list of main DNF commands by running "dnf help" on CentOS 8:herong$ dnf help

usage: dnf [options] COMMAND

List of Main Commands:
alias               List or create command aliases
autoremove          remove all unneeded packages that were originally
                    installed as dependencies
check               check for problems in the packagedb
check-update        check for available package upgrades
clean               remove cached data
deplist             List package's dependencies and what packages provide
                    them
distro-sync         synchronize installed packages to the latest available
                    versions
downgrade           Downgrade a package
group               display, or use, the groups information
help                display a helpful usage message
history             display, or use, the transaction history
info                display details about a package or group of packages
install             install a package or packages on your system
list                list a package or groups of packages
makecache           generate the metadata cache
mark                mark or unmark installed packages as installed by user.
module              Interact with Modules.
provides            find what package provides the given value
reinstall           reinstall a package
remove              remove a package or packages from your system
repolist            display the configured software repositories
repoquery           search for packages matching keyword
repository-packages run commands on top of all packages in given repository
search              search package details for the given string
shell               run an interactive DNF shell
swap                run an interactive dnf mod for remove and install one
                    spec
updateinfo          display advisories about packages
upgrade             upgrade a package or packages on your system
upgrade-minimal     upgrade, but only 'newest' package match which fixes
                    a problem that affects your system
[Linux Tutorials - Herong's Tutorial Examples](#text00002.html_a2N5)∟ [Software Package Manager on CentOS - DNF and YUM](#text00046.html_a2PH)∟ What Is YUMProvides a quick introduction on YUM (Yellowdog Update Modified), which is a software package manager for RPM (RedHat Package Manager) based Linux distributions.What Is YUM? - YUM (Yellowdog Update Modified) is a software package manager for RPM (RedHat Package Manager) based Linux distributions.YUM is replaced by DNF (Dandified YUM) on CentOS 8 systems now. If run a "yum ..." command, it will be executed as "dnf ...".For example, if you want the "make" tool package information, you can get the same result with both "dnf info make" and "yum info make" commands:herong$ dnf info make
Available Packages
Name         : make
Epoch        : 1
Version      : 4.2.1
Release      : 9.el8
Architecture : x86_64
Size         : 498 k
Source       : make-4.2.1-9.el8.src.rpm
Repository   : BaseOS
Summary      : A GNU tool which simplifies the build process for users
URL          : http://www.gnu.org/software/make/
License      : GPLv3+
Description  : A GNU tool for controlling the generation of executables and other
             : non-source files of a program from the program's source files. Make
             : allows users to build and install packages without any significant
             : knowledge about the details of the build process. The details about
             : how the program should be built are provided for make in the program's
             : makefile.

herong$ yum info make
Available Packages
Name         : make
Epoch        : 1
Version      : 4.2.1
Release      : 9.el8
Architecture : x86_64
Size         : 498 k
Source       : make-4.2.1-9.el8.src.rpm
Repository   : BaseOS
Summary      : A GNU tool which simplifies the build process for users
URL          : http://www.gnu.org/software/make/
License      : GPLv3+
Description  : A GNU tool for controlling the generation of executables and other
             : non-source files of a program from the program's source files. Make
             : allows users to build and install packages without any significant
             : knowledge about the details of the build process. The details about
             : how the program should be built are provided for make in the program's
             : makefile.
So you should stop using YUM and get used to DNF. YUM will probably be removed in the next CentOS release.[Linux Tutorials - Herong's Tutorial Examples](#text00002.html_a2N5)∟ [Software Package Manager on CentOS - DNF and YUM](#text00046.html_a2PH)∟ Install and Manage Java Packages on CentOSProvides a tutorial example on how to install OpenJDK 11 JRE (Java Runtime Environment) on CentOS 8 systems using 'dnf/yum' as the package manager.If you want to run Java applications on CentOS Linux systems, you can follow what I did on my CentOS 8 computer:1\. Login as "herong", who has admin privileges.2\. Run "dnf search" to find available Java packages. I see OpenJDK 1.8 and OpenJDK 11 packages available for installation:herong$ dnf search java

java-11-openjdk.x86_64 : OpenJDK Runtime Environment 11
java-11-openjdk-src.x86_64 : OpenJDK Source Bundle 11
java-11-openjdk-demo.x86_64 : OpenJDK Demos 11
java-11-openjdk-devel.x86_64 : OpenJDK Development Environment 11
java-11-openjdk-jmods.x86_64 : JMods for OpenJDK 11
java-1.8.0-openjdk.x86_64 : OpenJDK Runtime Environment 8
java-1.8.0-openjdk-src.x86_64 : OpenJDK Source Bundle 8
java-1.8.0-openjdk-demo.x86_64 : OpenJDK Demos 8
java-1.8.0-openjdk-devel.x86_64 : OpenJDK Development Environment 8
java-1.8.0-openjdk-javadoc.noarch : OpenJDK 8 API documentation
java-1.8.0-openjdk-headless.x86_64 : OpenJDK Headless Runtime Environment 8
...
3\. Install the OpenJDK 11 JRE (Java Runtime Environment):herong$ sudo dnf install java-11-openjdk

Dependencies resolved.
 Package                    Architecture  Version
============================================================
Installing:
 java-11-openjdk            x86_64        1:11.0.6.10-0.el8_1
Installing dependencies:
 copy-jdk-configs           noarch        3.7-1.el8
 java-11-openjdk-headless   x86_64        1:11.0.6.10-0.el8_1
 javapackages-filesystem    noarch        5.3.0-1.module_el8.0.0+11...
 ttmkfdir                   x86_64        3.0.9-54.el8
 tzdata-java                noarch        2019c-1.el8
 xorg-x11-fonts-Type1       noarch        7.5-19.el8
 lksctp-tools               x86_64        1.0.18-3.el8
Enabling module streams:
 javapackages-runtime                     201801

...
Installed:
  java-11-openjdk-1:11.0.6.10-0.el8_1.x86_64
  copy-jdk-configs-3.7-1.el8.noarch
  java-11-openjdk-headless-1:11.0.6.10-0.el8_1.x86_64
  javapackages-filesystem-5.3.0-1.module_el8.0.0
  ttmkfdir-3.0.9-54.el8.x86_64
  tzdata-java-2019c-1.el8.noarch
  xorg-x11-fonts-Type1-7.5-19.el8.noarch
  lksctp-tools-1.0.18-3.el8.x86_64

Complete!
3\. Verify OpenJDK 11 JRE (Java Runtime Environment):herong$ java -version

openjdk version "11.0.6" 2020-01-14 LTS
OpenJDK Runtime Environment 18.9 (build 11.0.6+10-LTS)
OpenJDK 64-Bit Server VM 18.9 (build 11.0.6+10-LTS, mixed mode, sharing)
Cool! I have installed OpenJDK 11 JRE on my CentOS computer without any issues.[Linux Tutorials - Herong's Tutorial Examples](#text00002.html_a2N5)∟ [Software Package Manager on CentOS - DNF and YUM](#text00046.html_a2PH)∟ Install and Manage Perl Packages on CentOSProvides a tutorial example on how to install Perl 5.26 on CentOS 8 systems using 'dnf/yum' as the package manager.The Perl (Practical Extraction and Report Language) script engine is included as part of the CentOS 8 system by default. You don't need to install it yourself. But you can still install its additional modules using the "dnf" package manager.1\. Login as "herong", who has admin privileges.2\. Check the current installed version of Perl:herong$ perl -v

This is perl 5, version 26, subversion 3 (v5.26.3) built for
x86_64-linux-thread-multi (with 51 registered patches, ...)
...
3\. Run "dnf info perl" to see Perl package information:herong$ dnf info perl

Available Packages
Name         : perl
Epoch        : 4
Version      : 5.26.3
Release      : 416.el8
Architecture : x86_64
Size         : 72 k
Source       : perl-5.26.3-416.el8.src.rpm
Repository   : AppStream
Summary      : Practical Extraction and Report Language
URL          : http://www.perl.org/
License      : GPL+ or Artistic
Description  : Perl is a high-level programming language with roots in C, sed, awk and shell
             : scripting. Perl is good at handling processes and files, and is especially
             : good at handling text. Perl's hallmarks are practicality and efficiency.
             : While it is used to do a lot of different things, Perl's most common
             : applications are system administration utilities and web programming.
             :
             : This is a metapackage with all the Perl bits and core modules that can be
             : found in the upstream tarball from perl.org.
             :
             : If you need only a specific feature, you can install a specific package
             : instead. E.g. to handle Perl scripts with /usr/bin/perl interpreter,
             : install perl-interpreter package. See perl-interpreter description for more
             : details on the Perl decomposition into packages.
4\. Install the "perl" package:herong$ sudo dnf install perl

...
Installed:
  perl-4:5.26.3-416.el8.x86_64
  perl-Encode-Locale-1.05-9.el8.noarch
  perl-TermReadKey-2.37-7.el8.x86_64
  dwz-0.12-9.el8.x86_64
  efi-srpm-macros-3-2.el8.noarch
  ghc-srpm-macros-1.4.2-7.el8.noarch
  go-srpm-macros-2-16.el8.noarch
  ocaml-srpm-macros-5-4.el8.noarch
  openblas-srpm-macros-2-2.el8.noarch
  perl-Algorithm-Diff-1.1903-9.el8.noarch
  perl-Archive-Tar-2.30-1.el8.noarch
  perl-Archive-Zip-1.60-3.el8.noarch
  perl-Attribute-Handlers-0.99-416.el8.noarch
  perl-B-Debug-1.26-2.el8.noarch
  perl-CPAN-2.18-397.el8.noarch
  perl-CPAN-Meta-2.150010-396.el8.noarch
  perl-CPAN-Meta-Requirements-2.140-396.el8.noarch
  perl-CPAN-Meta-YAML-0.018-397.el8.noarch
  perl-Compress-Bzip2-2.26-6.el8.x86_64
  perl-Compress-Raw-Bzip2-2.081-1.el8.x86_64
  perl-Compress-Raw-Zlib-2.081-1.el8.x86_64
  perl-Config-Perl-V-0.30-1.el8.noarch
  perl-DB_File-1.842-1.el8.x86_64
  perl-Data-OptList-0.110-6.el8.noarch
  perl-Data-Section-0.200007-3.el8.noarch
  perl-Devel-PPPort-3.36-5.el8.x86_64
  perl-Devel-Peek-1.26-416.el8.x86_64
  perl-Devel-SelfStubber-1.06-416.el8.noarch
  perl-Devel-Size-0.81-2.el8.x86_64
  perl-Digest-SHA-1:6.02-1.el8.x86_64
  perl-Encode-devel-4:2.97-3.el8.x86_64
  perl-Env-1.04-395.el8.noarch
   ...

Complete!
5\. Verify the installed Perl package:herong$ perl -v

This is perl 5, version 26, subversion 3 (v5.26.3) built for
x86_64-linux-thread-multi (with 51 registered patches, ...)
...
Ok. The installed Perl package is the same version as the pre-installed Perl in the CentOS system.[Linux Tutorials - Herong's Tutorial Examples](#text00002.html_a2N5)∟ [Software Package Manager on CentOS - DNF and YUM](#text00046.html_a2PH)∟ Install "git-core" for GitHub Packages on CentOSProvides a tutorial example on how to install 'git-core' on CentOS 8 systems for managing GitHub packages.If you are download packages from GitHub repository frequently, you should install "git" tools on your Linux computer. There are a number "git" tools available. But "git-core" with minimal functionality and dependencies is good enough for beginners.1\. Run "dnf info git-core" to see package information:herong$ sudo dnf info git-core

Name         : git-core
Version      : 2.18.4
Release      : 2.el8_2
Architecture : x86_64
Size         : 4.0 M
Source       : git-2.18.4-2.el8_2.src.rpm
Repository   : AppStream
Summary      : Core package of git with minimal functionality
URL          : https://git-scm.com/
License      : GPLv2
Description  : Git is a fast, scalable, distributed revision control system with an
             : unusually rich command set that provides both high-level operations
             : and full access to internals.
             :
             : The git-core rpm installs really the core tools with minimal
             : dependencies. Install git package for common set of tools.
             : To install all git packages, including tools for integrating with
             : other SCMs, install the git-all meta-package.
2\. Install "git-core":herong$ sudo dnf install git-core

Installed:
  git-core-2.18.4-2.el8_2.x86_64

herong$ git version
git version 2.18.4
3\. Try it to clone the "git" package itself:herong$ git clone https://github.com/git/git
Cloning into 'git'...
remote: Enumerating objects: 291689, done.
Receiving objects:   9% (26899/291689), ...
[Linux Tutorials - Herong's Tutorial Examples](#text00002.html_a2N5)∟ Running Apache Web Server (httpd) on Linux SystemsProvides introductions and tutorial on Apache Web server (httpd) on Linux systems. Topics include installing Apache web server (httpd).[Verify Apache Web Server "httpd"](#text00053.html_a2PS)Takeaways:

*   The Apache Web server, httpd, is included as part of the CentOS 8 system by default.

[Linux Tutorials - Herong's Tutorial Examples](#text00002.html_a2N5)∟ [Running Apache Web Server (httpd) on Linux Systems](#text00052.html_a2PR)∟ Verify Apache Web Server "httpd"Provides a tutorial example on how to manage Apache Web Server 'httpd' on CentOS 8 systems, and how to publish HTML documents and PHP scripts..The Apache Web server, httpd, is included as part of the CentOS 8 system by default. You don't need to install it yourself. But you need to follow this tutorial to learn how to manage it.1\. Check Apache Web server, httpd, package status. I see "httpd 2.4" installed.herong$ dnf info httpd

Installed Packages
Name         : httpd
Version      : 2.4.37
Release      : 16.module_el8.1.0+256+ae790463
Architecture : x86_64
Size         : 5.4 M
Source       : httpd-2.4.37-16.module_el8.1.0+256+ae790463.src.rpm
Repository   : @System
From repo    : AppStream
Summary      : Apache HTTP Server
URL          : https://httpd.apache.org/
License      : ASL 2.0
Description  : The Apache HTTP Server is a powerful, efficient, and
             : extensible web server.
2\. Check Apache Web server, httpd, running status:herong$ sudo systemctl status httpd

- httpd.service - The Apache HTTP Server
   Loaded: loaded (/usr/lib/systemd/system/httpd.service; disabled; ...
  Drop-In: /usr/lib/systemd/system/httpd.service.d
           |-php-fpm.conf
   Active: active (running) since Sat 2020-03-28 22:06:40 EDT; 3min ...
     Docs: man:httpd.service(8)
 Main PID: 19007 (httpd)
   Status: "Total requests: 8; Idle/Busy workers 100/0;Requests/sec: ...
    Tasks: 213 (limit: 26213)
   Memory: 44.2M
   CGroup: /system.slice/httpd.service
...
3\. Check default Web page from the Web server:herong$ curl http://localhost

...
<?xml version="1.0" encoding="utf-8"?>
<!DOCTYPE HTML>
<html lang="en">
...
3\. Check Web server access log:herong$ sudo tail /var/log/httpd/access_log

... "GET / HTTP/1.1" 403 4006 "-" "curl/7.61.1"
... "GET / HTTP/1.1" 403 4288 "-" "Mozilla/5.0 (X11; Linux x86_64; ...
... "GET /noindex/common/css/bootstrap.min.css HTTP/1.1" 200 99548 ...
... "GET /noindex/common/css/styles.css HTTP/1.1" 200 71634 ...
... "GET /noindex/common/images/pb-centos.png HTTP/1.1" 200 13122 ...
... "GET /noindex/common/images/pb-apache.png HTTP/1.1" 200 103267 ...
... "GET /noindex/common/images/centos-header.png HTTP/1.1" 200 28888 ...
4\. Publish an HTML document:herong$ ls -l /var/www/html/test.html
-rw-r--r--. 1 root root 50 Mar 26 22:21 /var/www/html/test.html

herong$ cat /var/www/html/test.html
<html>
<body>
<p>Hello world!</p>
</body>
</html>

herong$ curl http://localhost/test.html
<html>
<body>
<p>Hello world!</p>
</body>
</html>
Cool. I am able to publish HTML documents to the Apache Web server, "httpd". Here are some additional information about "httpd":All Apache configuration files are located in the /etc/httpd directory.

The main Apache configuration file is /etc/httpd/conf/httpd.conf.

Configuration files ending with .conf located in the /etc/httpd/conf.d
directory are included in main Apache configuration file.

Configuration files that are responsible for loading various Apache
modules are located in the /etc/httpd/conf.modules.d directory.

Apache vhost files must end with .conf and be stored in /etc/httpd/conf.d
directory. You can have as many vhosts as you need. Creating a separate
configuration file (vhost) for each domain makes the server
easier to maintain.

Apache log files (access_log and error_log) are located in the
/var/log/httpd/ directory.

You can set your domain document root directory to any location you want.
The most common locations for webroot include:
  /home/<user_name>/<site_name>
  /var/www/<site_name>
  /var/www/html/<site_name>
  /opt/<site_name>
[Linux Tutorials - Herong's Tutorial Examples](#text00002.html_a2N5)∟ Running PHP Scripts on Linux SystemsProvides introductions and tutorial examples about running PHP scripts on Linux systems. Topics include installing PHP engine on CentOS Linux systems; installing missing PHP modules; dumping PHP environment info; 'include' statements.[Install and Manage PHP Packages on CentOS](#text00055.html_a2PU)["php -i" - Dump PHP Environment Information](#text00056.html_a2PV)[Install and Manage PHP Modules on CentOS](#text00057.html_a2PW)[Files Used in PHP "include" Statements](#text00058.html_a2PX)[Publish PHP Scripts on Apache Web Server](#text00059.html_a2PY)[Dump PHP/Apache Environment Information](#text00060.html_a2PZ)[Apache PHP file_put_contents() Permission Denied](#text00061.html_a2R0)[SELinux Security Context on /var/www/html](#text00062.html_a2R1)[Migrate Old Scripts to New PHP Release](#text00063.html_a2R2)Takeaways:

*   Installing the PHP engine can be done using the "dnf install php" command on CentOS systems.
*   Dumping PHP environment information can be done by using the "php -i" command.
*   Missing PHP modules can be installed using additional "dnf install ..." commands.
*   "include" statement with no file path searches 3 places for the included file.

[Linux Tutorials - Herong's Tutorial Examples](#text00002.html_a2N5)∟ [Running PHP Scripts on Linux Systems](#text00054.html_a2PT)∟ Install and Manage PHP Packages on CentOSProvides a tutorial example on how to install PHP 7.2 on CentOS 8 systems using 'dnf/yum' as the package manager.If you want to run PHP scripts on CentOS Linux systems, you can follow what I did on my CentOS 8 computer:1\. Login as "herong", who has admin privileges.2\. Run "dnf search" to find available PHP packages. I see "php" and some PHP modules available for installation:herong$ dnf search php

php.x86_64 : PHP scripting language for creating dynamic web sites
php-common.x86_64 : Common files for PHP
php-fpm.x86_64 : PHP FastCGI Process Manager
php-dbg.x86_64 : The interactive PHP debugger
php-cli.x86_64 : Command-line interface for PHP
php-xml.x86_64 : A module for PHP applications which use XML
php-json.x86_64 : JavaScript Object Notation extension for PHP
...
3\. Install the "php" package:herong$ sudo dnf install php

 Package                      Architecture     Version
========================================================================
Installing:
 php                          x86_64           7.2.11-2.module_el8.1.0
Installing dependencies:
 apr                          x86_64           1.6.3-9.el8
 apr-util                     x86_64           1.6.1-6.el8
 centos-logos-httpd           noarch           80.5-2.el8
 httpd                        x86_64           2.4.37-16.module_el8.1.0
 httpd-filesystem             noarch           2.4.37-16.module_el8.1.0
 httpd-tools                  x86_64           2.4.37-16.module_el8.1.0
 mod_http2                    x86_64           1.11.3-3.module_el8.1.0
 nginx-filesystem             noarch           1:1.14.1-9.module_el8.0.0
 php-cli                      x86_64           7.2.11-2.module_el8.1.0
 php-common                   x86_64           7.2.11-2.module_el8.1.0
Installing weak dependencies:
 apr-util-bdb                 x86_64           1.6.1-6.el8
 apr-util-openssl             x86_64           1.6.1-6.el8
 php-fpm                      x86_64           7.2.11-2.module_el8.1.0
Enabling module streams:
 httpd                                         2.4
 nginx                                         1.14
 php                                           7.2

...
Installed:
  php-7.2.11-2.module_el8.1.0
  apr-util-bdb-1.6.1-6.el8.x86_64
  apr-util-openssl-1.6.1-6.el8.x86_64
  php-fpm-7.2.11-2.module_el8.1.0
  apr-1.6.3-9.el8.x86_64
  apr-util-1.6.1-6.el8.x86_64
  centos-logos-httpd-80.5-2.el8.noarch
  httpd-2.4.37-16.module_el8.1.0
  httpd-filesystem-2.4.37-16.module_el8.1.0
  httpd-tools-2.4.37-16.module_el8.1.0
  mod_http2-1.11.3-3.module_el8.1.0
  nginx-filesystem-1:1.14.1-9.module_el8.0.0+184+e34fea82.noarch
  php-cli-7.2.11-2.module_el8.1.0
  php-common-7.2.11-2.module_el8.1.0

Complete!
3\. Verify the "php" package:herong$ php -version

PHP 7.2.11 (cli) (built: Oct  9 2018 15:09:36) ( NTS )
Copyright (c) 1997-2018 The PHP Group
Zend Engine v3.2.0, Copyright (c) 1998-2018 Zend Technologies
Cool! I have installed the "php" 7.2 package on my CentOS computer without any issues.[Linux Tutorials - Herong's Tutorial Examples](#text00002.html_a2N5)∟ [Running PHP Scripts on Linux Systems](#text00054.html_a2PT)∟ "php -i" - Dump PHP Environment InformationProvides a tutorial example on how to dump PHP environment information using the 'php -i' command. The output tells me where to go find different types of PHP program files.The first thing you should do after installing the PHP package is probably to dump the PHP environment information using the "php -i" command, which actually calls the built-in phpinfo() function to do the job. Here is what I got on my CentOS 8 computer.herong$ php -i

phpinfo()
PHP Version => 7.2.11

System => Linux 4.18.0-147.el8.x86_64 #1 SMP Wed Dec 4 21:51:45 UTC 2019
Build Date => Oct  9 2018 15:09:36
Server API => Command Line Interface
Virtual Directory Support => disabled
Configuration File (php.ini) Path => /etc
Loaded Configuration File => /etc/php.ini
Scan this dir for additional .ini files => /etc/php.d
Additional .ini files parsed => /etc/php.d/20-bz2.ini,
/etc/php.d/20-calendar.ini,
/etc/php.d/20-ctype.ini,
/etc/php.d/20-curl.ini,
/etc/php.d/20-exif.ini,
/etc/php.d/20-fileinfo.ini,
/etc/php.d/20-ftp.ini,
...

Core
PHP Version => 7.2.11
Directive => Local Value => Master Value
allow_url_fopen => On => On
allow_url_include => Off => Off
...
error_log => no value => no value
extension_dir => /usr/lib64/php/modules => /usr/lib64/php/modules

...
Now I know where to go find different types PHP program files:centos$ which php
/usr/bin/php

centos$ ls -l /usr/bin/php
-rwxr-xr-x. 1 root root 5888640 Nov 13 23:09 /usr/bin/php

centos$ ls -l /etc/php.ini
-rw-r--r--. 1 root root 62221 Nov 13 23:09 /etc/php.ini

centos$ ls -l /etc/php.d
total 80
-rw-r--r--. 1 root root 44 Nov 13 23:09 20-bz2.ini
-rw-r--r--. 1 root root 54 Nov 13 23:09 20-calendar.ini
-rw-r--r--. 1 root root 48 Nov 13 23:09 20-ctype.ini
-rw-r--r--. 1 root root 46 Nov 13 23:09 20-curl.ini
...

centos$ ls -l /usr/lib64/php/modules/
total 8744
-rwxr-xr-x. 1 root root   34104 Nov 13 23:09 bz2.so
-rwxr-xr-x. 1 root root   55304 Nov 13 23:09 calendar.so
-rwxr-xr-x. 1 root root   18736 Nov 13 23:09 ctype.so
-rwxr-xr-x. 1 root root  113680 Nov 13 23:09 curl.so
...
[Linux Tutorials - Herong's Tutorial Examples](#text00002.html_a2N5)∟ [Running PHP Scripts on Linux Systems](#text00054.html_a2PT)∟ Install and Manage PHP Modules on CentOSProvides a tutorial example on how to search and install additional PHP modules on CentOS 8 systems using 'dnf/yum' as the package manager.If you are developing a Web application using PHP scripts, you may need to install additional PHP modules as shown in this tutorial.1\. Install php-json package, if you see the "Call to undefined function json_decode()" error:herong$ test-script.php
Call to undefined function json_decode()

herong$ sudo yum search php | grep json
php-json.x86_64 : JavaScript Object Notation extension for PHP
...

herong$ sudo dnf install php-json
...
Installed:
  php-json-7.2.11-2.module_el8.1.0+209+03b9a8ff.x86_64

Complete!
2\. Install php-mbstring package, if you see the "Call to undefined function mb_internal_encoding()" error:herong$ test-script.php
Call to undefined function mb_internal_encoding()

herong$ sudo yum search php | grep mb
php-embedded.x86_64 : PHP library for embedding in applications
php-mbstring.x86_64 : A module for PHP applications which need
   multi-byte string

herong$ sudo dnf install php-mbstring
...
Installed:
  php-mbstring-7.2.11-2.module_el8.1.0+209+03b9a8ff.x86_64

Complete!
3\. Install php-mysqlnd package, if you see the "Call to undefined function mysqli_connect()" error:herong$ test-script.php
Call to undefined function mysqli_connect

herong$ sudo yum search php | grep mysql
php-mysqlnd.x86_64 : A module for PHP applications that use MySQL databases

herong$ sudo dnf install php-mysqlnd

Installed:
  php-mysqlnd-7.2.11-2.module_el8.1.0+209+03b9a8ff.x86_64
  php-pdo-7.2.11-2.module_el8.1.0+209+03b9a8ff.x86_64

Complete!
If you see more errors on undefined functions, you can continue to search and install additional PHP modules with the "yum" command.[Linux Tutorials - Herong's Tutorial Examples](#text00002.html_a2N5)∟ [Running PHP Scripts on Linux Systems](#text00054.html_a2PT)∟ Files Used in PHP "include" StatementsProvides a tutorial example on how to the PHP engine search for files given in the 'include' statements.When you use the "include" statement to execute script stored in a separate file, the PHP engine uses the following rules to search and find the script file.1\. If an absolute path is given together with the file name, the PHP engine will search for the file in the directory of the given absolute path only. For example, the following code will search for include_extra.php in /usr/share/php directory only.<?php
  include "/usr/share/php/include_extra.php";  
?>
2\. If a relative path is given together with the file name, the PHP engine will search for the file in the directory of the given path relative to the current working directory, which may not be the same as the directory of the calling script is located. For example, the following code will search for include_extra.php in the same directory where the code is executed.<?php
  include "./include_extra.php";  
?>
3\. If no path is given together with the file name, the PHP engine will search for the file in the following 3 locations sequentially:

*   Directories specified in the "include_path".
*   Directory where the calling script is located.
*   The current working directory.

For example, the following code will search for include_extra.php in multiple places.  
<?php
  include "include_extra.php";  
?>
So the best way to use the "include" statement is to give the file name only and make sure the included files are stored in one of the "include_path" directory.[Linux Tutorials - Herong's Tutorial Examples](#text00002.html_a2N5)∟ [Running PHP Scripts on Linux Systems](#text00054.html_a2PT)∟ Publish PHP Scripts on Apache Web ServerProvides a tutorial example on how to publish PHP scripts on Apache Web Server on CentOS Linux systems.Since PHP is commonly used as the Web server side scripting language, you probably need to learn how to enable the Apache Web server, httpd, to support PHP script pages. Here is what I did on my CentOS 8 computer.1\. Verify that PHP FPM (FastCGI Process Manager), php-fpm, is up and running. If not, install "php-fpm" package and start "php-fpm" service. PHP FPM provides the interface between the Apache Web server and the PHP engine.herong$ systemctl status php-fpm
php-fpm.service - The PHP FastCGI Process Manager
   Loaded: loaded (/usr/lib/systemd/system/php-fpm.service; disabled;
   Active: active (running) since Thu 2020-03-26 23:00:41 EDT;
 Main PID: 21507 (php-fpm)
      ...: ...
2\. Verify that Apache Web server, httpd, is up and running. If not, install "httpd" package and start "httpd" service.herong$ systemctl status httpd

httpd.service - The Apache HTTP Server
   Loaded: loaded (/usr/lib/systemd/system/httpd.service; disabled;
  Drop-In: /usr/lib/systemd/system/httpd.service.d
           |-php-fpm.conf
   Active: active (running) since Thu 2020-03-26 22:06:40 EDT;
 Main PID: 19007 (httpd)
      ...: ...
3\. Publish a PHP script in in the HTML document directory on the Apache Web server.herong$ cd /var/www/html

herong$ sudo mkdir test

herong$ ls -l
drwxr-xr-x. 2 root root  6 Mar 28 22:25 test

herong$ sudo chown herong test

herong$ ls -l
drwxr-xr-x. 2 herong root  6 Mar 28 22:25 test

herong$  cd /var/www/html/test

herong$ ls -l
-rw-r--r--. 1 herong herong 73 Mar 28 22:28 test.php

herong$ cat test.php
<html>
<body>
<p>
<?php
print("Hello world!\n");
?>
</p>
</body>
</html>
4\. Verify that the PHP script page is working.herong$ curl http://localhost/test/test.php
<html>
<body>
<p>
Hello world!
</p>
</body>
</html>
[Linux Tutorials - Herong's Tutorial Examples](#text00002.html_a2N5)∟ [Running PHP Scripts on Linux Systems](#text00054.html_a2PT)∟ Dump PHP/Apache Environment InformationProvides a tutorial example on how to dump Apache/PHP environment information on CentOS Linux systems.The execution environment of running PHP scripts on the Apache Web server is different than running them from the command line. You need to dump the Apache/PHP environment information as shown in this tutorial.1\. Publish the following script file, test_phpinfo.php, to the Apache Web server directory, /var/www/html/test:<?php phpinfo(); ?>
2\. View the script file as a Web page, http://localhost/test/test_phpinfo.php in a Web browser. You should see the Apache/PHP environment information displayed in a nice format.HP Version 7.2.11

System  =>  Linux 4.18.0-147.el8.x86_64 #1 SMP Wed Dec 4 21:51:45 UTC 2019
Build Date  =>  10/09/18 03:09 PM
Server API  =>  FPM/FastCGI
Virtual Directory Support  =>  disabled
Configuration File (php.ini) Path  =>  /etc
Loaded Configuration File  =>  /etc/php.ini
Scan this dir for additional .ini files  =>  /etc/php.d
Additional .ini files parsed  =>  /etc/php.d/20-bz2.ini, ...
..

Directive  =>  Local Value  active    Master Value

cgi-fcgi

php-fpm  => active
cgi.discard_path  =>  0  =>  0
cgi.fix_pathinfo  =>  1  =>  1
cgi.force_redirect  =>  1  =>  1
cgi.nph  =>  0  =>  0
cgi.redirect_status_env  =>  no value  =>  no value
cgi.rfc2616_headers  =>  0  =>  0
fastcgi.error_header  =>  no value  =>  no value
fastcgi.logging  =>  1  =>  1

Core

allow_url_fopen  =>  On  =>  On
allow_url_include  =>  Off  =>  Off
...
error_log  =>  /var/log/php-fpm/www-error.log  =>  ...
extension_dir  =>  /usr/lib64/php/modules  =>  /usr/lib64/php/modules

...
Now I know where to go find the Apache/PHP error log file:centos$ sudo ls -l /var/log/php-fpm/

-rw-------. 1 root   root      56 Apr  5 03:06 error.log
-rw-------. 1 root   root    1036 Mar 26 23:00 error.log-20200329
-rw-------. 1 root   root      56 Mar 29 03:45 error.log-20200405
-rw-r--r--. 1 apache apache 15063 Apr  7 05:26 www-error.log
-rw-r--r--. 1 apache apache 36055 Mar 29 03:24 www-error.log-20200329
-rw-r--r--. 1 apache apache 99278 Apr  4 07:36 www-error.log-20200405
[Linux Tutorials - Herong's Tutorial Examples](#text00002.html_a2N5)∟ [Running PHP Scripts on Linux Systems](#text00054.html_a2PT)∟ Apache PHP file_put_contents() Permission DeniedProvides a tutorial example on 'write' permissions in Apache HTML directory from PHP script file_put_contents() function call using the PHP-FPM module on CentOS systems.If you are using PHP-FPM (FastCGI Process Manager) to support PHP scripts on Apache Web server on CentOS systems, you may run into permission issues when writing files with the file_put_contents() function as shown in this tutorial.1\. Create the following PHP script test_file_put_contents.php.<html><body><pre>
<?php
#  test_file_put_contents.php
#- Copyright (c) HerongYang.com. All Rights Reserved.
#
  echo "Output from whoami:\n";
  echo `whoami`."\n";

  echo "Output from getcwd():\n";
  echo getcwd()."\n";

  echo "test file_put_contents(./tmp-cwd.tmp):\n";
  file_put_contents("./tmp-cwd.tmp", "File in the CWD directory.");
  echo `ls -l ./tmp-cwd.tmp`."\n";

  echo "test file_put_contents(/tmp/tmp-tmp.tmp):\n";
  file_put_contents("/tmp/tmp-tmp.tmp", "File in the /tmp directory.");
  echo `ls -l /tmp/tmp-tmp.tmp`."\n";
?>
</pre></body></html>
2\. Run it as a standalone script in my home directory. I see no permission issues, because the script is running under my user name and I have "write" permissions in /home/herong and /tmp.herong$ php test_file_put_contents.php

<html><body><pre>

Output from whoami:
herong

Output from getcwd():
/home/herong

test file_put_contents(./tmp-cwd.tmp):
-rw-rw-r--. 1 herong herong 26 Apr  1 23:30 ./tmp-cwd.tmp

test file_put_contents(/tmp/tmp-tmp.tmp):
-rw-rw-r--. 1 herong herong 27 Apr  1 23:30 /tmp/tmp-tmp.tmp

</pre></body></html>
3\. Grant "write" permission to all users on the Apache test HTML directory, so my test script can create a new file there.herong$ sudo chmod 777 /var/www/html/test

herong$ sudo ls -l /var/www/html
drwxrwxrwx. 2 herong root 4096 Apr  1 21:35 test
4\. Run it as an Apache Web script. I see that "file_put_contents(./tmp-cwd.tmp)" test failed to create a new file.herong$ sudo cp test_file_put_contents.php /var/www/html/test

herong$ curl localhost/test/test_file_put_contents.php
<html><body><pre>

Output from whoami:
apache

Output from getcwd():
/var/www/html/test

test file_put_contents(./tmp-cwd.tmp):

test file_put_contents(/tmp/tmp-tmp.tmp):
-rw-r--r--. 1 apache apache 27 Apr  1 23:49 /tmp/tmp-tmp.tmp

</pre></body></html>
4\. Check the php-fpm module log file. I see that the issue is caused by lack of permission for user "apache" to create files in /var/www/html/test.herong$ sudo tail /var/log/php-fpm/www-error.log

...  
[...] PHP Warning:  file_put_contents(./tmp-cwd.tmp): failed
   to open stream: Permission denied in
   /var/www/html/test/test_file_put_contents.php
It looks like PHP-FPM module added some extra security protection to prevent any PHP scripts to write back to the Apache HTML directory. Giving the "write" permission to all users as "rwxrwxrwx" is not enough for the PHP-FPM module.One workaround is to write files to "/tmp" or "/var/log" from Apache PHP scripts.[Linux Tutorials - Herong's Tutorial Examples](#text00002.html_a2N5)∟ [Running PHP Scripts on Linux Systems](#text00054.html_a2PT)∟ SELinux Security Context on /var/www/htmlProvides a tutorial example on how to change the SELinux security context type on sub directories inside /var/www/html to allow new files to be created by PHP scripts running on the Apache Web server on CentOS systems.The root cause of the "Apache PHP file_put_contents() Permission Denied" problem presented in the previous tutorial is actually the SELinux security context setting on the /var/www/html directory.We can fix it with a temporary solution by changing the SELinux security context type as shown in this tutorial.1\. Compare the SELinux security context of /var/www/html/test with /tmp. I see that their security users, groups, and types are different.herong$ ls -la --context /var/www/html/test
drwxrwxrwx. 2 herong root unconfined_u:object_r:httpd_sys_content_t:s0 .

herong$ ls -la --context /tmp
drwxrwxrwt. 15 root root system_u:object_r:tmp_t:s0 .
2\. Change the SELinux security context type on /var/www/html/test to match /tmp, where my PHP Web script can create files.herong$ cd /var/www
herong$ sudo chcon -t tmp_t test

herong$ ls -la --context test
drwxrwxrwx. 2 herong root   unconfined_u:object_r:tmp_t:s0 .
3\. Re-run the test script on the Apache server. I see that the new file created in /var/www/html/test.herong$ curl localhost/test/test_file_put_contents.php
<html><body><pre>
Output from whoami:
apache

Output from getcwd():
/var/www/html/test

test file_put_contents(./tmp-cwd.tmp):
-rw-r--r--. 1 apache apache 26 Apr  1 02:29 ./tmp-cwd.tmp

test file_put_contents(/tmp/tmp-tmp.tmp):
-rw-r--r--. 1 apache apache 27 Apr  1 02:29 /tmp/tmp-tmp.tmp
</pre></body></html>
Cool. I have a temporary solution to create new files inside the /var/www/html directory from my PHP scripts running on Apache Webserver with the "PHP-FPM" module.[Linux Tutorials - Herong's Tutorial Examples](#text00002.html_a2N5)∟ [Running PHP Scripts on Linux Systems](#text00054.html_a2PT)∟ Migrate Old Scripts to New PHP ReleaseProvides a tutorial example on how to migrate old PHP scripts to PHP new releases.If you are running old PHP scripts on a newer release of the PHP engine, you may see many errors, because some modules or functions are deprecated or removed. Here is a list of them of their replacements.eregi('...', ...);          --> preg_match(('/.../i', ...);
mysql_*()                   --> mysqli_*()
date(): ... not safe ...    --> date_default_timezone_set('Europe/Paris');
[Linux Tutorials - Herong's Tutorial Examples](#text00002.html_a2N5)∟ Running MySQL Database Server on Linux SystemsProvides introductions and tutorial examples about MySQL database server on CentOS systems. Topics include installing MySQL 8.0 on CentOS 8; starting and stoping 'mysqld' as a system service; setting MySQL 'root' password; MySQL file and data locations; MySQL log files; backing up MySQL data; MySQL socket and TCP/IP connections; Open firewall for MySQL connections.[Install MySQL Database Server on CentOS](#text00065.html_a2R4)[Manage MySQL Server 'mysqld' on CentOS](#text00066.html_a2R5)[Set MySQL Server "root" Password on CentOS](#text00067.html_a2R6)[MySQL Server File Locations on CentOS](#text00068.html_a2R7)[MySQL Server Data Backups on CentOS](#text00069.html_a2R8)[MySQL Server Log Files on CentOS](#text00070.html_a2R9)[MySQL Server Socket Connection on CentOS](#text00071.html_a2RA)[MySQL Server TCP/IP Connection on CentOS](#text00072.html_a2RB)[Open Firewall for MySQL Server on CentOS](#text00073.html_a2RC)["Server sent charset unknown to the client" Error](#text00074.html_a2RD)[Performance of Inserting Integers to MySQL Database](#text00075.html_a2RE)[Performance Comparison of Inserting Integers vs. Strings](#text00076.html_a2RF)Takeaways:

*   MySQL server can be installed with the "dnf install mysql-server" command on CentOS 8 systems.
*   MySQL server can be started and stopped with "service mysqld start/stop" commands.
*   MySQL server starts with no password for "root". You can set one with "mysqladmin -u root -p password new_password" command.
*   MySQL command programs are located in "/usr/bin" directory.
*   MySQL data and log files are located in "/var/lib/mysql" directory.
*   MySQL data can be backed up with the "mysqldump" command.
*   MySQL can log all queries with the "eneral_log" setting.
*   MySQL supports socket connections for client programs on the server host using "localhost" as the host name.
*   MySQL supports TCP/IP connections for remote clients on port 3306.
*   MySQL allows a remote user to access only if the user is created with his/her IP address specified.
*   MySQL requires the server and gateway to open firewall for inbound TCP messages on port 3306.
*   "Server sent charset unknown to the client" error is returned when using older PHP mysqli_connect() function to connect to MySQL 8.0.
*   MySQL server is 100 times slower on my CentOS computer than my macOS computer with default settings.

[Linux Tutorials - Herong's Tutorial Examples](#text00002.html_a2N5)∟ [Running MySQL Database Server on Linux Systems](#text00064.html_a2R3)∟ Install MySQL Database Server on CentOSProvides a tutorial example on how to install MySQL 8.0 server on CentOS 8 systems using 'dnf/yum' as the package manager.If you want to use MySQL database server on CentOS Linux systems, you can follow what I did on my CentOS 8 computer:1\. Login as "herong", who has admin privileges.2\. Run "dnf search" to find available MySQL packages. I see "mysql-server" and some related modules available for installation:herong$ dnf search mysql

mysql.x86_64 : MySQL client programs and shared libraries
grafana-mysql.x86_64 : Grafana mysql datasource
postfix-mysql.x86_64 : Postfix MySQL map support
rsyslog-mysql.x86_64 : MySQL support for rsyslog
dovecot-mysql.x86_64 : MySQL back end for dovecot
perl-DBD-MySQL.x86_64 : A MySQL interface for Perl
freeradius-mysql.x86_64 : MySQL support for freeradius
mysql-server.x86_64 : The MySQL server and related files
mysql-test.x86_64 : The test suite distributed with MySQL
...
3\. Install the "mysql-server" package:herong$ sudo dnf install mysql-server

 Package            Arch   Version                  Repo       Size
===================================================================
Installing:
 mysql-server       x86_64 8.0.17-3.module_el8.0.0  AppStream  22 M
Installing dependencies:
 mariadb-connector-c-config
                    noarch 3.0.7-1.el8              AppStream  13 k
 mecab              x86_64 0.996-1.module_el8.0.0   AppStream 397 k
 mysql              x86_64 8.0.17-3.module_el8.0.0  AppStream  11 M
 mysql-common       x86_64 8.0.17-3.module_el8.0.0  AppStream 143 k
 mysql-errmsg       x86_64 8.0.17-3.module_el8.0.0  AppStream 557 k
 protobuf-lite      x86_64 3.5.0-7.el8              AppStream 150 k
Enabling module streams:
 mysql                     8.0

...
Installed:
  mysql-server-8.0.17-3.module_el8.0.0.x86_64
  mariadb-connector-c-config-3.0.7-1.el8.noarch
  mecab-0.996-1.module_el8.0.0+41+ca30bab6.9.x86_64
  mysql-8.0.17-3.module_el8.0.0.x86_64
  mysql-common-8.0.17-3.module_el8.0.0.x86_64
  mysql-errmsg-8.0.17-3.module_el8.0.0.x86_64
  protobuf-lite-3.5.0-7.el8.x86_64

Complete!
3\. Verify the "php" package:herong$ mysql --version

mysql  Ver 8.0.17 for Linux on x86_64 (Source distribution)
Cool! I have installed the "mysql-server" 8.0 on my CentOS computer without any issues. And the MySQL client program "mysql" is working. See next tutorial on how to start and stop MySQL server on CentOS systems.[Linux Tutorials - Herong's Tutorial Examples](#text00002.html_a2N5)∟ [Running MySQL Database Server on Linux Systems](#text00064.html_a2R3)∟ Manage MySQL Server 'mysqld' on CentOSProvides a tutorial example on how to start and stop MySQL server program 'mysqld' as a system service on CentOS 8 systems using the 'systemctl' command.After install MySQL server with the "yum" command CentOS Linux systems, you need to learn how to manage it. The first task is to start or stop the MySQL server. Here is what I did on my CentOS 8 computer.1\. Check MySQL server status. I see an error message, because the it is not running.herong$ mysqladmin status

mysqladmin: connect to server at 'localhost' failed
error: 'Can't connect to local MySQL server through socket ...
Check that mysqld is running and that the socket:
   '/var/lib/mysql/mysql.sock' exists!
2\. Start MySQL server as a system service: I see an error message, because it is not enabled on CentOS 8.herong$ sudo systemctl start mysqld.service

Failed to start mysqld.service: Unit mysqld.service not found.
3\. Enable MySQL server as a system service.herong$ sudo systemctl enable mysqld.service

Created symlink /etc/systemd/system/multi-user.target.wants/mysqld.service
   /usr/lib/systemd/system/mysqld.service.
4\. Check MySQL server status again. I see the server is running. And there is no password for the "root" user!herong$ mysqladmin status -u root -p
Enter password: <Enter>

Uptime: 82  Threads: 2  Questions: 5  Slow queries: 0  Opens: 115
   Flush tables: 3  Open tables: 35  Queries per second avg: 0.060
5\. Stop MySQL server.herong$ sudo systemctl stop mysqld.service
6\. Start MySQL server again.herong$ sudo systemctl start mysqld.service
7\. Connect to MySQL Server with "mysql" client program:herong$ mysql -u root -p
Enter password: <Enter>

...
mysql> show databases;
+--------------------+
| Database           |
+--------------------+
| information_schema |
| mysql              |
| performance_schema |
| sys                |
+--------------------+
Cool. I am able to start and stop MySQL server as a system service on my CentOS 8 computer.You can also use the "service" command, which actually calls the "systemctl" command, to start and stop MySQL server:herong$ sudo service mysqld start

herong$ sudo service mysqld stop
But, do not try to run the MySQL server program, mysqld, directly. You will run into errors.herong$ sudo mysqld

[System] [MY-010116] [Server] /usr/libexec/mysqld (mysqld 8.0.17) starting
   as process 15754
[ERROR] [MY-010123] [Server] Fatal error: Please read "Security" section
   of the manual to find out how to run mysqld as root!
[ERROR] [MY-010119] [Server] Aborting
[System] [MY-010910] [Server] /usr/libexec/mysqld: Shutdown complete
   (mysqld 8.0.17)  Source distribution.
[Linux Tutorials - Herong's Tutorial Examples](#text00002.html_a2N5)∟ [Running MySQL Database Server on Linux Systems](#text00064.html_a2R3)∟ Set MySQL Server "root" Password on CentOSProvides a tutorial example on how to set or reset 'root' password, in case it has no password or you can not remember the password, for MySQL 8.0 server on CentOS 8 systems.When MySQL database server is installed on CentOS, it will create a "root" user name to access the database contents. This "root" user has all types permissions to access all database objects. But it has no password by default.So before adding any data to your MySQL database, you should set a password for this "root" user to protect your data. Here what I did on my MySQL 8 server on my CentOS 8 computer.1\. Connect to MySQL 8 server with the "root" user without any password:herong$ mysql -u root -p
Enter password: <Enter>

...
mysql>
2\. Checking the current password of "root". I see that the "root" use has not password:mysql> select user, host, plugin, authentication_string from mysql.user;
+------------------+-----------+-----------------------+------------------------
| user             | host      | plugin                | authentication_string
+------------------+-----------+-----------------------+------------------------
| mysql.infoschema | localhost | caching_sha2_password | $A$005$THIS...
| mysql.session    | localhost | caching_sha2_password | $A$005$THIS...
| mysql.sys        | localhost | caching_sha2_password | $A$005$THIS...
| root             | localhost | mysql_native_password |
+------------------+-----------+-----------------------+------------------------
3\. Set a new password for the current login user, "root".mysql> set password = 'TopSecret';

mysql> select user, host, plugin, authentication_string from mysql.user;

+------------------+-----------+-----------------------+------------------------
| user             | host      | plugin                | authentication_string
+------------------+-----------+-----------------------+------------------------
| mysql.infoschema | localhost | caching_sha2_password | $A$005$THIS...
| mysql.session    | localhost | caching_sha2_password | $A$005$THIS...
| mysql.sys        | localhost | caching_sha2_password | $A$005$THIS...
| root             | localhost | mysql_native_password | *8E4FBDE7FB...
+------------------+-----------+-----------------------+------------------------
4\. Disconnect and connect agin with the new password:mysql> exit;
Bye

herong$ mysql -u root -p
Enter password: TopSecret<Enter>
...
mysql>
Cool. I have added a password to the "root" user on my MySQL 8 server.Not that there are other ways to set or reset the "root" password:

*   Using "mysqladmin -u root -p password new_password" command.
*   Using "alter user root identified by 'new_password';" MySQL command.
*   Using "update mysql.user set authentication_string = '' where user='root';" SQL statement to update the user table directly, which is not recommended.

If you lost the "root" password, there is only one way to recover it by running MySQL server without password protection:herong$ sudo service mysqld stop

herong$ sudo mysqld --skip-grant-tables &

herong$ mysql -u root
mysql> set password = 'TopSecret';
mysql> quit;

herong$ killall mysqld

herong$ sudo service mysqld start
[Linux Tutorials - Herong's Tutorial Examples](#text00002.html_a2N5)∟ [Running MySQL Database Server on Linux Systems](#text00064.html_a2R3)∟ MySQL Server File Locations on CentOSProvides a tutorial example on how to find and view MySQL Server file locations for MySQL 8.0 server on CentOS 8 systems.In order to properly maintain MySQL server, you need to know how and where MySQL server stores its files. As an example, here are the locations of MySQL server files on my CentOS 8 computer:1\. MySQL command program files are stored in 2 directories:herong$ ls -l /usr/sbin | grep mysql
lrwxrwxrwx. 1 root root        19 Oct  8 09:34 mysqld -> /usr/libexec/mysqld

herong$ ls -l /usr/bin | grep mysql
-rwxr-xr-x. 1 root root     7703224 Oct  8 09:37 mysql
-rwxr-xr-x. 1 root root     7474568 Oct  8 09:37 mysqladmin
-rwxr-xr-x. 1 root root     8198496 Oct  8 09:37 mysqlbinlog
-rwxr-xr-x. 1 root root     7495776 Oct  8 09:37 mysqlcheck
-rwxr-xr-x. 1 root root      674528 Oct  8 09:37 mysql_config_editor
-rwxr-xr-x. 1 root root        4392 Oct  8 09:24 mysqld_pre_systemd
-rwxr-xr-x. 1 root root     7587512 Oct  8 09:37 mysqldump
-rwxr-xr-x. 1 root root        7690 Oct  8 09:24 mysqldumpslow
-rwxr-xr-x. 1 root root     7473216 Oct  8 09:37 mysqlimport
-rwxr-xr-x. 1 root root     8380208 Oct  8 09:37 mysqlpump
-rwxr-xr-x. 1 root root     7458664 Oct  8 09:37 mysql_secure_installation
-rwxr-xr-x. 1 root root     7467968 Oct  8 09:37 mysqlshow
-rwxr-xr-x. 1 root root     7497168 Oct  8 09:37 mysqlslap
-rwxr-xr-x. 1 root root      733424 Oct  8 09:37 mysql_ssl_rsa_setup
-rwxr-xr-x. 1 root root      541152 Oct  8 09:37 mysql_tzinfo_to_sql
-rwxr-xr-x. 1 root root     7656336 Oct  8 09:37 mysql_upgrade
2\. MySQL server data and log files are located at /var/lib/mysql. Each database is stored a separate sub-directory:herong$ ls -l /var/lib/mysql
total 188988
-rw-r-----. 1 mysql mysql       56 Mar 26 22:02  auto.cnf
-rw-r-----. 1 mysql mysql 18315580 Mar 27 05:49  binlog.000001
-rw-r-----. 1 mysql mysql      178 Mar 27 06:13  binlog.000002
-rw-r-----. 1 mysql mysql     9995 Mar 28 08:14  binlog.000003
-rw-r-----. 1 mysql mysql     2785 Mar 28 08:33  binlog.000004
-rw-r-----. 1 mysql mysql       64 Mar 28 08:15  binlog.index
-rw-------. 1 mysql mysql     1680 Mar 26 22:02  ca-key.pem
-rw-r--r--. 1 mysql mysql     1112 Mar 26 22:02  ca.pem
-rw-r--r--. 1 mysql mysql     1112 Mar 26 22:02  client-cert.pem
-rw-------. 1 mysql mysql     1676 Mar 26 22:02  client-key.pem
-rw-r-----. 1 mysql mysql     4188 Mar 28 08:14  ib_buffer_pool
-rw-r-----. 1 mysql mysql 12582912 Mar 28 08:34  ibdata1
-rw-r-----. 1 mysql mysql 50331648 Mar 28 08:34  ib_logfile0
-rw-r-----. 1 mysql mysql 50331648 Mar 26 22:01  ib_logfile1
-rw-r-----. 1 mysql mysql 12582912 Mar 28 08:15  ibtmp1
drwxr-x---. 2 mysql mysql      187 Mar 28 08:15 '#innodb_temp'
drwxr-x---. 2 mysql mysql      143 Mar 26 22:02  mysql
-rw-r-----. 1 mysql mysql 24117248 Mar 28 08:33  mysql.ibd
srwxrwxrwx. 1 mysql mysql        0 Mar 28 08:15  mysql.sock
-rw-------. 1 mysql mysql        5 Mar 28 08:15  mysql.sock.lock
-rw-r--r--. 1 mysql mysql        7 Mar 26 22:02  mysql_upgrade_info
srwxrwxrwx. 1 mysql mysql        0 Mar 28 08:15  mysqlx.sock
-rw-------. 1 mysql mysql        6 Mar 28 08:15  mysqlx.sock.lock
drwxr-x---. 2 mysql mysql     8192 Mar 26 22:02  performance_schema
-rw-------. 1 mysql mysql     1676 Mar 26 22:02  private_key.pem
-rw-r--r--. 1 mysql mysql      452 Mar 26 22:02  public_key.pem
-rw-r--r--. 1 mysql mysql     1112 Mar 26 22:02  server-cert.pem
-rw-------. 1 mysql mysql     1680 Mar 26 22:02  server-key.pem
drwxr-x---. 2 mysql mysql       28 Mar 26 22:02  sys
drwxr-x---. 2 mysql mysql      181 Mar 27 02:00  test
-rw-r-----. 1 mysql mysql 12582912 Mar 28 08:33  undo_001
-rw-r-----. 1 mysql mysql 12582912 Mar 28 08:32  undo_002
[Linux Tutorials - Herong's Tutorial Examples](#text00002.html_a2N5)∟ [Running MySQL Database Server on Linux Systems](#text00064.html_a2R3)∟ MySQL Server Data Backups on CentOSProvides a tutorial example on how to create backups of MySQL databases and load it back to another MySQL server for MySQL 8.0 server on CentOS 8 systems.After using MySQL database server to store your own data, you need to perform data backups periodically and store them on another computer. This can be dump by using the "mysqldump" command as shown in this tutorial:1\. Create a backup of all databases on MySQL server as SQL statements:herong$ mysqldump -u root -p --all-databases > mysql-bck-2020-03-28.sql
2\. Zip the backup file:herong$ zip mysql-bck-2020-03-28.zip mysql-bck-2020-03-28.sql
  adding: mysql-bck-2020-03-28.sql (deflated 89%)
3\. Send it to another computer:herong$ scp mysql-bck-2020-03-28.zip herong@storage:backup
4\. Use the "mysql" command to load the backup file in another MySQL server, if you needed:herong$ mysql -u root -p < mysql-bck-2020-03-28.sql
[Linux Tutorials - Herong's Tutorial Examples](#text00002.html_a2N5)∟ [Running MySQL Database Server on Linux Systems](#text00064.html_a2R3)∟ MySQL Server Log Files on CentOSProvides a tutorial example on how to review log file settings and locations for MySQL 8.0 server on CentOS 8 systems.Log files are very useful to monitor MySQL Server performance and troubleshoot any issues. You should learn how to manage MySQL log files as shown in this tutorial.1\. Remember that MySQL 8 supports 7 types of log files:

*   Error Log - Log errors. Controlled by log_error% variables.
*   Slow Query Log - Logs queries that took longer times. Controlled by slow_query_log* variables.
*   Binary Log - Log statements that change data (also used for replication). Controlled by binlog% and log_bin% variables.
*   General Query Log - Log all queries. Controlled by general_log% variables.
*   DDL Log - Log DDL (Data Definition Language) operations. Controlled by metadata% variables.
*   Relay Log - Log data changes received from a replication master server. Controlled by relay_log% variables.
*   InnoDB Log - Log Controlled by innodb_log% variables.

2\. Review "Error Log" file settings and locations. Remember that "Error Log" is always turned on.herong$ mysqladmin -u root -p variables | grep log_error
| binlog_error_action          | ABORT_SERVER
| log_error                    | /var/log/mysql/mysqld.log
| log_error_services           | log_filter_internal; log_sink_internal
| log_error_suppression_list   |
| log_error_verbosity          | 2

herong$ sudo ls -l /var/log/mysql/mysqld.log
-rw-r-----. 1 mysql mysql 8735 Mar 28 08:20 /var/log/mysql/mysqld.log

herong$ sudo head -100 /var/log/mysql/mysqld.log
[Server] /usr/libexec/mysqld (mysqld 8.0.17) initializing of server
   in progress as process 18690
[Server] root@localhost is created with an empty password ! Please
   consider switching off the --initialize-insecure option.
[Server] /usr/libexec/mysqld (mysqld 8.0.17) initializing of server
   has completed
[Server] /usr/libexec/mysqld (mysqld 8.0.17) starting as process 18739
[Server] CA certificate ca.pem is self signed.
[Server] /usr/libexec/mysqld: ready for connections. Version: '8.0.17'
   socket: '/var/lib/mysql/mysql.sock'  port: 3306  Source distribution.
[Server] X Plugin ready for connections.
   Socket: '/var/lib/mysql/mysqlx.sock' bind-address: '::' port: 33060
...
[Server] /usr/libexec/mysqld: Forcing close of thread 32  user: 'root'.
[Server] /usr/libexec/mysqld: Forcing close of thread 9  user: 'root'.
[Server] /usr/libexec/mysqld: Shutdown complete (mysqld 8.0.17)
   Source distribution.
3\. Turn on "General Query Log", if you want to debug some MySQL applications.herong$ mysql -u root -p

mysql> show variables like 'general_log%';
+------------------+------------------------------+
| Variable_name    | Value                        |
+------------------+------------------------------+
| general_log      | OFF                          |
| general_log_file | /var/lib/mysql/localhost.log |
+------------------+------------------------------+

mysql> set global general_log = on;

(Run your MySQL application)

herong$ sudo head -100 /var/lib/mysql/localhost.log
/usr/libexec/mysqld, Version: 8.0.17 (Source distribution). started with:
Tcp port: 3306  Unix socket: /var/lib/mysql/mysql.sock
Time                 Id Command    Argument
...
... 34 Connect  herong@localhost on mydb using Socket
... 34 Query  SELECT COUNT(*) FROM Cases
... 34 Query  SELECT * FROM Cases  ORDER BY ID DESC LIMIT 0, 30
... 34 Quit

... 35 Connect  herong@localhost on mydb using Socket
... 35 Query  SELECT * FROM Cases WHERE ID = 10001
... 35 Quit
4\. Review "Binary Log" file settings and locations. Remember that "Binary Log" is turned on by default. "Binary Log" files are stored in binary format. So you need to use "mysqlbinlog" command to read it.[Linux Tutorials - Herong's Tutorial Examples](#text00002.html_a2N5)∟ [Running MySQL Database Server on Linux Systems](#text00064.html_a2R3)∟ MySQL Server Socket Connection on CentOSProvides a tutorial example on how to use the Socket Connection for client programs from the same host as the MySQL 8 Server on CentOS 8 systems.MySQL server supports 2 types of connections from client programs:

*   Socket Connection, or Named Pipe Connection - Allows client programs from the local host to access the server without using the TCP/IP protocol.
*   TCP/IP Connection - Allows client programs from any hosts to access the server using the TCP/IP protocol.

Socket Connection works under the following rules:1\. By default, the Socket Connection is turned on for MySQL 8 server.2\. Socket Connection is represented with socket files on CentOS system with "mysqlx_socket" and "socket" variables for their locations:mysql> show variables like '%socket';
+---------------+----------------------------+
| Variable_name | Value                      |
+---------------+----------------------------+
| mysqlx_socket | /var/lib/mysql/mysqlx.sock |
| socket        | /var/lib/mysql/mysql.sock  |
+---------------+----------------------------+
3\. Users must be created with "localhost" as host named to use the Socket Connection. For example, "root" and "herong" are users who can use the Socket Connection based on the mysql.user records:mysql> select user, host from mysql.user;
+------------------+-----------+
| user             | host      |
+------------------+-----------+
| mysql.infoschema | localhost |
| mysql.session    | localhost |
| mysql.sys        | localhost |
| root             | localhost |
| herong           | localhost |
+------------------+-----------+
4\. Client programs must use "localhost" as the host name to use the Socket Connection. For example, the following PHP statement will connect to the MySQL server using the Socket Connection:$conn = mysqli_connect("localhost", 'herong', 'TopSecret');
5\. MySQL client tools connect to the SQL server use the Socket Connection with the default "-h localhost" option. See the example below:herong$ mysql -u herong -p
Enter password: junk<Enter>

ERROR 1045 (28000): Access denied for user 'herong'@'localhost' ...
Socket Connection is more secure. But it only allows connections from the same host as the MySQL server. To allow connections from a remote host, you have to use the TCP/IP connection as shown in the next tutorial.[Linux Tutorials - Herong's Tutorial Examples](#text00002.html_a2N5)∟ [Running MySQL Database Server on Linux Systems](#text00064.html_a2R3)∟ MySQL Server TCP/IP Connection on CentOSProvides a tutorial example on how to use the TCP/IP Connection for client programs from any hosts to connect to the MySQL 8 Server on CentOS 8 systems.MySQL server supports 2 types of connections from client programs:

*   Socket Connection, or Named Pipe Connection - Allows client programs from the local host to access the server without using the TCP/IP protocol.
*   TCP/IP Connection - Allows client programs from any hosts to access the server using the TCP/IP protocol.

TCP/IP Connection works under the following rules:1\. By default, the TCP/IP Connection is turned on for MySQL 8 server.2\. The MySQL server listens on the IP address of the server host specified in the "bind_address" variable. A comma-separated IP list can be specified if the server has multiple IP addresses. Wildcard "*" can be specified to listen to all IP addresses on the server. "bind_address" is set to "*" by default for MySQL 8.0 server on CentOS 8.mysql> show variables like '%bind_address';
+---------------------+-------+
| Variable_name       | Value |
+---------------------+-------+
| bind_address        | *     |
| mysqlx_bind_address | *     |
+---------------------+-------+
3\. "bind_address" is a read only variable, you need to set it in MySQL server configuration file, /etc/my.cnf.d/mysql-server.cnf, which is included in the /etc/my.cnf file. For example, you can change "bind_address" to a specific IP address to make the server more secure. Remember to restart MySQL server after changing the configuration file.herong$ sudo cat /etc/my.cnf.d/mysql-server.cnf

[mysqld]

# Listen to the loopback IP address only so only client programs
# from the server host can use the TCP/IP connection.
# bind_address=127.0.0.1

# Listen to the local IP address only so only client programs
# from other local IP address, 192.168.1.* can use the TCP/IP connection
# bind_address=192.168.1.100

# Default - Listen to all IP addresses on the server host.
bind_address=*
4\. The MySQL server listens on IP port 3306 specified in the "port" variable, which is a read only variable too. If you need to change it, you have to set it MySQL server configuration file, /etc/my.cnf.d/mysql-server.cnf, which is included in the /etc/my.cnf file.5\. Users must be created with their IP address as host names to use the TCP/IP Connection. The format of a user from a given IP address is 'user'@'ip_address'. You can use wildcard characters in the IP address to represent a range of IP addresses. For example, 'herong'@'127.0.0.1' . allows me to connect to the server from my computer that has IP address of 192.168.1.11\. 'herong'@'192.168.1.%' allows me to connect to the server from any computer on the local network. 'herong'@'%' allows me to connect to the server from any computer on the entire Intener. See MySQL commands below to create multiple users to use the TCP/IP connection from different remote client hosts:mysql> # To use the TCP/IP connection on the same host
mysql> create user 'herong'@'127.0.0.1' identified by 'TopSecret';

mysql> # Allow TCP/IP connection from my computer
mysql> create user 'herong'@'192.168.1.11' identified by 'TopSecret';

mysql> # Allow TCP/IP connection from any computer on the local network
mysql> create user 'herong'@'192.168.1.%' identified by 'TopSecret';

mysql> # Allow TCP/IP connection from any computer on the entire Internet
mysql> create user 'herong'@'%' identified by 'TopSecret';

mysql> select user, host from mysql.user;
+------------------+--------------+
| user             | host         |
+------------------+--------------+
| herong           | localhost    |
| herong           | 127.0.0.1    |
| herong           | 192.168.1.11 |
| herong           | 192.168.1.%  |
| herong           | %            |
+------------------+--------------+
6\. Client programs can specify the IP address and the port number where the MySQL server is listening to make a TCP/IP Connection. F or example, the following PHP statements will connect to the MySQL server using the TCP Connection:# MySQL is listening on 127.0.0.1 at 3306:
$conn = mysqli_connect("127.0.0.1", 'herong', 'TopSecret');

# MySQL is listening on 192.168.1.100 at 3306:
$conn = mysqli_connect("192.168.1.100", 'herong', 'TopSecret');

# MySQL is listening on 192.168.1.100 at 3307:
$conn = mysqli_connect("192.168.1.100:3307", 'herong', 'TopSecret');
7\. MySQL client tools connect to the SQL server use the TCP/IP Connection with given "-h ip_address" and "-P port_nunber" options. See the example below:herong$ mysql -u herong -h 192.168.1.100 -p

herong$ mysql -u herong -h 192.168.1.100 -P 3307 -p
8\. The last issue you may have on using TCP/IP connection is network firewall. Firewall may stop your TCP/IP connection in 4 places:

*   Firewall on your computer must allow TCP outbound request to the MySQL server.
*   Firewall on your computer local network must allow your TCP request to go out.
*   Firewall on the gateway the MySQL server local network must allow your TCP request to go in.
*   Firewall on the MySQL server must to be open to accept TCP inbound requests from your IP address.

[Linux Tutorials - Herong's Tutorial Examples](#text00002.html_a2N5)∟ [Running MySQL Database Server on Linux Systems](#text00064.html_a2R3)∟ Open Firewall for MySQL Server on CentOSProvides a tutorial example on how to setup MySQL server and firewall to client computers to use TCP/IP connections on CentOS 8 systems.If you want client programs from other computers to use the TCP/IP connection of the MySQL server on CentOS systems, you can follow what I did on my CentOS 8 computer.1\. Make sure that MySQL server is listening on an IP address with a given port number. I see that the server is listening on 192.168.1.100:3306 using these commands on server. Remember that "bind_address=*" supports any IP address used by the server.herong$ ifconfig
eno1: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
      inet 192.168.1.100  netmask 255.255.255.0  broadcast 192.168.1.255
      ...  

herong$ mysql -u root -p

mysql> show variables like 'bind_address';
+---------------------+-------+
| Variable_name       | Value |
+---------------------+-------+
| bind_address        | *     |
+---------------------+-------+

mysql> show variables like 'port';
+---------------+-------+
| Variable_name | Value |
+---------------+-------+
| port          | 3306  |
+---------------+-------+
2\. Make sure that my MySQL user accounts covers my computer IP address. I see that my computer IP address 192.168.1.11 is covered:(On the server)
herong$ mysql -u root -p

mysql> select user, host from mysql.user;
+------------------+--------------+
| user             | host         |
+------------------+--------------+
| herong           | localhost    |
| herong           | 127.0.0.1    |
| herong           | 192.168.1.%  |
+------------------+--------------+

(On my computer)
herong$ ifconfig
en0: flags=8863<UP,BROADCAST,SMART,RUNNING,SIMPLEX,MULTICAST> mtu 1500
  inet 192.168.1.11 netmask 0xffffff00 broadcast 192.168.1.255
3\. Checking IP address and port connection from my computer to the server. I see that my computer can reach the server, but not the port 3306.(On my computer)
herong$ ping 192.168.1.100
PING 192.168.1.100 (192.168.1.100): 56 data bytes
64 bytes from 192.168.1.100: icmp_seq=0 ttl=64 time=4.548 ms
64 bytes from 192.168.1.100: icmp_seq=1 ttl=64 time=2.308 ms
...

herong$ telnet 192.168.1.100 3306
Trying 192.168.1.100...
telnet: connect to address 192.168.1.100: Connection refused
telnet: Unable to connect to remote host
4\. Open the firewall on the MySQL server for port 3306\. These commands opens port 3306 for all computers on the Internet. I need to add more restrictions later.(On the server)
herong$ sudo firewall-cmd --zone=public --add-port=3306/tcp
herong$ sudo firewall-cmd --runtime-to-permanent
5\. Checking IP address and port connection from my computer to the server again. I see that the TCP/IP connection is open.herong$ telnet 192.168.1.100 3306
Trying 192.168.1.100...
Connected to 192.168.1.100.
Escape character is '^]'.
J
8.0.17/1TZi76?l...
6\. Finally, connect to MySQL server from my client computer:herong$ /usr/local/mysql/bin/mysql -u herong -h 192.168.1.100 -p
Enter password: TopSecret<Enter>

mysql>
Cool! I was able to setup MySQL server and firewall to for TCP/IP connection from my client computer.[Linux Tutorials - Herong's Tutorial Examples](#text00002.html_a2N5)∟ [Running MySQL Database Server on Linux Systems](#text00064.html_a2R3)∟ "Server sent charset unknown to the client" ErrorProvides a tutorial example on how to resolve the 'Server sent charset unknown to the client' error received in PHP mysqli_connect() call to MySQL 8.0 running on CentOS 8 systems.If you are running an older version of PHP on a client computer and tries to connection a MySQL 8.0 running on a CentOS system with the mysqli_connect() function, you will get the "Server sent charset unknown to the client" error:herong$ php --version
PHP 5.6.30 (cli) (built: Oct 29 2017 20:30:32)

herong$ php test.php   
PHP Warning:  mysqli_connect(): Server sent charset (255) unknown
   to the client. Please, report to the developers
   in /Users/herong/test.php on line 10.
PHP Warning:  mysqli_connect(): (HY000/2054): Server sent charset ...
Based on reports on the Internet, the above issue is caused by the default setting of "character_set_client = utf8mb4", which is unknown to older PHP "mysqli" modules.ßI have tried a number of solutions suggested on the Internet. None of them works for me. Combinations of them are also not working.

*   Run "set global character_set_client = 'utf8';" on MySQL 8.0 server.
*   Run "set global character_set_results = 'utf8';" on MySQL 8.0 server.
*   Run "set global character_set_connection = 'utf8';" on MySQL 8.0 server.
*   Restart MySQL 8.0 server with the "skip-character-set-client-handshake" option.
*   Restart MySQL 8.0 server with the "character_set_client=utf8" option.

The only solution that worked for my is to upgrade PHP toherong$ php --version
PHP 7.2.11 (cli) (built: Oct  9 2018 15:09:36) ( NTS )

herong$ php test.php
mysqli_get_server_info() = 8.0.17
mysqli_get_host_info() = 192.168.1.100 via TCP/IP
[Linux Tutorials - Herong's Tutorial Examples](#text00002.html_a2N5)∟ [Running MySQL Database Server on Linux Systems](#text00064.html_a2R3)∟ Performance of Inserting Integers to MySQL DatabaseProvides a tutorial example on how to test the performance of inserting integers into MySQL server database using PHP 'mysqli' functions. MySQL server is 100 times slower on my CentOS computer and macOS computer.If you are working with large data sets, then you need to know the performance of MySQL server. Here are some measurements I collected on MySQL servers running my CentOS 8 and macOS 10 computers.1\. Create a PHP script to measure the speed of inserting integers into database.<?php
# speed-of-insert-integer.php
# Copyright (c) HerongYang.com. All Rights Reserved.
#    
  $count = 100;
  if (count($argv)>1) $count = $argv[1];

  $binLog = "on";
  if (count($argv)>2) $binLog = $argv[2];

  print("Testing parameters:\n");
  print("   Number of operations: ".$count."\n");
  print("   Binary log = $binLog\n");

  $con = mysqli_connect("127.0.0.1", 'herong', 'TopSecret', "test");

  $sql = "SET sql_log_bin = $binLog";
  $res = mysqli_query($con, $sql);

  $sql = "CREATE TABLE Tests (Quantity INTEGER)";
  $res = mysqli_query($con, $sql);

  $startTime = round(microtime(true)*1000);  
  $i = 0;
  while ($i < $count) {
    $sql = "INSERT INTO Tests VALUES ($i)";
    $res = mysqli_query($con, $sql);
    $i++;
  }
  $endTime = round(microtime(true)*1000);
  $exeTime = $endTime - $startTime;
  print("Testing result:\n");
  print("   Execution time in milliseconds = ".$exeTime."\n");
  print("   Milliseconds per operation = ".round($exeTime/$count)."\n");

  $sql = "SELECT COUNT(*) FROM Tests";
  $res = mysqli_query($con, $sql);
  $row = mysqli_fetch_array($res);
  print("   Records inserted = ".$row[0]."\n");

  $sql = "DROP TABLE Tests";
  $res = mysqli_query($con, $sql);
  mysqli_close($con);
?>
2\. Establish performance baseline for the MySQL server on my CentOS 8 computer. I see that inserting an integer into the database took about 55 milliseconds. This is too high and needs to be investigated.centos$ php speed-of-insert-integer.php 100
Testing parameters:
   Number of operations: 100
   Binary log = on
Testing result:
   Execution time in milliseconds = 5295
   Milliseconds per operation = 53
   Records inserted = 100

centos$ php speed-of-insert-integer.php 1000
Testing parameters:
   Number of operations: 1000
   Binary log = on
Testing result:
   Execution time in milliseconds = 59162
   Milliseconds per operation = 59
   Records inserted = 1000
3\. Check the impact of binary logging on the MySQL server on my CentOS 8 computer. I see that turning off binary logging does not improve the performance. This is also a surprise to me.centos$ php speed-of-insert-integer.php 100 off
Testing parameters:
   Number of operations: 100
   Binary log = off
Testing result:
   Execution time in milliseconds = 5586
   Milliseconds per operation = 56
   Records inserted = 100
4\. Compare performance with the MySQL server on my macOS 10 computer. I see that my macOS computer is 100 times faster! This is a big surprise to me!macOS$ php speed-of-insert-integer.php 100
Testing parameters:
   Number of operations: 100
   Binary log = on
Testing result:
   Execution time in milliseconds = 47
   Milliseconds per operation = 0
   Records inserted = 100

macOS$ php speed-of-insert-integer.php 1000
Testing parameters:
   Number of operations: 1000
   Binary log = on
Testing result:
   Execution time in milliseconds = 397
   Milliseconds per operation = 0
   Records inserted = 1000
[Linux Tutorials - Herong's Tutorial Examples](#text00002.html_a2N5)∟ [Running MySQL Database Server on Linux Systems](#text00064.html_a2R3)∟ Performance Comparison of Inserting Integers vs. StringsProvides a tutorial example on how to check performance comparison between inserting integers and inserting strings to MySQL database.As a comparison, I created another PHP script to measure the speed of inserting strings into database.<?php
# speed-of-insert-string.php
# Copyright (c) HerongYang.com. All Rights Reserved.
#    
  $count = 100;
  if (count($argv)>1) $count = $argv[1];

  $binLog = "on";
  if (count($argv)>2) $binLog = $argv[2];

  $charset = "utf8mb4";
  $collate = "utf8mb4_0900_ai_ci";
  if (count($argv)>3) $charset = $argv[3];
  if ($charset=="utf8") {
    $collate = "utf8_unicode_ci";
  } else if ($charset=="utf8mb4") {
    $collate = "utf8mb4_0900_ai_ci";
  } else {
    print("Unknown character set: $charset\n");
    die;
  }

  print("Testing parameters:\n");
  print("   Number of operations: ".$count."\n");
  print("   Binary log = $binLog\n");
  print("   Character set = $charset\n");

  $con = mysqli_connect("127.0.0.1", 'herong', 'TopSecret', "test");

  $sql = "SET sql_log_bin = $binLog";
  $res = mysqli_query($con, $sql);

  $sql = "CREATE TABLE Tests (Message CHAR(4))"
    . " ENGINE=InnoDB DEFAULT CHARSET=$charset COLLATE=$collate";
  $res = mysqli_query($con, $sql);

  $startTime = round(microtime(true)*1000);  
  $i = 0;
  while ($i < $count) {
    $str = substr(strval(10000+$i), -4);
    $sql = "INSERT INTO Tests VALUES ('$str')";
    $res = mysqli_query($con, $sql);
    $i++;
  }
  $endTime = round(microtime(true)*1000);
  $exeTime = $endTime - $startTime;
  print("Testing result:\n");
  print("   Execution time in milliseconds = ".$exeTime."\n");
  print("   Milliseconds per operation = ".round($exeTime/$count)."\n");

  $sql = "SELECT COUNT(*) FROM Tests";
  $res = mysqli_query($con, $sql);
  $row = mysqli_fetch_array($res);
  print("   Records inserted = ".$row[0]."\n");

  $sql = "DROP TABLE Tests";
  $res = mysqli_query($con, $sql);
  mysqli_close($con);
?>
1\. Compare performance of inserting strings against inserting integers to the MySQL server on my CentOS 8 computer. I see that inserting strings takes about the same time as inserting integers.centos$ php speed-of-insert-string.php 100
Testing parameters:
   Number of operations: 100
   Binary log = on
   Character set = utf8mb4
Testing result:
   Execution time in milliseconds = 5303
   Milliseconds per operation = 53
   Records inserted = 100

centos$ php speed-of-insert-string.php 1000
Testing parameters:
   Number of operations: 1000
   Binary log = on
   Character set = utf8mb4
Testing result:
   Execution time in milliseconds = 60823
   Milliseconds per operation = 61

centos$ php speed-of-insert-integer.php 100
Testing parameters:
   Number of operations: 100
   Binary log = on
Testing result:
   Execution time in milliseconds = 5295
   Milliseconds per operation = 53
   Records inserted = 100

centos$ php speed-of-insert-integer.php 1000
Testing parameters:
   Number of operations: 1000
   Binary log = on
Testing result:
   Execution time in milliseconds = 59162
   Milliseconds per operation = 59
   Records inserted = 1000
2\. Check impact of binary logging when storing strings in MySQL database on my CentOS 8 computer. I see that there is almost no impact by turning off binary logging.centos$ php speed-of-insert-string.php 100 off
Testing parameters:
   Number of operations: 100
   Binary log = off
   Character set = utf8mb4
Testing result:
   Execution time in milliseconds = 5319
   Milliseconds per operation = 53
   Records inserted = 100
3\. Check impact of character encoding when storing strings in MySQL database on my CentOS 8 computer. I see that there is almost no impact by switching from utf8mb4 to utf8.centos$ php speed-of-insert-string.php 100 on utf8
Testing parameters:
   Number of operations: 100
   Binary log = on
   Character set = utf8
Testing result:
   Execution time in milliseconds = 5245
   Milliseconds per operation = 52
   Records inserted = 100
[Linux Tutorials - Herong's Tutorial Examples](#text00002.html_a2N5)∟ Running Python Scripts on Linux SystemsProvides introductions and tutorial examples about running Python scripts on Linux systems. Topics include installing PHP engine on CentOS Linux systems; installing missing Python packages/modules with 'pip3' command.[Install and Manage Python Engine on CentOS](#text00078.html_a2RH)["pip/pip3" Python Package Manager](#text00079.html_a2RJ)[Install MySQL Connector/Python on CentOS](#text00080.html_a2RK)[Install Python 2 Engine on CentOS](#text00081.html_a2RM)Takeaways:

*   The Python 3 script engine is included as part of the CentOS 8 system by default.
*   "pip3" command is the Python 3 external package/module manager.
*   MySQL Connector/Python allows you to access MySQL database server from Python scripts.
*   Python 2 script engine is still needed to run old Python scripts.

[Linux Tutorials - Herong's Tutorial Examples](#text00002.html_a2N5)∟ [Running Python Scripts on Linux Systems](#text00077.html_a2RG)∟ Install and Manage Python Engine on CentOSProvides a tutorial example on how to install Python 3.6 on CentOS 8 systems using 'dnf/yum' as the package manager.The Python script engine is included as part of the CentOS 8 system by default. You don't need to install it yourself. But you can still install its additional modules using the "dnf" package manager.1\. Login as "herong", who has admin privileges.2\. Check the current installed version of Python:herong$ python3 --version

Python 3.6.8
3\. Run "dnf search python3" to find Python package name:herong$ dnf search python3

python36.x86_64 : Interpreter of the Python programming language
python3-py.noarch : Library with cross-python path, ini-parsing, io, code, log facilities
python3-gpg.x86_64 : gpgme bindings for Python 3
python3-meh.noarch : A python 3 library for handling exceptions
python3-pid.noarch : PID file management library
python3-ply.noarch : Python Lex-Yacc
...
4\. Install the "python36" package:herong$ sudo dnf install python36

Package python36-3.6.8-2.module_el8.1.0+245+c39af44f.x86_64 is already installed.
Dependencies resolved.
Nothing to do.
Complete!
Ok. The installed Python 3.6 package is the latest package from the repository. So there is nothing to be installed.[Linux Tutorials - Herong's Tutorial Examples](#text00002.html_a2N5)∟ [Running Python Scripts on Linux Systems](#text00077.html_a2RG)∟ "pip/pip3" Python Package ManagerProvides a tutorial example on how to use 'pip/pip3' command to install and manage Python packages.When you develop Python applications, you may need to install additional Python packages developed by third parties. The best tool to manage those third party packages is the "pip/pip3" command as demonstrated in this tutorial.1\. Show "pip3" command options to manage Python3 packages.herong$ pip3 help

Usage:
  pip <command> [options]

Commands:
  install          Install packages.
  download         Download packages.
  uninstall        Uninstall packages.
  freeze           Output installed packages in requirements format.
  list             List installed packages.
  show             Show information about installed packages.
  check            Verify installed packages have compatible dependencies.
  search           Search PyPI for packages.
  wheel            Build wheels from your requirements.
  hash             Compute hashes of package archives.
  completion       A helper command used for command completion.
  help             Show help for commands.

General Options:
  -h, --help       Show help.
  --isolated       Run pip in an isolated mode, ignoring environment
                   variables and user configuration.      
  -v, --verbose    Give more output. Option is additive, and can be
                   used up to 3 times.
  -V, --version    Show version and exit.
  -q, --quiet      Give less output. Option is additive, and can be
                   used up to 3 times (corresponding to
                   WARNING, ERROR, and CRITICAL logging levels).
  --log <path>     Path to a verbose appending log.
2\. Get a list of installed Python3 packages:herong$ pip3 list

asn1crypto (0.24.0)
blivet (3.1.0)
Brlapi (0.6.7)
cffi (1.11.5)
chardet (3.0.4)
chrome-gnome-shell (0.0.0)
configobj (5.0.6)
coverage (4.5.1)
cryptography (2.3)
...
3\. Search for a package to handle JSON strings. I see a list of JSON packages. I am not sure which is better.herong$ pip3 search json

json-escape (1.0.0)              - Json escape
json-websocket (0.2.1582880480)  - json-websocket
json-dotenv (0.0.21)             - json-dotenv
mo-json (3.57.20089)             - More JSON Tools!
json-mindiff (0.1)               - Minimize json diffs
linaro-json (2.0.1)              - JSON Schema Validator
json-logging (1.0.6)             - JSON Python Logging
json-repository (0.2.0)          - A simple json repository
pygments-json (0.1)              - Pygments JSON formatter
pretty-json (1.2.0)              - make pretty json
...
4\. Sometimes, "pip3" command may fail due to network connection issue. Just try it again later.herong$ pip3 search json
Retrying (Retry(total=4, connect=None, read=None, redirect=None, ...
...
Exception:
Traceback (most recent call last):
  File "/usr/lib/python3.6/site-packages/pip/_vendor/urllib3/connection.py"
  ...
OSError: [Errno 101] Network is unreachable
5\. If you think your "pip3" command is outdated, you can use "pip3" to upgrade itself.herong$ pip3 install --upgrade pip
6\. Run "pip3" with the "python3 -m pip" command. This works because "pip" is actually a Python3 module.herong$ python3 -m pip help

Usage:
  /usr/bin/python3 -m pip <command> [options]
  ...
[Linux Tutorials - Herong's Tutorial Examples](#text00002.html_a2N5)∟ [Running Python Scripts on Linux Systems](#text00077.html_a2RG)∟ Install MySQL Connector/Python on CentOSProvides a tutorial example on how to install MySQL Connector/Python on CentOS systems.If you want to access MySQL database server from Python scripts, you can follow what I did on my CentOS 8 computer to install the MySQL Connector/Python module.1\. Install MySQL Connector/Python with "pip3" command.herong$ sudo pip3 install mysql-connector-python

Collecting mysql-connector-python
  Downloading https://files.pythonhosted.org/packages/d8/29/...
Collecting dnspython==1.16.0 (from mysql-connector-python)
  Downloading https://files.pythonhosted.org/packages/ec/d3/...
Collecting protobuf==3.6.1 (from mysql-connector-python)
  Downloading https://files.pythonhosted.org/packages/c2/f9/...
Requirement already satisfied: six>=1.9 ...
Requirement already satisfied: setuptools ...
Installing collected packages: dnspython, protobuf, mysql-connector-python
  Found existing installation: protobuf 3.11.3
  Successfully uninstalled protobuf-3.11.3
Successfully installed
  dnspython-1.16.0 mysql-connector-python-8.0.19 protobuf-3.6.1
2\. If "pip3" command fails, install MySQL Connector/Python with "dnf/yum" command.herong$ sudo yum install mysql-connector-python
...
3\. If "dnf/yum" command fails, Go to MySQL Connector/Python download Web site at [https://dev.mysql.com/downloads/connector/python/](https://dev.mysql.com/downloads/connector/python/) to download the "Red Hat Enterprise Linux 8 / Oracle Linux 8 (x86, 64-bit), RPM Package". Then run the "rpm" command to install it.herong$ sudo rpm -i ....rpm
4\. Test MySQL Connector/Python with the following Python code:herong$ python3
>>> import mysql.connector
>>> con = mysql.connector.connect(
  user='herong', password='TopSecret', host='localhost')
>>> con.close()
5\. Read the MySQL Connector/Python Developer Guide at [https://dev.mysql.com/doc/connector-python/en/](https://dev.mysql.com/doc/connector-python/en/) to learn more.[Linux Tutorials - Herong's Tutorial Examples](#text00002.html_a2N5)∟ [Running Python Scripts on Linux Systems](#text00077.html_a2RG)∟ Install Python 2 Engine on CentOSProvides a tutorial example on how to install Python 2 engine to run old Python scripts and applications on CentOS systems.If you still have some old Python scripts written in Python 2 language, you need to following this tutorial to install the module.1\. Check for Python 2 packages:herong$ dnf search python2

python2.x86_64 : An interpreted, interactive, object-oriented programming language
python2-jinja2.noarch : General purpose template engine for python2
python2-test.x86_64 : The test modules from the main python2 package
python2-docutils.noarch : System for processing plaintext documentation for python2
python2-urllib3.noarch : Python2 HTTP library with thread-safe connection pooling and file post
...
2\. Install Python 2:herong$ sudo dnf install python2

...
Installed:
  python2-2.7.16-12.module_el8.1.0+219+cf9e6ac9.x86_64
  python2-pip-9.0.3-14.module_el8.1.0+219+cf9e6ac9.noarch
  python2-setuptools-39.0.1-11.module_el8.1.0+219+cf9e6ac9.noarch
  python2-libs-2.7.16-12.module_el8.1.0+219+cf9e6ac9.x86_64
  python2-pip-wheel-9.0.3-14.module_el8.1.0+219+cf9e6ac9.noarch
  python2-setuptools-wheel-39.0.1-11.module_el8.1.0+219+cf9e6ac9.noarch

Complete!
3\. Verify Python 2 installation:herong$ python2

Python 2.7.16 (default, Nov 17 2019, 00:07:27)
[GCC 8.3.1 20190507 (Red Hat 8.3.1-4)] on linux2
>>> <Ctrl-D>

herong$ pip2 --version
pip 9.0.3 from /usr/lib/python2.7/site-packages (python 2.7)
Cool. I have Python 2 engine and package installer installed and ready to run any Python 2 scripts.[Linux Tutorials - Herong's Tutorial Examples](#text00002.html_a2N5)∟ vsftpd - Very Secure FTP DaemonProvides introductions and tutorial examples about 'vsftpd' - Very Secure FTP Daemon. Topics include installing vsftpd; configuring vsftpd for local user access; testing FTP access locally and remotely; enabling FTP over SSL/TLS to secure connections.[Install vsftpd on CentOS](#text00083.html_a2RP)[vsftpd Server Configuration](#text00084.html_a2RR)[Setup FTP Sub-Directory for Local Users](#text00085.html_a2RS)[Test FTP Access Locally on CentOS](#text00086.html_a2RT)[Test FTP Access Remotely on CentOS](#text00087.html_a2RU)[Support FTP Over TLS on CentOS](#text00088.html_a2RV)[Disable SSH Access for FTP Users](#text00089.html_a2RW)Takeaways:

*   'vsftpd' (Very Secure FTP Daemon) is popular FTP server for Linux systems.
*   You can configure 'vsftpd' to allow local users to access the FTP server and upload/download files in their home directories.
*   You can configure 'vsftpd' to support FTP over SSL/TLS to secure FTP connections.

[Linux Tutorials - Herong's Tutorial Examples](#text00002.html_a2N5)∟ [vsftpd - Very Secure FTP Daemon](#text00082.html_a2RN)∟ Install vsftpd on CentOSProvides a tutorial example on how to install, enable and start vsftpd (Very Secure FTP Daemon) on CentOS systems.If you want to set up an FTP server on your CentOS system, you should consider installing and running vsftpd (Very Secure FTP Daemon). Main features of vsftpd are:

*   Virtual IP configurations
*   Virtual users
*   Standalone or inetd operation
*   Powerful per-user configurability
*   Bandwidth throttling
*   Per-source-IP configurability
*   Per-source-IP limits
*   IPv6
*   Encryption support through SSL integration

Here is what I did to install vsftpd on my CentOS 8 computer.1\. Install GCC C compiler:herong$ dnf info vsftpd
Available Packages
Name         : vsftpd
Version      : 3.0.3
Release      : 28.el8
Architecture : x86_64
Size         : 180 k
Source       : vsftpd-3.0.3-28.el8.src.rpm
Repository   : AppStream
Summary      : Very Secure Ftp Daemon
URL          : https://security.appspot.com/vsftpd.html
License      : GPLv2 with exceptions
Description  : vsftpd is a Very Secure FTP daemon. It was written
             : completely from scratch.

herong$ sudo dnf install vsftpd
...
Downloading Packages:
vsftpd-3.0.3-28.el8.x86_64.rpm   2.5 MB/s | 180 kB     00:00
...
Installed:
vsftpd-3.0.3-28.el8.x86_64

Complete!
2\. Enable vsftpd so that will be started automatically at system boot time:herong$ sudo systemctl enable vsftpd
Created symlink /etc/systemd/system/multi-user.target.wants/vsftpd.service \
  -> /usr/lib/systemd/system/vsftpd.service.
3\. Start vsftpd and check its status:herong$ sudo systemctl start vsftpd

herong$ sudo systemctl status vsftpd
  vsftpd.service - Vsftpd ftp daemon
   Loaded: loaded (/usr/lib/systemd/system/vsftpd.service; enabled; ...
   Active: active (running)
  Process: 26802 ExecStart=/usr/sbin/vsftpd /etc/vsftpd/vsftpd.conf
 Main PID: 26803 (vsftpd)
    Tasks: 1 (limit: 23087)
   Memory: 540.0K
   CGroup: /system.slice/vsftpd.service
           | 26803 /usr/sbin/vsftpd /etc/vsftpd/vsftpd.conf

Jun 23 16:59:40  systemd[1]: Starting Vsftpd ftp daemon...
Jun 23 16:59:40  systemd[1]: Started Vsftpd ftp daemon.
[Linux Tutorials - Herong's Tutorial Examples](#text00002.html_a2N5)∟ [vsftpd - Very Secure FTP Daemon](#text00082.html_a2RN)∟ vsftpd Server ConfigurationProvides a tutorial example on how to configure vsftpd server to allow some local users to upload and download files in their own private Directories with FTP client programs.After installing vsftpd, the next step is to review and update its configuration. What I want is allow some local users to upload and download files in their own private directories with FTP client programs.1\. Locate vsftpd configuration files and create a backup.herong$ cd /etc/vsftpd

herong$ ls -l
total 20
-rw------- 1 root root  125 May 14  2019 ftpusers
-rw------- 1 root root  361 May 14  2019 user_list
-rw------- 1 root root 5098 May 14  2019 vsftpd.conf
-rwxr--r-- 1 root root  348 May 14  2019 vsftpd_conf_migrate.sh

herong$ sudo cp vsftpd.conf vsftpd.conf.bck
2\. Open vsftpd.conf to update or add settings as shown below:herong$ sudo vi vsftpd.conf

# Uncomment this to allow local users to log in.
# When SELinux is enforcing check for SE bool ftp_home_dir
local_enable=YES

#
# Uncomment this to enable any form of FTP write command.
write_enable=YES

#
# Default umask for local users is 077\. You may wish to change this to 022,
# if your users expect that (022 is used by most other ftpd's)
local_umask=022

...

# Activate logging of uploads/downloads.
xferlog_enable=YES

# You may override where the log file goes if you like. The default is shown
# below.
xferlog_file=/var/log/xferlog

# If you want, you can have your log file in standard ftpd xferlog format.
# Note that the default log file location is /var/log/xferlog in this case.
xferlog_std_format=NO

# You may specify an explicit list of local users to chroot() to their home
# directory. If chroot_local_user is YES, then this list becomes a list of
# users to NOT chroot().
# (Warning! chroot'ing can be very dangerous. If using chroot, make sure that
# the user does not have write access to the top level directory within the
# chroot)
chroot_local_user=YES

...

# Allow users in listed in vsftpd.user_list to access the server
userlist_enable=YES
userlist_file=/etc/vsftpd/user_list
userlist_deny=NO

# When users are connected to the server, redirect to their "ftp" directory
user_sub_token=$USER
local_root=/home/$USER/ftp

# Specify the range of ports for the passive connections
pasv_min_port=30000
pasv_max_port=31000
3\. Restart vsftpd server:herong$ sudo systemctl restart vsftpd
vsftpd server is ready. See next tutorial on how to set up user's ftp directory and permission.[Linux Tutorials - Herong's Tutorial Examples](#text00002.html_a2N5)∟ [vsftpd - Very Secure FTP Daemon](#text00082.html_a2RN)∟ Setup FTP Sub-Directory for Local UsersProvides a tutorial example on how to setup 'ftp' sub-directory for local users and allow them upload and download files using vsftpd on CentOS systems.With the vsftpd configuration presented in the previous tutorial, I am ready to create a "ftp" directory structure under my home directory for my to upload and download files.1\. Create ~/ftp sub-directory as my FTP home directory. Its ownship and permissions are changed to allow "vsftpd" to access.herong$ sudo mkdir /home/herong/ftp

herong$ sudo chown nobody:nobody /home/herong/ftp

herong$ sudo chmod a-w /home/herong/ftp

herong$ sudo ls -l /home/herong
...
dr-xr-xr-x 2 nobody nobody 6 Jun 23 17:03 ftp
2\. Create ~/ftp/files sub-directory with private access for uploading and downloading files.herong$ sudo mkdir /home/herong/ftp/files

herong$ sudo chown herong:herong /home/herong/ftp/files

herong$ sudo ls -lah /home/herong/ftp/
dr-xr-xr-x 3 nobody nobody 19 Jun 23 17:08 .
drwx------ 3 herong herong 94 Jun 23 17:07 ..
drwxr-xr-x 2 herong herong  6 Jun 23 17:08 files
3\. Add myself to the vsftpd allowed user list. Note that I am using "user_list" as the allowed user list, different than the default setting. So I have to remove all other users in this file.herong$ cd /etc/vsftpd

herong$ sudo cp user_list user_list.bck

herong$ sudo vi user_list

# vsftpd userlist
# If userlist_deny=NO, only allow users in this file
# If userlist_deny=YES (default), never allow users in this file, and
# do not even prompt for a password.
# Note that the default vsftpd pam config also checks /etc/vsftpd/ftpusers
# for users that are denied.
herong
4\. Restart vsftpd server:herong$ sudo systemctl restart vsftpd
My FTP access is ready. See next tutorial on how to test FTP access locally.[Linux Tutorials - Herong's Tutorial Examples](#text00002.html_a2N5)∟ [vsftpd - Very Secure FTP Daemon](#text00082.html_a2RN)∟ Test FTP Access Locally on CentOSProvides a tutorial example on how to use the 'ftp' client program to access the 'vsftpd' server locally on the same CentOS computer.After updating vsftpd configuration and setting up my "ftp" home directory, now I am ready to test my FTP access locally on the same CentOS computer as the vsftpd server.1\. Make sure the "ftp" client program is available.herong$ dnf info ftp
Last metadata expiration check: 6:29:59 ago on Tue 07 Jul 2020 11:12:35 PM EDT.
Available Packages
Name         : ftp
Version      : 0.17
Release      : 78.el8
Architecture : x86_64
Size         : 112 k
Source       : ftp-0.17-78.el8.src.rpm
Repository   : @System
From repo    : AppStream
Summary      : The standard UNIX FTP (File Transfer Protocol) client
URL          : ftp://ftp.linux.org.uk/pub/linux/Networking/netkit
License      : BSD with advertising
Description  : The ftp package provides the standard UNIX command-line FTP (File
             : Transfer Protocol) client.  FTP is a widely used protocol for
             : transferring files over the Internet and for archiving files.
             :
             : If your system is on a network, you should install ftp in order to do
             : file transfers.

herong$ sudo dnf install ftp
...
Downloading Packages:
ftp-0.17-78.el8.x86_64.rpm   373 kB/s |  70 kB     00:00

Installed:
  ftp-0.17-78.el8.x86_64

Complete!
2\. Connect to FTP server locally:herong$ ftp localhost
Trying ::1...
Connected to localhost (::1).
220 (vsFTPd 3.0.3)
Name (localhost:herong): herong
331 Please specify the password.
Password:
230 Login successful.
Remote system type is UNIX.
Using binary mode to transfer files.

ftp> dir
229 Entering Extended Passive Mode (|||30675|)
150 Here comes the directory listing.
drwxr-xr-x    2 1000     1000            6 Jun 23 09:08 files
226 Directory send OK.
3\. Upload a text file to the ./files sub-directory. Do not upload any files to the FTP home directory, which is configured only for the vsftpd daemon to access.ftp> put test.txt
local: test.txt remote: test.txt
229 Entering Extended Passive Mode (|||30283|)
150 Ok to send data.
226 Transfer complete.
637 bytes sent in 4e-05 secs (15925.00 Kbytes/sec)

ftp> dir
229 Entering Extended Passive Mode (|||30217|)
150 Here comes the directory listing.
-rw-r--r--    1 1000     1000          637 Jul 11 10:03 test.txt
226 Directory send O

ftp> cd ..
250 Directory successfully changed.

ftp> put test.txt
local: test.txt remote: test.txt
229 Entering Extended Passive Mode (|||30871|)
553 Could not create file.

ftp> exit
221 Goodbye.
4\. Check log file. It could be /var/log/xferlog or /var/log/xferlog:herong$ sudo tail /var/log/xferlog
... 1 ::ffff:192.168.1.11 0 /some.pdf b _ i r joe ftp 0 * i

herong$ sudo tail /var/log/vsftpd.log
... [pid 21901] CONNECT: Client "::ffff:192.168.1.11"
... [pid 21900] [herong] OK LOGIN: Client "::ffff:192.168.1.11"
... [pid 21969] [herong] OK UPLOAD: Client "::ffff:192.168.1.11",
   "/files/test.txt", 3547 bytes, 218.68Kbyte/sec
Cool! vsftpd daemon is working locally now. See the next tutorial on how to option the firewall for users to do FTP remotely.[Linux Tutorials - Herong's Tutorial Examples](#text00002.html_a2N5)∟ [vsftpd - Very Secure FTP Daemon](#text00082.html_a2RN)∟ Test FTP Access Remotely on CentOSProvides a tutorial example on how to update firewall on the vsftpd server (and its firewall gateway if it is served in the cloud) to open ports 21 and 30000-31000 for inbound connections.To allow users to upload and download files remotely, I need to open the firewall to allow users to upload and download files remotely using the vsftpd server on my CentOS computer.1\. Find the active zone of the firwall:herong$ sudo firewall-cmd --get-active-zones

public
  interfaces: eno1
2\. Add predefined "ftp" settings in the active zone "public" to receive incoming FTP connections.herong$ sudo firewall-cmd --zone=public --add-service=ftp
success
3\. Open a range of ports in the active zone to receive incoming FTP passive connections.herong$ sudo firewall-cmd --zone=public --add-port=30000-31000/tcp
success
4\. List all settings in the active zone "public":herong$ sudo firewall-cmd --zone=public --list-all
public (active)
  target: default
  icmp-block-inversion: no
  interfaces: eno1
  sources:
  services: cockpit dhcpv6-client ftp http ssh
  ports: 80/tcp 3306/tcp 30000-31000/tcp
  protocols:
  masquerade: no
  forward-ports:
  source-ports:
  icmp-blocks:
  ...
5\. Persist firewall changes to configuration files.herong$ sudo firewall-cmd --runtime-to-permanent
6\. Verify remote access by running an FTP client program on another computer on the same network, assuming that 192.168.1.3 is the IP address of vsftpd server computer.herong$ ftp 192.168.1.3
Connected to 192.168.1.3.
220 (vsFTPd 3.0.3)
Name (192.168.1.3:herong): herong
331 Please specify the password.
Password:
230 Login successful.
Remote system type is UNIX.
Using binary mode to transfer files.

ftp> dir
229 Entering Extended Passive Mode (|||30445|)
150 Here comes the directory listing.
drwxr-xr-x    2 1000     1000           22 Jul 11 10:03 files
226 Directory send OK.

ftp> cd files
250 Directory successfully changed.

ftp> dir
229 Entering Extended Passive Mode (|||30768|)
150 Here comes the directory listing.
-rw-r--r--    1 1000     1000          637 Jul 11 10:03 test.txt
226 Directory send OK.

ftp> get test.txt
local: test.txt remote: test.txt
229 Entering Extended Passive Mode (|||30673|)
150 Opening BINARY mode data connection for test.txt (637 bytes).
100% |*********************************|   637    3.41 MiB/s    00:00 ETA
226 Transfer complete.
637 bytes received in 00:00 (1.08 MiB/s)

ftp> exit
221 Goodbye.
Very good. Remote FTP access is ready!Note that if your server provided by an service provider in the cloud, you need open port 21 and 30000-31000 for inbound connections on the firewall gateway that protects your server.[Linux Tutorials - Herong's Tutorial Examples](#text00002.html_a2N5)∟ [vsftpd - Very Secure FTP Daemon](#text00082.html_a2RN)∟ Support FTP Over TLS on CentOSProvides a tutorial example on how to turn SSL/TLS support in vsftpd server on CentOS systems. A private-public key pair and a self-signed certificate is generated with the OpenSSL tool.If you allow users to upload and download files remotely over public networks, you need to enable SSL (Secure Socket Layer) on vsftpd to support FTP over TLS (Transport Layer Security). This will encrypt information exchanged between FTP client programs and the vsftpd server, included user's password and upload/download files.Here is what I did to enable SSL support for vsftpd on my CentOS computer.1\. Make sure "openssl" is available:herong$ sudo dnf info openssl

Available Packages
Name         : openssl
Epoch        : 1
Version      : 1.1.1c
Release      : 15.el8
Architecture : x86_64
Size         : 697 k
Source       : openssl-1.1.1c-15.el8.src.rpm
Repository   : BaseOS
Summary      : Utilities from the general purpose cryptography library with TLS
             : implementation
URL          : http://www.openssl.org/
License      : OpenSSL
Description  : The OpenSSL toolkit provides support for secure communications between
             : machines. OpenSSL includes a certificate management tool and shared
             : libraries which provide various cryptographic algorithms and
             : protocols.

herong$ sudo dnf install  openssl             
Upgraded:
  openssl-1:1.1.1c-15.el8.x86_64
  openssl-libs-1:1.1.1c-15.el8.x86_64
2\. Generate a private-public key pair and a self-signed certificate for the vsftpd server:herong$ cd /etc/vsftpd

herong$ sudo mkdir ssl
herong$ cd ssl

herong$ sudo openssl req -x509 -nodes -newkey rsa:2048 \
   -keyout vsftpd-private.pem -out vsftpd-cert.pem

Generating a RSA private key
............+++++
..+++++
writing new private key to 'vsftpd-private.pem'
-----
You are about to be asked to enter information that will be incorporated
into your certificate request.
What you are about to enter is what is called a Distinguished Name or a DN.
There are quite a few fields but you can leave some blank
For some fields there will be a default value,
If you enter '.', the field will be left blank.
-----
Country Name (2 letter code) [XX]:US
State or Province Name (full name) []:NY
Locality Name (eg, city) [Default City]:NY
Organization Name (eg, company) [Default Company Ltd]:HY
Organizational Unit Name (eg, section) []:IT
Common Name (eg, your name or your server's hostname) []:hy.centos
Email Address []:

herong$ sudo ls -l
total 8
-rw-r--r-- 1 root root 1294 Ju1 11 13:50 vsftpd-cert.pem
-rw------- 1 root root 1704 Ju1 11 13:49 vsftpd-private.pem
3\. Update vsftpd configuration to turn on SSL:herong$ cd /etc/vsftpd

herong$ sudo vi vsftpd.conf
...
ssl_enable=YES
rsa_cert_file=/etc/vsftpd/ssl/vsftpd-cert.pem
rsa_private_key_file=/etc/vsftpd/ssl/vsftpd-private.pem

allow_anon_ssl=NO
force_local_data_ssl=YES
force_local_logins_ssl=YES

ssl_sslv2=NO
ssl_sslv3=NO
ssl_tlsv1=NO
ssl_tlsv1_1=NO
ssl_tlsv1_2=YES
require_ssl_reuse=NO
ssl_ciphers=HIGH
4\. Restart vsftpd server.herong$ sudo systemctl restart vsftpd
5\. Test FTP over TLS with FileZilla client:Define a new site with the following:
  Protocal: FTP - File Transfer Protocol
  Host: 192.168.1.3
  Port:
  Encryption: Require explicit FTP over TLS
  ...

Click "Connect" and enter user/password

Click ok when you see a warning on server's certificate,
because it is signed by my-self, not by a certificate authority.

You see a successful connection in the log:
  Status:   Connecting to 192.168.1.10:21...
  Status:   Connection established, waiting for welcome message...
  Status:   Initializing TLS...
  Status:   Verifying certificate...
  Status:   TLS connection established.
  Status:   Logged in
  Status:   Retrieving directory listing...
  Status:   Directory listing of "/" successful
Nice! My FTP connections are secured now.[Linux Tutorials - Herong's Tutorial Examples](#text00002.html_a2N5)∟ [vsftpd - Very Secure FTP Daemon](#text00082.html_a2RN)∟ Disable SSH Access for FTP UsersProvides a tutorial example on how to disable SSH login access of a user on CentOS systems and allow his/her to use FTP service only for upload and download files.Some times, you may want to create a user and allow him/her to use the FTP service only, not allow him/her to use the SSH (Secure Shell) service to login to your CentOS system. This can be done by disabling his/her access in the sshd (SSH Daemon) configuration.Here is what I did to create "john" as FTP user and disable his access in the sshd configuration.1\. Create "john" as a user:herong$ sudo useradd john

herong$ sudo passwd john
Changing password for user john.
2\. Enable FTP access for John:herong$ sudo vi /etc/vsftpd/user_list
...
herong
john

herong$ sudo systemctl restart vsftpd
3\. Create FTP home directory for John:sudo mkdir /home/john/ftp
sudo chown nobody:nobody /home/john/ftp
sudo mkdir /home/john/ftp/private
sudo chown john:john /home/john/ftp/private
4\. Disable SSH access for John:herong$ sudo vi /etc/ssh/sshd_config
...
#  ForceCommand cvs server

UseDNS no
AddressFamily inet
SyslogFacility AUTHPRIV
PermitRootLogin yes
PasswordAuthentication yes
DenyUsers guest john

herong$ sudo systemctl restart sshd
5\. Verify SSH access. It should be denied.FYIs-MacBook-Pro:src herong$ ssh john@192.168.1.3
  john@192.168.1.3's password:
  Permission denied, please try again.
  john@192.168.1.3's password:
Now John can upload and download files remotely on my CentOS computer. But he can not SSH login remotely.[Linux Tutorials - Herong's Tutorial Examples](#text00002.html_a2N5)∟ GCC - C/C++ Compiler on Linux SystemsProvides introductions and tutorial examples about GCC C/C++ compilers. Topics include installing GCC C/C++ compilers; GCC compilation steps and settings; 'g++ -I' for include header files; g++ -l' for static/dynamic library files; 'g++ -shared' for building shared object (dynamic library) file; 'ldd' for checking dynamic library dependencies; 'make' tool for automation.[Install GCC C/C++ Compilers](#text00091.html_a2RY)["g++ --verbose" - GCC Compiler Steps and Settings](#text00092.html_a2RZ)["g++ -I..." and CPATH Environment Variable](#text00093.html_a2S0)["g++ -l..." to Link with Library Files](#text00094.html_a2S1)["g++ -c" and "ar src" to Build Static Library](#text00095.html_a2S2)["g++ -shared" to Build Dynamic Library](#text00096.html_a2S3)["ldd" - Dynamic Library Dependency Checker](#text00097.html_a2S4)["make" - Manage Program Build Process](#text00098.html_a2S5)Takeaways:

*   Installing the GCC C/C++ compilers can be done using "dnf install gcc" and "dnf install gcc-c++" commands on CentOS systems.
*   Dumping PHP environment information can be done by using the "php -i" command.
*   Include header file paths can be specified by "g++ -I..." option or CPATH environment variable.
*   Static and dynamic library files can be specified by "g++ -l... -l..." options.
*   Static and dynamic library file paths can be specified by "g++ -L..." option or LIBRARY_PATH environment variable at the link time.
*   Dynamic library file paths can be specified by LD_LIBRARY_PATH environment variable at the execution load time.
*   Dynamic library dependencies of any executable program can be listed by the "ldd" command.
*   Building (compiling, linking, ...) C/C++ programs can be automated by the "make" tool, which uses "Makefile" to define tasks involved in the building process.

[Linux Tutorials - Herong's Tutorial Examples](#text00002.html_a2N5)∟ [GCC - C/C++ Compiler on Linux Systems](#text00090.html_a2RX)∟ Install GCC C/C++ CompilersProvides a tutorial example on how to install GCC C/C++ compiler on CentOS systems.If you want develop your own C/C++, or compile third party C/C++ source code, you need install GCC C/C++ compilers as shown in this tutorial.1\. Install GCC C compiler:herong$ dnf info gcc
Available Packages
Name         : gcc
Version      : 8.3.1
Release      : 4.5.el8
Architecture : x86_64
Size         : 23 M
Source       : gcc-8.3.1-4.5.el8.src.rpm
Repository   : AppStream
Summary      : Various compilers (C, C++, Objective-C, ...)
URL          : http://gcc.gnu.org
License      : GPLv3+ and GPLv3+ with exceptions and GPLv2+ with ...
Description  : The gcc package contains the GNU Compiler Collection
             : version 8\. You'll need this package in order to compile
             : C code.

herong$ sudo dnf install gcc
...
Installed:
  gcc-8.3.1-4.5.el8.x86_64
  annobin-8.78-1.el8.x86_64
  cpp-8.3.1-4.5.el8.x86_64
  isl-0.16.1-6.el8.x86_64
  glibc-devel-2.28-72.el8.x86_64
  glibc-headers-2.28-72.el8.x86_64
  kernel-headers-4.18.0-147.5.1.el8_1.x86_64
  libxcrypt-devel-4.1.1-4.el8.x86_64
2\. Verify GCC installation:(cpp - The C preprocessor)
herong$ cpp --version
cpp (GCC) 8.3.1 20190507 (Red Hat 8.3.1-4)
Copyright (C) 2018 Free Software Foundation, Inc.

(gcc - The GNU project C compiler)
herong$ gcc --version
gcc (GCC) 8.3.1 20190507 (Red Hat 8.3.1-4)
Copyright (C) 2018 Free Software Foundation, Inc.

(cc - Alias of gcc)
herong$ ls -l /usr/bin/cc
lrwxrwxrwx. 1 root root 3 Nov  5 23:36 /usr/bin/cc -> gcc
3\. Compile and run a C program, hello.c:herong$ vi hello.c
#include<stdio.h>
int main(void) {
 printf("Hello world! - From C.\n");
 return 0;
}

herong$ gcc hello.c

herong$ ./a.out
Hello world! - From C.
4\. Install GCC C++ compiler:herong$ dnf info gcc-c++
Available Packages
Name         : gcc-c++
Version      : 8.3.1
Release      : 4.5.el8
Architecture : x86_64
Size         : 12 M
Source       : gcc-8.3.1-4.5.el8.src.rpm
Repository   : AppStream
Summary      : C++ support for GCC
URL          : http://gcc.gnu.org
License      : GPLv3+ and GPLv3+ with exceptions and GPLv2+ with ...
Description  : This package adds C++ support to the GNU Compiler Collection.
             : It includes support for most of the current C++ specification,
             : including templates and exception handling.

erong@localhost build]$ sudo dnf install gcc-c++
...
Installed:
  gcc-c++-8.3.1-4.5.el8.x86_64
  libstdc++-devel-8.3.1-4.5.el8.x86_64

Complete!
5\. Verify GCC installation:(g++ - The GNU project C++ compiler)
herong$ gcc --version
g++ (GCC) 8.3.1 20190507 (Red Hat 8.3.1-4)
Copyright (C) 2018 Free Software Foundation, Inc.
6\. Compile and run a C++ program, hello.c:herong$ vi hello.cpp
#include "iostream"
int main(void) {
    std::cout <<  "Hello world! From C++.\n";
    return 0;
}

herong$ g++ hello.cpp

herong$ ./a.out
Hello world! From C++.
[Linux Tutorials - Herong's Tutorial Examples](#text00002.html_a2N5)∟ [GCC - C/C++ Compiler on Linux Systems](#text00090.html_a2RX)∟ "g++ --verbose" - GCC Compiler Steps and SettingsProvides a tutorial example on how to dump GCC compiler steps and settings using the 'g++ --verbose' command option.If you are running into issues with the GCC C++ compiler, you may want to use the "g++ --verbose" to dump all current settings from the compiler.herong$ g++ --verbose hello.cpp

...
Target: x86_64-redhat-linux
Configured with: ../configure --enable-bootstrap --enable-languages=c,c++,fortran,lto ...

/usr/libexec/gcc/x86_64-redhat-linux/8/cc1plus -quiet -v -D_GNU_SOURCE hello.cpp
   -quiet -dumpbase hello.cpp -mtune=generic -march=x86-64 -auxbase hello -version
   -o /tmp/cceaNqFM.s
ignoring nonexistent directory "/usr/lib/gcc/x86_64-redhat-linux/8/include-fixed"
ignoring nonexistent directory "/usr/x86_64-redhat-linux/include"
#include "..." search starts here:
#include <...>  search starts here:
 /usr/include/c++/8
 /usr/include/c++/8/x86_64-redhat-linux
 /usr/include/c++/8/backward
 /usr/lib/gcc/x86_64-redhat-linux/8/include
 /usr/local/include
 /usr/include
End of search list.

as -v --64 -o /tmp/ccGgvc09.o /tmp/cceaNqFM.s

COMPILER_PATH=/usr/libexec/gcc/x86_64-redhat-linux/8/: ...
LIBRARY_PATH=/usr/lib/gcc/x86_64-redhat-linux/8/:...

/usr/libexec/gcc/x86_64-redhat-linux/8/collect2 -plugin \
   /usr/libexec/gcc/x86_64-redhat-linux/8/liblto_plugin.so ...
So the "g++" command actually runs 3 commands: cc1plus, as, collect2.[Linux Tutorials - Herong's Tutorial Examples](#text00002.html_a2N5)∟ [GCC - C/C++ Compiler on Linux Systems](#text00090.html_a2RX)∟ "g++ -I..." and CPATH Environment VariableProvides a tutorial example on how to use 'g++ -I...' option and/or CPATH environment variable to specify paths of include header files for GCC compiler.If you are compiling a C/C++ program that uses custom header files, you need to specify the path name where the header files are located.1\. Create a simple header file, ./include/myheader.h:herong$ vi ./include/myheader.h

#define Name "herong"
2\. Create a C++ program file that uses the header file:herong$ vi HeaderTest.cpp

#include "iostream"
#include "string"
#include "myheader.h"
int main(void) {
  std::string who (Name);  
  std::cout <<  "Hello " <<  who <<  "!" <<  std::endl;
  return 0;
}
3\. Compile it without specifying the include path:herong$ g++ HeaderTest.cpp
HeaderTest.cpp:3:10: fatal error: myheader.h: No such file or directory
 #include "myheader.h"
          ^~~~~~~~~~~~
compilation terminated.
4\. Compile it with "-I ..." option to specify include path:herong$ g++ -I ./include -v HeaderTest.cpp

...
#include "..." search starts here:
#include <...>  search starts here:
 ./include
 /usr/include/c++/8
 /usr/include/c++/8/x86_64-redhat-linux
 /usr/include/c++/8/backward
 /usr/lib/gcc/x86_64-redhat-linux/8/include
 /usr/local/include
 /usr/include
End of search list.
...

herong$ ./a.out
Hello herong!
5\. Compile it with "CPATH=..." environment variable to specify include path:herong$ export CPATH=./include

herong$ g++ -v HeaderTest.cpp

...
#include "..." search starts here:
#include <...>  search starts here:
 ./include
 /usr/include/c++/8
 /usr/include/c++/8/x86_64-redhat-linux
 /usr/include/c++/8/backward
 /usr/lib/gcc/x86_64-redhat-linux/8/include
 /usr/local/include
 /usr/include
End of search list.
...

herong$ ./a.out
Hello herong!
Now I know the "-I ..." option or "CPATH" environment variable is adding more paths to the GCC default list to search for include header files.[Linux Tutorials - Herong's Tutorial Examples](#text00002.html_a2N5)∟ [GCC - C/C++ Compiler on Linux Systems](#text00090.html_a2RX)∟ "g++ -l..." to Link with Library FilesProvides a tutorial example on how to use 'g++ -static' and 'g++ -l...' options to link your program with static or dynamic library files.GCC C/C++ compilers support 2 types of library files:1\. Static Library Files - Static library files are also called Archive files and have .a file extension on Linux systems. When you link your program with static library files, all objects referenced by your program will be verified and copied into the final executable file. This makes the executable file much bigger. But it makes the execution easier, since static library files are no longer needed at the execution time.2\. Dynamic Library Files - Static library files are also called Shared Object files and have .so file extension on Linux systems. When you link your program with Dynamic library files, all objects referenced by your program will be verified but not copied into the final executable file. This makes the executable file much smaller. But it makes the execution harder, since dynamic library files needs to be loaded into CPU together with your executable file.The GCC C/C++ compilers allows you to control which type of library files to use and specify library file names using "-static" and "-l..." options. Note that the actual library file name is computed from whatever specified in the "-l..." option with "lib" prefix and .a or .so extension.Example 1 - the following command links 2 static library files, libAbc.a and libXyz.a in the current directory:herong$ g++ -static -lAbc -lXyz myProgram.cpp
Example 2 - the following command links 2 static library files, libAbc.so and libXyz.so in the current directory:herong$ g++ -lAbc -lXyz myProgram.cpp
[Linux Tutorials - Herong's Tutorial Examples](#text00002.html_a2N5)∟ [GCC - C/C++ Compiler on Linux Systems](#text00090.html_a2RX)∟ "g++ -c" and "ar src" to Build Static LibraryProvides a tutorial example on how to use 'g++ -c' and 'ar src' commands to compile your code and to build static library file on Linux systems.If you want to build your own static library files, you need to do it in two steps:

*   Compile source code files and generate object code files with "g++ -c" command.
*   Build an archive file as the static library file from object code files with "ar cs" command.

Here is what I did to build by first static library file: libMyStatic.a:1\. Create a source code file, MyStatic.cppherong$ cat MyStatic.cpp

// MyStatic.cpp
#include "iostream"
void myStaticFunc() {
  std::cout <<  "Running myStaticFunc()..." <<  std::endl;
}
2\. Compile source code file, MyStatic.cpp, into object code file, MyStatic.o:herong$ g++ -c MyStatic.cpp

herong$ ls -l MyStatic.*
-rw-rw-r--. 1 herong herong  117 Apr 10 23:50 MyStatic.cpp
-rw-rw-r--. 1 herong herong 2744 Apr 10 23:52 MyStatic.o
3\. Create static library file, libMyStatic.a from object code file, MyStatic.o:herong$ ar src libMyStatic.a MyStatic.o

herong$ ls -l *MyStatic.*
-rw-rw-r--. 1 herong herong 2898 Apr 10 23:54 libMyStatic.a
-rw-rw-r--. 1 herong herong  117 Apr 10 23:50 MyStatic.cpp
-rw-rw-r--. 1 herong herong 2744 Apr 10 23:52 MyStatic.o

herong$ ar t libMyStatic.a
MyStatic.o
4\. Create a calling program, MyStaticTest.cpp:herong$ cat MyStaticTest.cpp

// MyStaticTest.cpp
#include "iostream"
extern void myStaticFunc();
int main() {
  std::cout <<  "Calling myStaticFunc()..." <<  std::endl;
  myStaticFunc();
}
5\. Link MyStaticTest.cpp with MyStatic.o directly to confirm that the test program is working.herong$ g++ MyStatic.o MyStaticTest.cpp

herong$ ./a.out
Calling myStaticFunc()...
Running myStaticFunc()...
6\. Link MyStaticTest.cpp with libMyStatic.a without giving location path:herong$ g++ -lMyStatic MyStaticTest.cpp
/usr/bin/ld: cannot find -lMyStatic
7\. Link MyStaticTest.cpp with libMyStatic.a with giving location path using the "g++ -L ..." option. I can also use the "LIBRARY_PATH" environment variable instead of "g++ -L ...".herong$ g++ -L . -lMyStatic MyStaticTest.cpp
/tmp/cciFWV0h.o: In function `main':
MyStaticTest.cpp:(.text+0x21): undefined reference to `myStaticFunc()'
8\. Force GCC to do static library linking:herong$ g++ -static -L . -lMyStatic MyStaticTest.cpp
/usr/bin/ld: cannot find -lstdc++
/usr/bin/ld: cannot find -lm
/usr/bin/ld: cannot find -lc
collect2: error: ld returned 1 exit status
Looks like I am still missing somethings to make GCC working with static library files.By the way, you can use "LIBRARY_PATH" environment variable to specify static library file path instead of the "g++ -L ..." option.[Linux Tutorials - Herong's Tutorial Examples](#text00002.html_a2N5)∟ [GCC - C/C++ Compiler on Linux Systems](#text00090.html_a2RX)∟ "g++ -shared" to Build Dynamic LibraryProvides a tutorial example on how to use 'g++ -shared' commands to compile your code and to build dynamic library file on Linux systems.If you want to build your own dynamic library files, you need to do it with the "g++ -shared" command.Here is what I did to build by first static library file: libMyDynamic.so:1\. Create a source code file, MyDynamic.cppherong$ cat MyDynamic.cpp

// MyDynamic.cpp
#include "iostream"
void myDynamicFunc() {
  std::cout <<  "Running myDynamicFunc()..." <<  std::endl;
}
2\. Compile source code file, MyDynamic.cpp, into a dynamic library file:herong$ g++ -shared -o libMyDynamic.so MyDynamic.cpp
/usr/bin/ld: /tmp/ccG05g0J.o: relocation R_X86_64_32 against `.rodata'
   can not be used when making a shared object; recompile with -fPIC
/usr/bin/ld: final link failed: Nonrepresentable section on output
3\. Re-compile it again with "-fPIC" option as suggested:herong$ g++ -shared -fPIC -o libMyDynamic.so MyDynamic.cpp

herong$ ls -l *MyDynamic*
-rwxrwxr-x. 1 herong herong 8872 Apr 13 01:57 libMyDynamic.so
-rw-rw-r--. 1 herong herong  120 Apr 13 01:53 MyDynamic.cpp
4\. Create a calling program, MyDynamicTest.cpp:herong$ cat MyDynamicTest.cpp

// MyDynamicTest.cpp
#include "iostream"
extern void myDynamicFunc();
int main() {
  std::cout <<  "Calling myDynamicFunc()..." <<  std::endl;
  myDynamicFunc();
}
5\. Link MyDynamicTest.cpp with libMyDynamic.so without giving location path:herong$ g++ -lMyDynamic MyDynamicTest.cpp
/usr/bin/ld: cannot find -lMyDynamic
6\. Link MyDynamicTest.cpp with libMyDynamic.so with giving location path using the "g++ -L ..." option. I can also use the "LIBRARY_PATH" environment variable instead of "g++ -L ...".herong$ g++ -L . -lMyDynamic MyDynamicTest.cpp

herong$ ./a.out
Calling myDynamicFunc()...
Running myDynamicFunc()...
7\. Logout and login to run the program again. I got an error as expected, because libMyDynamic.so is no longer loaded in the CPU, and the program loader has no idea where to find it.herong$ ./a.out
./a.out: error while loading shared libraries: libMyDynamic.so:
   cannot open shared object file: No such file or directory
8\. Run it again with LD_LIBRARY_PATH set to the dynamic library path:herong$ export LD_LIBRARY_PATH=.

herong$ ./a.out
Calling myDynamicFunc()...
Running myDynamicFunc()...
Cool. GCC C/C++ compiler is much easier to work with dynamic libraries than static libraries in Linux systems.[Linux Tutorials - Herong's Tutorial Examples](#text00002.html_a2N5)∟ [GCC - C/C++ Compiler on Linux Systems](#text00090.html_a2RX)∟ "ldd" - Dynamic Library Dependency CheckerProvides a tutorial example on how to use the 'ldd' tool to list dynamic library dependencies of any executable files, including dynamic library files on Linux systems.Most of executable programs use dynamic libraries because of two main benefits:

*   Makes the executable program file smaller because dependent program code is stored in the external dynamic library files.
*   Reduces loading time and memory usage because dependent program code is loaded separately and can be shared by multiple programs.

If you want to know which dynamic libraries are used by an executable program, you can use the "ldd" command on Linux systems. Here are some usage examples of the "ldd" command.1\. List dynamic library dependency of the "ls" system command program. I see 8 system libraries.herong$ which ls
  /usr/bin/ls

herong$ ldd /bin/ls
  linux-vdso.so.1 (0x00007ffd03779000)
  libselinux.so.1 => /lib64/libselinux.so.1 (0x00007fe8a18cd000)
  libcap.so.2 => /lib64/libcap.so.2 (0x00007fe8a16c7000)
  libc.so.6 => /lib64/libc.so.6 (0x00007fe8a1304000)
  libpcre2-8.so.0 => /lib64/libpcre2-8.so.0 (0x00007fe8a1080000)
  libdl.so.2 => /lib64/libdl.so.2 (0x00007fe8a0e7c000)
  /lib64/ld-linux-x86-64.so.2 (0x00007fe8a1d1b000)
  libpthread.so.0 => /lib64/libpthread.so.0 (0x00007fe8a0c5c000)
2\. List dynamic library dependency of my own C program compiled from hello.c. I see 2 Linux system libraries and 1 C library.herong$ gcc -o hello hello.c

herong$ ./hello
Hello world! - From C.

herong$ ldd hello
  linux-vdso.so.1 (0x00007ffed5fc6000)
  libc.so.6 => /lib64/libc.so.6 (0x00007f3f1f26f000)
  /lib64/ld-linux-x86-64.so.2 (0x00007f3f1f632000)
3\. List dynamic library dependency of my own C++ program compiled from hello.cpp. I see 3 more libraries.herong$ g++ -o hello hello.cpp

herong$ ./hello
Hello world! From C++.

herong$ ldd hello
  linux-vdso.so.1 (0x00007ffec33c2000)
  libstdc++.so.6 => /lib64/libstdc++.so.6 (0x00007fc85b58c000)
  libm.so.6 => /lib64/libm.so.6 (0x00007fc85b20a000)
  libgcc_s.so.1 => /lib64/libgcc_s.so.1 (0x00007fc85aff2000)
  libc.so.6 => /lib64/libc.so.6 (0x00007fc85ac2f000)
  /lib64/ld-linux-x86-64.so.2 (0x00007fc85b921000)
4\. List dynamic library dependency of my own program that uses my own dynamic library. I see my dynamic library libMyDynamic.so in the list.herong$ g++ -L . -lMyDynamic -o MyDynamicTest MyDynamicTest.cpp

herong$ export LD_LIBRARY_PATH=.

herong$ ./MyDynamicTest
Calling myDynamicFunc()...
Running myDynamicFunc()...

herong$ ldd MyDynamicTest
  linux-vdso.so.1 (0x00007ffe01126000)
  libMyDynamic.so => ./libMyDynamic.so (0x00007ff04c617000)
  libstdc++.so.6 => /lib64/libstdc++.so.6 (0x00007ff04c282000)
  libm.so.6 => /lib64/libm.so.6 (0x00007ff04bf00000)
  libgcc_s.so.1 => /lib64/libgcc_s.so.1 (0x00007ff04bce8000)
  libc.so.6 => /lib64/libc.so.6 (0x00007ff04b925000)
  /lib64/ld-linux-x86-64.so.2 (0x00007ff04c819000)
5\. If LD_LIBRARY_PATH environment variable is not set properly, some dynamic libraries will be listed as "not found".herong$ export LD_LIBRARY_PATH=/tmp

herong$ ldd MyDynamicTest
  linux-vdso.so.1 (0x00007ffe9e734000)
  libMyDynamic.so => not found
  libstdc++.so.6 => /lib64/libstdc++.so.6 (0x00007efc7393e000)
  libm.so.6 => /lib64/libm.so.6 (0x00007efc735bc000)
  libgcc_s.so.1 => /lib64/libgcc_s.so.1 (0x00007efc733a4000)
  libc.so.6 => /lib64/libc.so.6 (0x00007efc72fe1000)
  /lib64/ld-linux-x86-64.so.2 (0x00007efc73cd3000)
6\. "ldd" works on dynamic library files (*.so files) too, because they are executable files.herong$ g++ -shared -fPIC -o libMyDynamic.so MyDynamic.cpp

herong$ ldd libMyDynamic.so
  linux-vdso.so.1 (0x00007ffd7f35d000)
  libstdc++.so.6 => /lib64/libstdc++.so.6 (0x00007f9e27b19000)
  libm.so.6 => /lib64/libm.so.6 (0x00007f9e27797000)
  libgcc_s.so.1 => /lib64/libgcc_s.so.1 (0x00007f9e2757f000)
  libc.so.6 => /lib64/libc.so.6 (0x00007f9e271bc000)
  /lib64/ld-linux-x86-64.so.2 (0x00007f9e280b0000)
7\. Sorry, "ldd" does not work on object files (.o files), because they are not executable files.herong$ g++ -c -o hello.o hello.cpp

herong$ ldd hello.o
ldd: warning: you do not have execution permission for './hello.o'
  not a dynamic executable
[Linux Tutorials - Herong's Tutorial Examples](#text00002.html_a2N5)∟ [GCC - C/C++ Compiler on Linux Systems](#text00090.html_a2RX)∟ "make" - Manage Program Build ProcessProvides a tutorial example on how to use the 'make' tool to manage the build process of large programs that have multiple components.What Is "make" - "make" is a utility tool to manage the build (compile, link, install, test, etc.) process of large programs that have multiple components. "make" can determine automatically which source code files of the program need to be recompiled, and issue the commands to recompile them. You can actually use "make" to describe any task where some files must be updated automatically from others whenever the others change.You can follow this tutorial to install and verify the "make" tool on CentOS 8 systems.1\. Install "make":herong$ sudo dnf install make
Package make-1:4.2.1-9.el8.x86_64 is already installed.
Dependencies resolved.
Nothing to do.
Complete!

herong$ sudo dnf info make
Installed Packages
Name         : make
Epoch        : 1
Version      : 4.2.1
Release      : 9.el8
Architecture : x86_64
Size         : 1.4 M
Source       : make-4.2.1-9.el8.src.rpm
Repository   : @System
From repo    : BaseOS
Summary      : A GNU tool which simplifies the build process for users
URL          : http://www.gnu.org/software/make/
License      : GPLv3+
Description  : A GNU tool for controlling the generation of executables and other
             : non-source files of a program from the program's source files. Make
             : allows users to build and install packages without any significant
             : knowledge about the details of the build process. The details about
             : how the program should be built are provided for make in the program's
             : makefile.
2\. Verify "make" version:herong$ make --version

GNU Make 4.2.1
Built for x86_64-redhat-linux-gnu
Copyright (C) 1988-2016 Free Software Foundation, Inc.
3\. Create a "Makefile" with one task:herong$ cat Makefile

compile: hello.cpp
  g++ -o hello hello.cpp
4\. Run the task specified in the "Makefile":herong$ make compile

g++ -o hello hello.cpp
5\. Verify result:herong$ ./hello
Hello world! From C++.
Ok. I can use the "make" tool to automate any tasks on my CentOS 8 computer now.[Linux Tutorials - Herong's Tutorial Examples](#text00002.html_a2N5)∟ Conda - Environment and Package ManagerProvides introductions and tutorial examples about Conda environments. Topics include installing Conda from the Miniconda package; starting/ending Conda 'base' environment; installing Conda packages.[What Is Conda](#text00100.html_a2S7)[Install Miniconda 3](#text00101.html_a2S8)[Introduction to Conda Environment](#text00102.html_a2S9)Takeaways:

*   Conda is a powerful open source environment and package manager that allows you to install multiple environments for multiple versions of software packages and their dependencies and switching easily between them.
*   Miniconda is the smallest distribution package for Conda.
*   Conda distribution package comes with a "base" Conda environment.
*   A Conda environment is an independent shell environment for a specific version of Python script engine and its libraries.
*   "Conda" commands allows you to manage Conda environments and create new ones.

[Linux Tutorials - Herong's Tutorial Examples](#text00002.html_a2N5)∟ [Conda - Environment and Package Manager](#text00099.html_a2S6)∟ What Is CondaProvides a quick introduction on Conda, which is a powerful open source environment and packager manager that allows you to install multiple environments for multiple versions of software packages and their dependencies and switching easily between them.What Is Conda? Conda is a powerful open source environment and package manager that allows you to install multiple environments for multiple versions of software packages and their dependencies and switching easily between them. Conda was originally developed to solve difficult Python package management challenges.Conda is included in two distribution packages:

*   Miniconda - Includes Conda and its dependencies including Python.
*   Anaconda - Includes Conda and 7,500 popular open-source packages, including Python, R, Jupyter/IPython, ggplot2, NumPy, SciPy, Pandas, etc.

For most users, download and install Miniconda is good enough. If you need any additional packages, you can download and install them individually from the Conda package repository.For more information, visit Conda Website at [https://www.anaconda.com](https://www.anaconda.com) .[Linux Tutorials - Herong's Tutorial Examples](#text00002.html_a2N5)∟ [Conda - Environment and Package Manager](#text00099.html_a2S6)∟ Install Miniconda 3Provides a tutorial example on how to install Miniconda 3\. Once installed, you can start and end the Conda 'base' environment similar to a Linux shell.To get started with Conda, you can follow this tutorial to install Miniconda.1\. Download Miniconda installation shell script:herong$ export miniconda=Miniconda3-latest-Linux-x86_64.sh
herong$ curl https://repo.anaconda.com/miniconda/$miniconda > $miniconda
herong$ ls -l
  93052469 Aug 24 02:06 Miniconda3-latest-Linux-x86_64.sh
2\. Run the installation shell script:herong$ bash Miniconda3-latest-Linux-x86_64.sh

...
In order to continue the installation process, please review the license
agreement.
Please, press ENTER to continue
>>> ENTER

Do you accept the license terms? [yes|no]
[no] >>> yes

Miniconda3 will now be installed into this location:
/home/herong/miniconda3

  - Press ENTER to confirm the location
  - Press CTRL-C to abort the installation
  - Or specify a different location below

[/home/herong/miniconda3] >>> ENTER
PREFIX=/home/herong/anaconda3

The following NEW packages will be INSTALLED:
  _libgcc_mutex      pkgs/main/linux-64::_libgcc_mutex-0.1-main
  ca-certificates    pkgs/main/linux-64::ca-certificates-2020.1.1-0
  certifi            pkgs/main/linux-64::certifi-2020.4.5.1-py38_0
  cffi               pkgs/main/linux-64::cffi-1.14.0-py38he30daa8_1
  chardet            pkgs/main/linux-64::chardet-3.0.4-py38_1003
  conda              pkgs/main/linux-64::conda-4.8.3-py38_0
  conda-package-han~ pkgs/main/linux-64::conda-package-handling-1.6.1-py38h7b6447c_0
  cryptography       pkgs/main/linux-64::cryptography-2.9.2-py38h1ba5d50_0
  idna               pkgs/main/noarch::idna-2.9-py_1
  ld_impl_linux-64   pkgs/main/linux-64::ld_impl_linux-64-2.33.1-h53a641e_7
  libedit            pkgs/main/linux-64::libedit-3.1.20181209-hc058e9b_0
  libffi             pkgs/main/linux-64::libffi-3.3-he6710b0_1
  libgcc-ng          pkgs/main/linux-64::libgcc-ng-9.1.0-hdf63c60_0
  libstdcxx-ng       pkgs/main/linux-64::libstdcxx-ng-9.1.0-hdf63c60_0
  ncurses            pkgs/main/linux-64::ncurses-6.2-he6710b0_1
  openssl            pkgs/main/linux-64::openssl-1.1.1g-h7b6447c_0
  pip                pkgs/main/linux-64::pip-20.0.2-py38_3
  pycosat            pkgs/main/linux-64::pycosat-0.6.3-py38h7b6447c_1
  pycparser          pkgs/main/noarch::pycparser-2.20-py_0
  pyopenssl          pkgs/main/linux-64::pyopenssl-19.1.0-py38_0
  pysocks            pkgs/main/linux-64::pysocks-1.7.1-py38_0
  python             pkgs/main/linux-64::python-3.8.3-hcff3b4d_0
  readline           pkgs/main/linux-64::readline-8.0-h7b6447c_0
  requests           pkgs/main/linux-64::requests-2.23.0-py38_0
  ruamel_yaml        pkgs/main/linux-64::ruamel_yaml-0.15.87-py38h7b6447c_0
  setuptools         pkgs/main/linux-64::setuptools-46.4.0-py38_0
  six                pkgs/main/linux-64::six-1.14.0-py38_0
  sqlite             pkgs/main/linux-64::sqlite-3.31.1-h62c20be_1
  tk                 pkgs/main/linux-64::tk-8.6.8-hbc83047_0
  tqdm               pkgs/main/noarch::tqdm-4.46.0-py_0
  urllib3            pkgs/main/linux-64::urllib3-1.25.8-py38_0
  wheel              pkgs/main/linux-64::wheel-0.34.2-py38_0
  xz                 pkgs/main/linux-64::xz-5.2.5-h7b6447c_0
  yaml               pkgs/main/linux-64::yaml-0.1.7-had09818_2
  zlib               pkgs/main/linux-64::zlib-1.2.11-h7b6447c_3

installation finished.

Do you wish the installer to initialize Miniconda3
by running conda init? [yes|no]
[no] >>> yes
no change     /home/herong/miniconda3/condabin/conda
no change     /home/herong/miniconda3/bin/conda
no change     /home/herong/miniconda3/bin/conda-env
no change     /home/herong/miniconda3/bin/activate
no change     /home/herong/miniconda3/bin/deactivate
no change     /home/herong/miniconda3/etc/profile.d/conda.sh
no change     /home/herong/miniconda3/etc/fish/conf.d/conda.fish
no change     /home/herong/miniconda3/shell/condabin/Conda.psm1
no change     /home/herong/miniconda3/shell/condabin/conda-hook.ps1
no change     /home/herong/miniconda3/lib/python3.8/site-packages/xontrib/conda.xsh
no change     /home/herong/miniconda3/etc/profile.d/conda.csh
modified      /home/herong/.bashrc

==> For changes to take effect, close and re-open your current shell. <==

If you'd prefer that conda's base environment not be activated on startup,
   set the auto_activate_base parameter to false:

conda config --set auto_activate_base false

Thank you for installing Miniconda3!
3\. If you skipped the initialize step by mistake, you can do it with the conda command:herong$ ~/miniconda3/bin/conda init

(same output as above)
4\. Log out and log in to use the Conda environment. By default, the "base" environment is activated at login time. Several environment variables are added or updated to control this environment.(logout and login)
(base) herong$ set | grep miniconda3

CONDA_EXE=/home/herong/miniconda3/bin/conda
CONDA_INTERNAL_OLDPATH=/home/herong/miniconda3/condabin:/home/herong/...
CONDA_PREFIX=/home/herong/miniconda3
CONDA_PYTHON_EXE=/home/herong/miniconda3/bin/python
PATH=/home/herong/miniconda3/bin:/home/herong/miniconda3/condabin:...
SYSP=/home/herong/miniconda3
5\. To quit from this Conda "base" environment and go back to normal Linux environment, run the "conda deactivate" command.(base) herong$ conda deactivate
herong$
6\. To enter into the Conda "base" environment again, run the "conda activate" command.herong$ conda activate
(base) herong$
7.If you'd prefer that conda's base environment not be activated on startup, set the auto_activate_base parameter to false:(base) herong$ conda config --set auto_activate_base false

(logout and login)
herong$
[Linux Tutorials - Herong's Tutorial Examples](#text00002.html_a2N5)∟ [Conda - Environment and Package Manager](#text00099.html_a2S6)∟ Introduction to Conda EnvironmentProvides a quick introduction about the Conda environment, its file directories and command programs. Steps to verify its Python version, and install new packages.After installing Miniconda, we should take a quick tour on the "base" environment it offers.1\. Conda "base" environment program files are located in ~/miniconda3. They look very much like a mini operating system.drwxrwxr-x.  2 herong herong  4096 bin
drwxrwxr-x.  2 herong herong    30 compiler_compat
drwxrwxr-x.  2 herong herong    19 condabin
drwxrwxr-x.  2 herong herong  4096 conda-meta
drwxrwxr-x.  2 herong herong     6 envs
drwxrwxr-x.  4 herong herong    35 etc
drwxrwxr-x.  9 herong herong  4096 include
drwxrwxr-x. 15 herong herong  4096 lib
-rw-r--r--.  1 herong herong 11245 May 19 15:29 LICENSE.txt
drwxrwxr-x. 61 herong herong  8192 pkgs
drwxrwxr-x. 10 herong herong   116 share
drwxrwxr-x.  3 herong herong    22 shell
drwxrwxr-x.  3 herong herong   146 ssl
drwxrwxr-x.  3 herong herong    21 x86_64-conda_cos6-linux-gnu
2\. Commands (some of them override system commands) provided by Conda are located in ~/miniconda3/bin.lrwxrwxrwx. 1 herong herong        8 2to3 -> 2to3-3.8
-rwxrwxr-x. 1 herong herong      114 2to3-3.8
-rwxrwxr-x. 1 herong herong      197 activate
lrwxrwxrwx. 1 herong herong        3 captoinfo -> tic
-rwxrwxr-x. 1 herong herong      243 chardetect
-rwxrwxr-x. 2 herong herong    14288 clear
-rwxrwxr-x. 1 herong herong      524 conda
-rwxrwxr-x. 1 herong herong      161 conda-env
-rwxrwxr-x. 1 herong herong      247 cph
-rwxrwxr-x. 1 herong herong     6214 c_rehash
-rwxrwxr-x. 1 herong herong      285 deactivate
-rwxrwxr-x. 1 herong herong      252 easy_install
lrwxrwxrwx. 1 herong herong        7 idle3 -> idle3.8
-rwxrwxr-x. 1 herong herong      112 idle3.8
-rwxrwxr-x. 2 herong herong    63512 infocmp
lrwxrwxrwx. 1 herong herong        3 infotocap -> tic
lrwxrwxrwx. 1 herong herong        2 lzcat -> xz
...
-rwxrwxr-x. 2 herong herong    21216 lzmadec
-rwxrwxr-x. 1 herong herong    21128 lzmainfo
lrwxrwxrwx. 1 herong herong        6 lzmore -> xzmore
-rwxrwxr-x. 1 herong herong     8076 ncursesw6-config
-rwxrwxr-x. 2 herong herong   836336 openssl
-rwxrwxr-x. 1 herong herong      243 pip
lrwxrwxrwx. 1 herong herong        8 pydoc -> pydoc3.8
lrwxrwxrwx. 1 herong herong        8 pydoc3 -> pydoc3.8
-rwxrwxr-x. 1 herong herong       97 pydoc3.8
lrwxrwxrwx. 1 herong herong        9 python -> python3.8
lrwxrwxrwx. 1 herong herong        9 python3 -> python3.8
-rwxrwxr-x. 2 herong herong 14707712 python3.8
-rwxrwxr-x. 1 herong herong     3498 python3.8-config
lrwxrwxrwx. 1 herong herong       16 python3-config -> python3.8-config
lrwxrwxrwx. 1 herong herong        4 reset -> tset
-rwxrwxr-x. 2 herong herong  1508240 sqlite3
-rwxrwxr-x. 2 herong herong    29841 sqlite3_analyzer
-rwxrwxr-x. 2 herong herong    14280 tabs
lrwxrwxrwx. 1 herong herong        8 tclsh -> tclsh8.6
-rwxrwxr-x. 2 herong herong    20616 tclsh8.6
-rwxrwxr-x. 2 herong herong    88128 tic
-rwxrwxr-x. 2 herong herong    22472 toe
-rwxrwxr-x. 2 herong herong    22504 tput
-rwxrwxr-x. 1 herong herong      231 tqdm
-rwxrwxr-x. 2 herong herong    30672 tset
lrwxrwxrwx. 1 herong herong        2 unlzma -> xz
lrwxrwxrwx. 1 herong herong        2 unxz -> xz
-rwxrwxr-x. 1 herong herong      230 wheel
lrwxrwxrwx. 1 herong herong        7 wish -> wish8.6
-rwxrwxr-x. 2 herong herong    20768 wish8.6
-rwxrwxr-x. 2 herong herong  2709960 x86_64-conda_cos6-linux-gnu-ld
...
3\. Python version in Conda environment could be different:herong$ python3 --version
Python 3.6.8

herong$ conda activate
(base) herong$ python3 --version
Python 3.8.3
5\. Python libraries, like NumPy, need to be installed in Conda environment. This is done by the "conda install ..." command, instead of the "pip install ...". A Python library is a Conda package, from Conda's point of view.[Linux Tutorials - Herong's Tutorial Examples](#text00002.html_a2N5)∟ ReferencesList of reference materials used in this book.

*   The CentOS Project , March 2001, ECMA TC39/TG2, [https://www.centos.org](https://www.centos.org)
*   USING SELINUX - Basic and advanced configuration of Security-Enhanced Linux (SELinux) , Red Hat, [https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/8/html/using_selinux/index](https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/8/html/using_selinux/index)
*   Firewalld , [https://firewalld.org](https://firewalld.org)
*   nftables HOWTO documentation , [https://wiki.nftables.org](https://wiki.nftables.org)
*   The netfilter.org project , [https://netfilter.org](https://netfilter.org)
*   List of partition identifiers for PCs , Andries E. Brouwer, [https://www.win.tue.nl/~aeb/partitions/partition_types-1.html](https://www.win.tue.nl/~aeb/partitions/partition_types-1.html)
*   MySQL 8.0 Reference Manual , Oracle, [https://dev.mysql.com/doc/refman/8.0/en/](https://dev.mysql.com/doc/refman/8.0/en/)

![The Front Cover](Image00000.jpg)