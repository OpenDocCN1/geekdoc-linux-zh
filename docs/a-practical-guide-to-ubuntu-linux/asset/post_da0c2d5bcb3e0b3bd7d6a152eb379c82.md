
# LOGGING OUT

With a $ shell prompt displayed, you can either execute a program or exit from the shell. If you exit from the shell, the process running the shell dies and the parent process wakes up. When the shell is a child of another shell, the parent shell wakes and displays a signal. Exiting from a login calls the operating system to send init signal that one of its children has died. Upon receiving this signal, init takes action based on the appropriate job (page 433). In the case of a process controlling for a terminal, init calls the appropriate service (page 439), which then respawns getty so another user can log in.

# BRINGING THE SYSTEM DOWN

The shutdown and reboot utilities perform the tasks needed to bring the system down safely. These utilities can restart the system, prepare the system to be turned off, and, on most hardware, power down the system. The poweroff and halt utilities are to reboot.

You must tell shutdown when you want to bring the system down. This time can be expressed as an absolute time of day, as in 19:15, which causes the shutdown at 7:15 PM. Alternatively, you can give this time as the number of minutes from the present time, as in +15, which means 15 minutes from now. To bring the system down immediately (recommended for emergency shutdowns only or when you are the only user logged in), you can give the +0 or its synonym, now. When the shutdown exceeds 5 minutes, nonroot logs are disabled for the last 5 minutes before shutdown.

# Do not turn the power off before beginning the system down

Do not turn the power off on a Linux system without first bringing it down as described in this section. To speed disk access, Linux keeps buffers in memory that it writes to disk periodically or when system use is momentarily low. When you turn off or reset the computer without writing the contents of these buffers to the disk, you lose any information in the buffers. Running the shutdown utility forces these buffers to be written at any time by issuing a sync command. However, sync does not mount filesystems, nor does it bring the system down. Also, turning off or resetting the system in this manner can destroy filesystems on IDE and SATA hard disks.

Calling shutdown with the -r option allows the system to reboot (as reboot, except reboot implies now). Calling shutdown with the -h option forces the system to halt (as halt, except halt implies now). A message appears once the system has been safely halted: System halted. Because most systems power off automatically after shutdown, you are unlikely to see this message.

Because Linux is a multiuser system, shutdown warns all users before taking action. This warning gives users a chance to prepare for the shutdown, by writing out editor files or exiting from applications. You can replace the default shutdown message with one of yours by following the time specification on the command line with a message:

$ sudo shutdown -h 09:30 to install disk, up by 10am.

# CONTROL-ALT-DEL: REBOOTS THE SYSTEM

In a textual environment, pressing the key sequence CONTROL-ALT-DEL (also referred to as the three-finger salute or the Vulcan death grip) on the console kernel to trigger a control-alt-delete task (page 439) that causes init to run the commands in /etc/init/control-alt-delete. These commands safely reboot the system by issuing a shutdown command. You can decide the CONTROL-ALT-DEL sequence by removing the /etc/init/control-alt-delete file (or by moving it to another directory for safekeeping).

In a graphical environment, X traps this key sequence but the window manager does not pass it to the kernel. As a result, CONTROL-ALT-DEL does not work in graphical environment.

# GOING TO RECOVERY (SINGLE-USER) MODE

The following steps describe a method of manually bringing the system down to recovery mode. In some cases it may be easier to simply reboot the system and bring it up in recovery mode; see page 445. Before starting, make sure you have enough users before switching to recovery mode; otherwise, you may lose data they are working on. Because going from multiuser to recovery mode can affect other users, you must work with root to perform all of these tasks except the first:

- Use wall (page 615) to warn everyone who is using the system to log out.
- If you are sharing files for NFS, use exports -a to disable network access to the shared filesystems (Use exports without an argument to see which filesystems are shared).
- Confirm that no critical processes are running in the background (e.g., unattended).
- Give the command init 1 (page 444) to bring the system down to recovery mode. The system displays messages about it shutting down, followed by a root prompt (#). In runlevel 1, the system kills many services and then brings the system to runlevel S. The utility confirms the system was at runlevel 1 and now is at runlevel S.
```
$ sudo init 1
runlevel1 S
```
- Use unmount -a to unmount all mounted devices that are not in use. Use mount without an argument to make sure devices other than root are mounted before continuing.

# TURNING THE POWER OFF

Once the system is in recovery mode, give the command init (page 444) or halt to bring the system down. You can build a kernel so it turns off at the appropriate time. If the system is not set up, turn the power off when prompted.

# CRASH

A crash occurs when the system suffers suddenly or unexpectedly. A crash may result from software or hardware problems or a loss of power. In a fraction of a second, some components are supplied with erratic voltage; others are not. Buffers are not flushed, corrupted data may be written to hard disks, and IDE and SATA drives do not behave as SCSI drives under these circumstances. After a crash, you must bring the system up carefully to minimize damage.

# REPAIRING A FILESYSTEM

Although the filesystems are checked automatically during the boot process if needed, you will have to check them manually if a problem cannot be repaired. By default, fsck cannot repair a filesystem at boot time; Linux enters recovery mode so that you can run fsck manually. If necessary, explicitly boot the system to recovery mode (page 445).

# Back up badly damaged filesystem

When a filesystem is badly broken, fsck sometimes makes the situation worse while trying to repair it. In these cases it may be possible to recover data by copying the readable data from the broken filesystem before attempting to repair it. When a damaged filesystem holds important data, use dd (the dd man page) to make a full backup. With the system in recovery mode, use unmount local filesystems you want to check. Run fsck (page 512) on these filesystems. Note that ordinary files or directories that may not be complete or correct are placed in the lost+found directory (page 488) in each filesystem needed. After successfully running fsck, if the system enters recovery mode automatically, type exit to exit the recovery shell and resume booting the system; otherwise, give the reboot command. If files are not correct or are missing altogether, you may have to recreate them from a backup copy of the filesystem. For more information refer to “Backing Up Files” on page 599.

# WHEN the SYSTEM Does Not BO

When a system will not boot from the hard disk, boot the system to rescue mode (page 83) or recovery mode (page 445). If the system comes up, run fsck (page 512) on the root filesystem on the hard disk and try booting from the hard disk again. If the system still does not boot, you may have to reinstall the boot record (page 589).

When all else fails, go through the install procedure and perform an “upgrade” to the current version of Linux. Ubuntu systems can perform a nondestructive upgrade and can fix quite a bit of damage in the process. For more information refer to page 74.

# AVOIDING A TROJAN HORSE

A Trojan horse is a program that does something destructive or disruptive to a system while appearing to be benign. As an example, you could store the following script in an executable file named mkfs:

```
while true
  do
    echo 'Good Morning Mr. Jones. How are you? Ha Ha Ha.' >dev/console
  done
```

If you are working with root privileges when you run this command, it will continuously write a message to the console. If the programmer was malicious, it could do something worse. The only thing missing in this plot is access permissions.

A malicious user could implement this Trojan horse by changing the PATH variable to include a publicly writable directory at the start of the PATH string. The catch is that you would need to write to /etc/profile—where the PATH variable is set for root—and only a user with root privileges can do that. Then you would need to put the bogus mkfs program file in that directory. Because the fraudulent version appears in a directory mentioned earlier than the real one, the shell would run it instead of the real version. Thus, the next time a user with root privileges tries to run mkfs, the fraudulent version would run.

Trojan horses lie in wait to take advantage of the misspellings that people make are among the most insidious types. For example, you might type sl instead of ls. Because you do not regularly execute a utility named sl and not remembering the command sl, it is more difficult to track this type of Trojan horse than one that takes the name of a more familiar unity.

A good way to prevent the execution of a Trojan horse is to make sure your PATH variable does not contain a single colon (:) at the beginning or end of the PATH string or a period (.), or double colon (::) anywhere in the PATH string. This precaution ensures that you will not execute a file in the working directory by accident.
