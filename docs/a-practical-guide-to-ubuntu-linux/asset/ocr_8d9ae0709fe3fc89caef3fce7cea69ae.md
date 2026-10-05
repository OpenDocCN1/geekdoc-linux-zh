$ sudo shutdown -h 09:30 to install disk, up by 10am.

# CONTROL-ALT-DEL: REBOOTS THE SYSTEM

In a textual environment, pressing the key sequence CONTROL-ALT-DEL (also referred to as the three-finger salute or the Vulcan death grip) on the console kernel to trigger a control-alt-delete task (page 439) that causes init to run the commands in /etc/init/control-alt-delete. These commands safely reboot the system by issuing a shutdown command. You can decide the CONTROL-ALT-DEL sequence by removing the /etc/init/control-alt-delete file (or by moving it to another directory for safekeeping).

In a graphical environment, the X Window traps this key sequence but the window manager does not pass it to the kernel. As a result, CONTROL-ALT-DEL does not work in a graphical environment.

# GOING TO RECOVERY (SINGLE-USER) MODE

The following steps describe a method of manually bringing the system down to recovery mode. In some cases it may be easier to simply reboot the system and bring it up in recovery mode; see page 445. Before starting, make sure you have enough users warning before switching to recovery mode; otherwise, you may lose the data they are working on. Because going from multiuser to recovery mode can affect other users, you must work with root to perform all of these tasks except the first.

+   1. Use wall (page 615) to warn everyone who is using the system to log out.
2. If you are sharing files for NFS, use exports -ua to disable network access to the shared filesystems. (Use exports without an argument to see which filesystems are being shared)
3. Confirm that no critical processes are running in the background (e.g., an unattended compile).
4. Give the command telinit 1 (page 444) to bring the system down to recovery mode. The system displays messages about the services it is shutting down, followed by a root shell prompt (#). In runlevel 1, the system kills many system services and then brings the system to runlevel S. The utility confirms the system was at runlevel 1 and now is at runlevel S. The user should caution about changing runlevels on page 444.

```
$ sudo telinit 1
# runlevel
1 S
```

+   5. Use unmount -a to unmount all mounted devices that are not in use. Use mount without an argument to make sure that no devices other than root (/) are mounted before continuing.