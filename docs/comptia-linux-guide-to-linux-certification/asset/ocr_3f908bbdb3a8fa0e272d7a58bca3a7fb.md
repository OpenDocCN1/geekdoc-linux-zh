+   9. At the command prompt, type `init 3` and press **Enter** to switch to runlevel 3 (multi-user.target). Note that you are on tty1 and the gdm is not loaded. Log in to the terminal using the user name of **root** and the password of **LNXrocks!**.

+   10. Next, type `runlevel1` and press **Enter**. What is your current and most recent runlevel?

+   11. At the command prompt, type `init 1` and press **Enter** to switch to single user mode (rescue.target). Supply the root password of **LNXrocks!** when prompted.

+   12. Next, type `runlevel1` and press **Enter**. What is your current and most recent runlevel?

+   13. At the command prompt, type `systemctl isolate graphical.target` and press **Enter** to switch to runlevel 5 (graphical.target). Note that the gdm is loaded. Press **Ctrl+Alt+F2** and log in to the terminal using the user name of **root** and the password of **LNXrocks!**.

+   14. At the command prompt, type `systemctl -a | grep crond.service` and press **Enter**. Is the Systemd cron daemon running?

+   15. At the command prompt, type `systemctl restart crond.service` and press **Enter** to restart the Systemd cron daemon.

+   16. At the command prompt, type `systemctl disable crond.service` and press **Enter** to prevent the system from starting the cron daemon in your current runlevel/target. Note that the existing symbolic link in the /etc/systemd/system/multi-user.target.wants directory instead of the /etc/systemd/system/graphical.target.wants directory?

+   17. At the command prompt, type `systemctl enable crond.service` and press **Enter** to start the cron daemon in your current runlevel/target. Was the symbolic link recreated?

+   18. At the command prompt, type `service netconsole start` and press **Enter**. Note that Systemd started the UNIX SysV netconsole daemon using the systemctl command because Systemd is backwards compatible with UNIX SysV.

+   19. At the command prompt, type `poweroff` and press **Enter** to power off your Fedora Linux virtual machine.

# Project 8-3

In this hands-on project, you explore and configure the system initialization process on Ubuntu Server 14.04.

+   1. Boot your Ubuntu Server Linux virtual machine. After your Linux system has been loaded, log into tty1 using the user name of **root** and the password of **LNXrocks!**.

+   2. At the command prompt, type `runlevel` and press **Enter**. What is your current runlevel? What is the most recent runlevel?

+   3. At the command prompt, type `ls /etc/init.d` and press **Enter**. What do the contents represent?

+   4. At the command prompt, type `ls /etc/init` and press **Enter**. What do the contents represent?

+   5. At the command prompt, type `cat /etc/init/ssh.conf` and press **Enter**. In which runlevel is the ssh daemon started?

![](bbox=[0.88, 0.42, 0.92, 0.46])