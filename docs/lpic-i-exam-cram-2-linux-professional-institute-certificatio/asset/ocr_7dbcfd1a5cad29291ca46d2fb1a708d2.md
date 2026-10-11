The halt command is directly used only in runlevels 0 and 6; otherwise, it simply calls the shutdown command with the appropriate action of reboot or halt. This can be overridden by the use of halt -f to force a system halt rather than just calling shutdown.

You can power down the system after halting is done with the poweroff command, which is a symlink to the halt command. On compatible systems, this halts the system and powers the computer off.

The reboot command is another symlink to the halt command, which calls the shutdown command with the -r parameter to effect a reboot of the system.

> ALERT: You need to know that the poweroff and reboot commands are symlinks to the halt command and that they all use the shutdown command in the stated situations.

# The init Process

When executed, the /sbin/init program becomes the first or parent process and is assigned PID 1. All other processes are children of init and inherit the environment and attributes of the init process by default.

The init process is configured by the /etc/inittab file and refers to this file at various times in its operations.

# The /etc/inittab File

The system and, in particular the init process, refers to this file; it's responsible for the runlevels, how many programs function and respond to stimulus, and how the system is initialized.

Entries in the /etc/inittab file consist of the following sections:

*id:runlevels:action:process*

For example, the system's virtual terminals (tty1 through tty6 by default) mingetty processes are configured by the following lines in the /etc/inittab file:

```
# Run gettys in standard runlevels
1:2345:respawn:/sbin/mingetty tty1
2:2345:respawn:/sbin/mingetty tty2
3:2345:respawn:/sbin/mingetty tty3
4:2345:respawn:/sbin/mingetty tty4
5:2345:respawn:/sbin/mingetty tty5
6:2345:respawn:/sbin/mingetty tty6
```