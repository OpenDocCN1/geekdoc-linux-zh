# Advanced Bash-Scripting Guide

```
bash$ fuser -um /dev/usbdrive
/mnt/usbdrive:      1772c(bozo)

bash$ kill -9 1772
bash$ umount /mnt/usbdrive
```

The fuser command, invoked with the -n option identifies the processes accessing a port. It is especially useful in connection with nmap.

```
root# nmap localhost .localdomain
PORT STATE SERVICE
25/tcp  open    smtp

root# fuser -un tcp 25
25/tcp:               2095(root)

root# ps ax | grep 2095 | grep -v grep
2095 ?      Ss       0:00 sendmail: accepting connections
```

cron program scheduler, performing such duties as cleaning up and deleting log files and updating theing database. This is the supervisor version of at (each user may have their own crontab file which can be changed with the crontab command). It runs as a daemon and executes entries from /etc/crontab.

+   * Some flavors of Linux crond, Matthew Dillon's version of cron.

# Process Control and Booting

init

The init command is the parent of all processes. In the final step of a bootup, init determines the runlevel of the system from /etc/inittab. Invoked by its alias telinit, and by root only.

telinit

Linked to init, this is a means of changing the system runlevel, usually used for maintenance or emergency filesystems. Inoked by root. This command can be dangerous -- be certain before you use it.

runlevel shows the current and last runlevel, that is whether the system is halted (runlevel 0), in single-user mode (1), in multi-user mode (2 or 3), in Windows (5), or rebooting (6). This command accesses the /var/run/utmp file.

halt, shutdown

Command set to shut down the system, usually just prior to power down.

+   * On Linux distributions, the halt command has 755 permissions, so it can be invoked by a non-root user. A careless halt in a terminal or a script may shut down the system!

service

Starts or stops a system service. The startup scripts in /etc/init.d and /etc/rc.d use this command to start services at boot.

Chapter 17. System and Administrative Commands 335