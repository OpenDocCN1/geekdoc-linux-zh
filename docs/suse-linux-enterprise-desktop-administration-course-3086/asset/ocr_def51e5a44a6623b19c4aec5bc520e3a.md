If the file system is mounted read-writable when you reset the computer in the next step, a file system check would need to be done when the computer starts up again.

+   7. Reset the computer.
+      You will notice that the start screen looks different now because you turned off the graphical menu.
+   8. If you want to edit the kernel command line, press **p** and then enter the password used in Step 4 and 5. A short help text informs you about the available options.
+   9. Press **b** to boot the computer.
+   10. Undo the changes in `/boot/grub/menu.lst`:
+       a. Log in as geeko, open a terminal window, and `su -` to root (password `n0v3ll`).
+       b. Open `/boot/grub/menu.lst` with vi, put a comment sign at the beginning of the line starting with `password`, and remove the comment sign in front of the line starting with `gfxmenu`. Save the file and close vi by pressing Esc and entering `:wq`.

# Objective 3—Manage Runlevels

Managing runlevels is an essential part of Linux system administration. In this objective, you learn what runlevels are, the role of the program init, and how to configure and change runlevels:

+   - The init Program and Linux Runlevels
+   - init Scripts and Runlevel Directories
+   - Change the Runlevel

# The init Program and Linux Runlevels

In order to understand Linux system initialization and management, you need to examine the following:

+   - The init Program
+   - The Runlevels
+   - init Configuration File (`/etc/inittab`)

**The init Program** The system is initialized by `/sbin/init`, which is started by the kernel as the first process of the system.

This process, or one of its child processes, starts all additional processes. In addition, because init is the last process running, it ensures that all other processes are correctly ended. This means that init controls the entire booting up and shutting down of the system.

Because of this position of priority, signal 9 (SIGKILL), with which all processes can normally be ended, has no effect on init.

The configuration file for init is `/etc/inittab`. Various scripts are started by init, depending on entries in this file. All these scripts are located in the `/etc/init.d/` directory.

Part of the configuration in `/etc/inittab` is the runlevel the system uses after booting.