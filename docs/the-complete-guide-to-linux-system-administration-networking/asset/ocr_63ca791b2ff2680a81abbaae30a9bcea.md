![](bbox=[0.15, 0.08, 0.62, 0.62])

# Figure 9-3 Kernel messages stored in /var/log/dmesg after system start-up; viewable after start-up using the dmesg command

If you are using the GRUB boot loader, press “a” when you see a list of operating system choices. This lets you type a boot parameter before starting Linux. If you are using LILO, enter the name of the system you want to start, then a space, then the boot parameters to pass to the Linux kernel.

![](bbox=[0.12, 0.86, 0.18, 0.95])

> In LILO you can press the Tab key to see a list of names for the available operating systems. GRUB lists the choices for you automatically.

You can use boot parameters to activate features of Linux. For example, by using the boot parameter single, you start Linux in a special single-user maintenance mode:

```
linux single
```

Another example is the mem= boot parameter. The kernel has trouble recognizing the correct amount of system memory on some systems with more than 64 MB of RAM. (Recall that the free command shows you how much memory the kernel is aware of.) You can use the mem= boot parameter to tell Linux how much memory you really have. (Note that if you tell the kernel that you have more memory than you really have, it will eventually crash trying to access the nonexistent memory.) For example, if your system has 512 MB of RAM, you can start Linux with this command:

```
linux mem=512M
```