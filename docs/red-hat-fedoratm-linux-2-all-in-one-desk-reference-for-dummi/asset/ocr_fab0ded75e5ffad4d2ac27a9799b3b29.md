+   5. Type the new root password that you want to use (it doesn’t appear on-screen) and then press Enter.
+   
+   Linux asks for the password again, like this:
+   
+   Retype new password:
+   
+   6. Type the password again, and press Enter.
+   
+   If you enter the same password both times, the passwd command changes the password and displays the following message:
+   
+   passwd: all authentication tokens updated successfully.
+   
+   7. Now type reboot to reboot the PC.
+   
+   After Linux starts, it displays the familiar login screen. Now you can log in as root with the new password.

> WARNING!
> Make sure your Fedora Core PC is physically secure. As these steps show, anyone who can physically access your Fedora Core PC can simply reboot, set a new root password, and do whatever they want with the system. Another way to protect against resetting the password is to set a GRUB password, which causes GRUB to require a valid password before it boots Fedora Core. Of course, you must then remember to enter the GRUB password every time you boot your system!

| Book VI | Performing Basic System Administration | Chapter 1 |
| --- | --- | --- |

# # Understanding How Fedora Core Boots

Knowing the sequence in which Fedora Core starts processes as it boots is important. You can use this knowledge to start and stop services, such as the Web server and Network File System (NFS). The next few sections provide you with an overview of how Fedora Core boots and starts the initial set of processes. These sections also familiarize you with the shell scripts that start various services on a Fedora Core system.

# ## Understanding the init process

When Fedora Core boots, it loads and runs the core operating-system program from the hard drive. The core operating system is designed to run other programs. A process named init starts the initial set of processes on your Linux system.

To see the processes currently running on the system, type

ps ax | more