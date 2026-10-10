+   4. At the command prompt, type `grub2-mkconfig -o /boot/grub2/grub.cfg` and press `Enter` to rebuild the GRUB2 configuration file with your change.
+   5. Reboot your system by typing `reboot` and pressing `Enter`. At the GRUB2 boot screen, view the available options. How long do you have to interact with the GRUB2 boot loader after POST before the default operating system is booted? Next, press `c` to obtain a command prompt.
+   6. At the grub> prompt, type `help` and press `Enter` to see a list of available commands. Next, type `lspci` and press `Enter` to see a list of detected PCI devices. Following this, type `list_env` and press `Enter` to view the variables present. Normally, there should be a single variable called `saved_entry` that lists the default OS that is booted by GRUB2, although on some systems you may not see this variable. Type `reboot` and press `Enter` to reboot your system.
+   7. At the GRUB2 boot screen, press `e` to edit your configuration. Where did you see these contents recently?
+   8. Locate the line that starts with the word “linux” and navigate to the end of this line (the last two keywords on this line should be `rhgb` and `quiet`). Add the word `single` after the word `quiet` and press `F10` to boot your modified configuration. What does this option tell the boot loader to do?
+   9. Supply your root password of Lnxrocks! when prompted.
+   10. Reboot your system by typing `reboot` and pressing `Enter`. Allow your system to boot normally.

# Project 8-2

In this hands-on project, you explore and configure the system initialization process on Fedora 20.

+   1. Switch to a command-line terminal (tty2) by pressing `Ctrl+Alt+F2` and log in to the terminal using the user name of `root` and the password of Lnxrocks!.
+   2. At the command prompt, type `runlevel` and press `Enter`. What is your current runlevel? What is the most recent runlevel?
+   3. At the command prompt, type `cat /etc/inittab` and press `Enter`. View the commented sections. Why is `/etc/inittab` not used in Fedora 20?
+   4. At the command prompt, type `ls /usr/lib/systemd/system` and press `Enter`. What do the contents represent?
+   5. At the command prompt, type `ls /etc/rc.d` and press `Enter`. Do you see init.d and rcl[unlevel],d subdirectories? Why?
+   6. At the command prompt, type `ls /etc/rc.d/init.d` and press `Enter`. Which UNIX SysV daemons are available on Fedora 20?
+   7. At the command prompt, type `chkconfig - -list netconsole` and press `Enter`. In which runlevels is the netconsole daemon started by default?
+   8. At the command prompt, type `chkconfig - -level 23 netconsole on` and press `Enter` to configure the netconsole daemon to start in runlevels 2 and 3. Next, type `ls /etc/rc.d/rc[23].d` and press `Enter`. Does the symbolic link to the netconsole rc script start with S? Why?