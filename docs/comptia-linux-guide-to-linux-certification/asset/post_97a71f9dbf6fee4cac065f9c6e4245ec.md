
5  root RT 0     0     0  S  0.0  0.0  0:00.00 watchdog/0
6  root RT 0     0     0  S  0.0  0.0  0:00.01 migration/1
7  root 20 0     0     0  S  0.0  0.0  0:00.45 ksoftirqd/1
8  root RT 0     0     0  S  0.0  0.0  0:00.00 watchdog/1
9  root 20 0     0     0  S  0.0  0.0  0:00.66 events/0
10 root 20 0     0     0  S  0.0  0.0  0:00.57 events/1
11 root 20 0     0     0  S  0.0  0.0  0:00.00 cpuset
12 root 20 0     0     0  S  0.0  0.0  0:00.00 khelper

Furthermore, the `free` command can be used to display the total amounts of physical and swap memory in kilobytes and their utilizations, as shown in the following output:

```
[root@server1 ~]# free
                  total        used        free      shared  buffers    cached
Mem:          961284      814820      146464           0    126120    480740
-/+ buffers/cache:    207960      753324
Swap:         4095992         212     4095780
[root@server1 ~]# _
```

The Linux kernel reserves some memory for its own use (`cached`) to hold requests from hardware devices (`buffers`); the `total` memory in the preceding output is calculated with and without these values to indicate how much memory the system has reserved. The output from the preceding `free` command indicates that there is sufficient memory in the system because little swap is used and a great deal of free physical memory is available.

Like the `free` utility, the `vmstat` utility can be used to indicate whether more physical memory is required by measuring swap performance:

```
[root@server1 ~]# vmstat
procs  -----------memory---------- -swap-  ----io----  system-----cpu-----
r b  swpd  free   buff  cache si so bi  bo in cs us sy id wa st
1  0   212 146496 126144 480752  0  0  5  2 49 51  0  0 99  0  0
[root@server1 ~]# _
```

The `vmstat` command shown in the previous output indicates more information than the `free` command used earlier, including the following:

- The number of processes waiting to be run (`r`)
- The number of sleeping processes (`b`)
- The amount of swap memory used, in Kilobytes (`swpd`)
- The amount of free physical memory (`free`)
- The amount of memory used by buffers, in Kilobytes (`buff`)
- The amount of memory used as cache (`cache`)
- The amount of memory in Kilobytes per second swapped in to the disk (`si`)
- The amount of memory in Kilobytes per second swapped out to the disk (`so`)
- The number of blocks per second sent to block devices (`bi`)
- The number of blocks per second received from block devices (`bo`)
- The number of interrupts sent to the CPU per second (`in`)
- The number of context changes sent to the CPU per second (`cs`)
- The CPU user time (`us`)
- The CPU system time (`sy`)
- The CPU idle time (`id`)
- The time spent waiting for I/O (`wa`)
- The time stolen from a virtual machine (`st`)

Thus, the output from `vmstat` shown previously indicates that little swap memory is being used because `swpd` is 212 KB and `si` and `so` are both zero; however, it also indicates that the reason for this is that the system is not running many processes at the current time (`r=1, id=99`).

## Security

In the past decade, hundreds of new services have been made available to Linux systems, and the number of Linux users has risen to tens of millions. In addition, Linux systems today are typically made available across networks such as the Internet. As a result, Linux is more prone today to security loopholes and attacks, both locally and from across networks. To protect your Linux computer, you should take steps to improve local and network security as well as understand how to detect intruders who manage to breach your Linux system.

### Securing the Local Computer

One of the most important security-related practices is to limit access to the physical Linux computer itself. If a malicious user has access to the Linux computer, that user could boot the computer using a USB flash drive, CD, or DVD that contains a small operating system and use it to access files on the partitions on the hard disk of the Linux computer without having to log in to the operating system installed on the hard disk. To prevent this, you should lock important computers, such as Linux servers, in a specific room to which only Linux administrators or trusted users have key access. This room is commonly called a **server closet**. Unfortunately, some Linux computers, such as Linux workstations, must be located in public areas. For these computers, you should remove the CD and DVD drives from the computer. In addition, you should ensure that the boot order listed in the computer BIOS prevents booting from the USB ports, as well as ensure that a system BIOS password is set to prevent other users from changing the boot order.

Another important security consideration for Linux computers is to limit access to graphical desktops and shells. If you walk away from your workstation for a few minutes and leave yourself logged in to the system, another person can use your computer while you are away. To avoid such security breaches, it is good security practice to lock your desktop environment or exit your command-line shell before leaving the computer.

Both the GNOME and KDE desktop environments allow you to lock your screen. For the GNOME desktop, you can click the power symbol icon in the upper-right corner menu and choose the lock icon. To use your desktop again, you need to enter your password.

While it is good practice to exit a command-line shell before leaving your workstation, doing so necessarily ends any background processes because the parent of those processes is your shell. If you run background processes that take a long time to complete, you can avoid problems associated with exiting the command-line shell by running the processes using the `nohup` command. This allows you to exit your command-line shell without ending any background processes. For example, to run the `updatedb` command and then exit your system (so that you can leave your workstation), perform the following commands:

```
[root@server1 ~]# nohup updatedb &
[1] 3773
nohup: ignoring input and appending output to ‘nohup.out’
[root@server1 ~]# exit
```

```
Fedora release 20 (Heisenbug)
Kernel 3.11.10-301.fc20.x86_64 on an x86_64 (tty2)

server1 login:
```

If you have root access to a Linux system, it is important to minimize the time that you are logged in as the root user to reduce the chance that another user can access your terminal if you accidentally leave your system without locking your desktop or exiting your shell. It is best practice to create a regular user account that you can use to check e-mails and perform other day-to-day tasks. Recall from Chapter 2 that you can then use the `su` command to obtain root access only when you need to perform an administrative task. When you are finished, you can use the `exit` command to return to your previous shell, where you are logged in as a regular user account.

The root user can use the `su` command to switch to any other user account without specifying the user account password.

Still, some users, such as software developers, need to run certain commands as the root user in certain situations. Instead of giving them the root password, it is best to give them the ability to run certain commands as the root user via the `sudo` command. The `sudo` command checks the `/etc/sudoers` file to see if you have rights to run a certain command as a different user. The following `/etc/sudoers` file gives software developers mary and bob the ability to run the `kill` and `killall` commands as the root user on the computers `server1` and `server2`:

```
[root@server1 ~]# cat /etc/sudoers
User_Alias SD = mary, bob
Cmd_Alias KILL = /bin/kill, /usr/bin/killall
Host_Alias SERVERS = server1, server2

SD  SERVERS = (root) KILL
[root@server1 ~]#
```

Now, if mary needs to kill the cron daemon on `server1` (which was started as the root user) to test a program that she wrote, she needs to use the `sudo` command, as shown in the following output, and supply her own password:

```
[mary@server1 ~]$ ps -ef | grep crond
root  2281 1  0  21:20 ?  00:00:00 crond
[mary@server1 ~]$ kill -9 2281
```

![](img/c27875544958897d817484d558c208c8_672_0.png)
