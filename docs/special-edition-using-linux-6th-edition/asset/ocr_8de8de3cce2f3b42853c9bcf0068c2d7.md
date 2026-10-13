But before you can modify any files, you’ll need to remount the root filesystem read-write with the following command:

```
mount -n -o remount,rw /
```

This command must be entered as above or you’ll get errors from the filesystem if you try to write to it. The -n tells mount not to try to write to the /etc/mtab file, the -o is for miscellaneous options, in this case remount, rw to remount the root filesystem (/) read-write. Do not run fsck on a filesystem that is mounted read-write because the kernel will periodically scan memory to the disk. You do not want this to occur while fsck is writing to the disk because fsck bypasses the kernel and writes directly to the disk. With both fsck and sync writing to the disk, you could corrupt the disk further.

> **Caution**
> 
> The next paragraph discusses booting directly to a shell, which can cause irreparable corruption to the filesystem. This is a last-resort option only!

If, however, despite your best efforts, you find that the boot process still hangs even with the -b option to LILO, or if you’ve forgotten the root password, don’t despair. At the LILO prompt, you can pass the parameter init=/bin/sh. This argument will be used by the kernel itself. Remember that the kernel runs one and only one program before it goes into the background: init. By passing the preceding argument to LILO, the kernel runs a shell as its only program. This is very dangerous, but it enables you to mount the root filesystem (mount -n -o remount, rw /), change /etc/mtab or /etc/shadow, and then sync and reboot. In this case I recommend calling sync twice and then remounting the root filesystem read-only and rebooting. Use this as a last resort before a reinstall because it can corrupt your disk, making a reinstall inevitable.

# TROUBLESHOOTING

*My system is prompting me for my root password at boot up. (I was not asked for a username.)*
*What’s going on?*

The system has found some corruption in the filesystem that it is unable to cope with. You should read and follow the instructions on the screen. They will say something to the effect of filesystem corruption, run fsck manually. Assuming the corruption was found on disk partition /dev/hda3, you need to run the following:

```
fsck -f /dev/hda3
```

You can add the -y option to the line if you are unfamiliar with repairing a filesystem manually. When fsck has finished, just log out, and the system reboots.

*During boot, the process stops (at loading amd or some other daemon). What should I do?*

Wait. Make sure a full two minutes has passed. If five minutes passes and nothing has happened, your system is probably frozen. When you reboot, specify the -b option at the LILO prompt:

```
boot: linux -b
```