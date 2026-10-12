# 6. Type the password again, and press Enter.

If you enter the same password both times, the passwd command changes the password and displays the following message:

```
passwd: all authentication tokens updated successfully.
```

# 7. Now type reboot to reboot the PC.

After Linux starts, it displays the familiar login screen. Now you should be able to log in as root with the new password.

![](bbox=[0.1, 0.42, 0.22, 0.56])

Make sure your Red Hat Linux PC is physically secure. As this procedure shows, anyone who can physically access your Red Hat Linux PC can simply reboot, set a new root password, and do whatever they want with the system. Another way to protect against resetting the password is to set a GRUB password, which causes GRUB to require a valid password before it boots Red Hat Linux. Of course, then you must remember and enter the GRUB password every time you boot your system!

# Understanding How Red Hat Linux Boots

Knowing the sequence in which Red Hat Linux starts processes as it boots is important. You can use this knowledge to start and stop services, such as the Web server and Network File System (NFS). The next few sections provide you with an overview of how Red Hat Linux boots and starts the initial set of processes. These sections also familiarize you with the shell scripts that start various services on a Red Hat Linux system.

# Understanding the init process

When Red Hat Linux boots, it loads and runs the core operating-system program from the hard drive. The core operating system is designed to run other programs. A process named init starts the initial set of processes on your Linux system.

```
ps ax | more
```

You get an output listing that starts off like this:

```
PID TTY   STAT TIME COMMAND
  1 ?     S    0:03 init
```

The first column, with the heading PID, shows a number for each process. PID stands for process ID (identification) — a sequential number assigned by the Linux kernel. The first entry in the process list, with a PID of 1, is the init