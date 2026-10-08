
# BIOS FEATURES SETUP

...is highlighted and hit Enter. Of the bewildering menu of options, select **Boot Sequence** by pressing the down arrow until this item is highlighted and press Enter. This is the sequence of devices that the machine will try to boot from.

For those blissfully ignorant of the DOS world, device "A" is the first floppy drive (also called a diskette and usually the top unit as opposed to the bottom unit), device "B," if it is the second floppy. Device "C" is the hard disk, and for those living large, device "D" is the second hard disk. Most recent BIOS versions also offer "SCSI" and "CD-ROM."

Press the + key, or, possibly, the PageUp key, repeatedly until it displays the device that you normally boot from, "C" or "SCSI." You do not want to select the option "C, A" because then an intruder can trash the hard disk Master Boot Record (MBR) and force the machine to boot from the floppy. If a subsequent corruption problem requires booting from a set of rescue disks (floppies), you can change this device order and return to the main menu. Then follow the instructions for saving the changes and exiting; commonly this is by pressing the F10, Y, and Enter keys.

Also, it is a good idea to configure the CMOS to disable all serial and parallel devices that you do not need. This will prevent someone from connecting a device to a serial port or from connecting a floppy drive, zip drive, or CD-RW burner to the parallel port.

## 2.16.3 Adding a CMOS Password

![](img/7d04225c75a86d3cf4bd6077596f35b2_136_0.png)

To prevent an intruder from altering the CMOS settings that you have configured for security and correct operation, you need to add a CMOS password by following the steps below. This will cause the CMOS code to ask for this password before doing anything of significance.

- 1. Reboot your system, and when prompted, press the Delete key to get into the CMOS menu. A common prompt for this is Press DEL to enter SETUP.
- 2. Move the down arrow until a menu selection is highlighted that reads something like CMOS Password or SUPERVISOR PASSWORD.
- 3. Press Enter and enter the desired password. Immediately write the password down and file it securely where you will remember to look for it at 3 A.M. in a year when you need to boot from rescue disks. Enter the password a second time.
- 4. Move the down arrow until the menu selection SAVE & EXIT SETUP is highlighted, press Enter, Y, and a second Enter (or F10, Y, Enter).

Now an intruder will be unable to alter the CMOS settings, say, to enable booting the floppy to get control of the system with his own UNRescue Disks.

What if an intruder changes a CMOS password after changing the CMOS settings to only boot from nonexistent hardware? What if the other Sys/Admin forgot to tell you the password before your vacation in the Outback?

Some motherboards have a jumper that can be set temporarily to erase the CMOS password. Some will turn off the Insert button if held down while booting. With still others, you simply remove the CMOS battery (with the system powered down) for 30 seconds or so. Physical security is required to prevent these intrusions. Keep in mind that removing the battery will cause other important configuration settings to be lost too. (It is a really good idea to record the BIOS settings of each of your systems somewhere.)

## 2.16.4 Defending Against Single-User Mode

![](img/7d04225c75a86d3cf4bd6077596f35b2_137_0.png)

Linux normally boots in multiuser mode. This allows for a secure boot system because it skips single-user mode where a root shell would be offered without the entering of the root password.[27] Sometimes a system will not complete the boot-sequence to multiuser mode either due to an error in the configuration or due to corruption in the root partition. To allow one to "get control" of such a system, LILO[28] allows one to request that Linux come up in single-user mode. Instead of lots of daemons coming up, in single-user mode /etc/init brings only a few things. To boot into single-user mode, at the LILO prompt type `single` instead of `linux`.

> Red Hat and most other distributions invoke fsck and do more operations than they should. Most UNIX versions do an absolute minimum when starting single-user mode to minimize problems in the event of file system corruption or misconfiguration.

There are a few different ways to prevent this. All of them involve changes to LILO's configuration file, typically stored in /etc/lilo.conf, and issuing the

[27] The default mode that Linux boots up is specified in the /etc/inittab file in the line ending in :initdefault: The number before this is the mode. The usual number is "3" for multiuser with networking which looks like id:3:initdefault.
[28] Other common modes are "2" for multiuser without servers, and "1" for single-user mode.
[29] The LILO program is the LINUX Loader for Intel hardware. There might be similar features in milo and silo, the boot loaders for Alpha and Sun hardware and in the boot loaders for the PowerPC and StrongARM architecture.

command lilo to store these instructions in the Master Boot Record (MBR). Although a reboot is not strictly necessary, you certainly will want one to verify that the changes worked.

The most flexible method is to require that a password be entered if boot options are passed to the boot loader. This is particularly useful because it prevents unauthorized personnel from booting into single-user mode while allowing anyone to boot multiuser mode, say, after a crash. Add the following two lines. Either may be global or per-image.

```
restricted
password=secret
```

Be sure that the configuration file can be read only by root:

```
chmod 600 /etc/lilo.conf
chown root /etc/lilo.conf
```

Another way to guard against single-user mode is to not allow anyone to issue any commands to LILO at the keyboard by setting a timeout of zero in the global commands section at the top of /etc/lilo.conf. (This is a requirement for Orange Boot C2 security).

```
timeout=0
```

Finally, disallow automatic rebooting by adding the line

```
prompt
```

to /etc/lilo.conf, in the global commands section at the top (before the per-image sections). Thus, if a cracker somehow found a way to remotely alter the Master Boot Record, installed a new kernel, or otherwise arranged to create havoc, they cannot boot the new system configuration. Naturally, because Linux is so reliable you should investigate after any crash for the chance that it was cracker-induced.

All of the entries in /etc/lilo.conf for cracker-proofed systems need to be secure-configured kernels, such as Linux kernels or similar. In other words, none of them should offer single-user mode or file systems with lax file permissions. None should be insecure operating systems. For those on non-Intel hardware, there may be similar capabilities.

## 2.16.5 Defeating Theft by the Floppy

![](img/7d04225c75a86d3cf4bd6077596f35b2_138_0.png)

Most people do not take floppies very seriously any more. After all, a 3-1/2-inch floppy holds only 1.44 MB; it would take 14,000 of them to store the data of a common 20 GB disk. Still, it would hold the name, home address, home phone number, and job title of about 10,000 employees, without even using compression, and could make a headhunter

(recruiter) very happy. A floppy could hold a lot of source code, customer lists, or specifications. Plenty of company data has been stolen this way over the years.

Some other ways of stealing data include connecting a modem to a serial port and sending data, or plugging in a printer, parallel-port CD-ROM burner, or disk drive into the parallel port and copying the data. Do consider the possibilities that USB offers, too. The solution to these problems is to enter the CMOS menus as discussed in the past few sections and disable the peripheral devices that are not needed.

## 2.16.6 Defeating Ctrl-Alt-Delete Attacks

![](img/7d04225c75a86d3cf4bd6077596f35b2_139_0.png)

The fixes discussed previously will prevent a physical intruder from being able to intrude. Forcing a reboot or shutting down the system certainly is a DoS attack. On unprotected systems, the standard Ctrl-Alt-Delete sequence will shut the system down in a few seconds.

This sequence can be disabled by commenting out the default entry in /etc/inittab. The entry that has the ctrlaltdel tag that allows it to look like the following:

```
#ca::ctrlaltdel:/bin/shutdown -t5 -rfn now
```

After editing /etc/inittab you need to tell init to reread it with the command `telinit q`.

Alternatively, the shutdown command could be replaced with another one, perhaps a shell script generating e-mail, that will notify you either that a user new to Linux needs your help or someone evil is at the keyboard.

Although there is a /proc/sys/kernel/ctrl-alt-del file starting in the 2.2 kernel, toggling its value between 0 and 1 does not seem to inhibit the system from rebooting when it is given the three-finger salute.
