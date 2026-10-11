# **SECURITY**





puter BIOS prevents booting from the USB ports, as well as ensure that a system BIOS password is set to prevent other users from changing the boot order.

Along these same lines, anyone who has access to the physical Linux computer could boot the computer and interact with the LILO or GRUB boot loader. This could allow a user to specify options that would boot the system in Single User Mode and gain root access to the system without specifying a password. To prevent this, simply ensure that you set a boot loader password in the LILO or GRUB configuration files, as discussed in Chapter 9.

Another important security consideration for Linux computers is to limit access to graphical desktops and shells. If you leave your workstation for a few minutes and leave yourself logged in to the system, another user can use your computer while you are away. As a result, it is good security practice to lock your desktop environment or exit your command-line shell before leaving the computer. To lock the GNOME or KDE desktop, simply navigate to the Red Hat button and choose Lock Screen; you will need to enter your password to use your desktop again. Exiting a command-line shell also ends any background processes because the parent of those processes is your shell. If you run background processes that take a long time to complete, simply run them using the `nohup command`; this allows you to exit your command-line shell without ending any background processes. For example, to run the `updatedb` command and exit your system afterward such that you can leave your workstation, simply perform the following commands:

```
```
[root@server1 root]# nohup updatedb &
[1] 3773
nohup: appending output to 'nohup.out'
[root@server1 root]# exit
```
```

```
```
Fedora Core release 2 (Tettnang)
Kernel 2.6.5-1.358 on an i686

server1 login:
```
```

If you have root access to a Linux system, it is important to minimize the time that you are logged in as the root user to reduce the chance that another user can access your terminal if you accidentally leave your system without locking your desktop or exiting your shell. It is best practice to create a regular user account that you can use to check e-mails and perform other day-to-day tasks. You can then use the `su [switch user] command` to obtain root access only when you need to perform an administrative task. When you are finished, you can use the `exit` command to return to your previous shell where you are logged in as a regular user account, as shown in the following output:

```
```
[user1@server1 user1]$ su - root
Password: ****
[root@server1 root]# _
[root@server1 root]# rm -f /etc/security
[root@server1 root]# exit
[user1@server1 user1] _
```
```