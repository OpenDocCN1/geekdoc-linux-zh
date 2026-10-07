
## General Troubleshooting Techniques

- Be patient and methodical. You're unlikely to find solutions in the last few hours of a 12-hour troubleshooting session. You can probably no longer look at the problem methodically after so long. Rest your brain and your eyes, and then try again. Don't forget to eat and sleep!

- If something worked yesterday but suddenly doesn't work today, it is probably not a configuration problem. Again, look at `/var/log/messages` to see if there is a message that will point to the problem. Check anything that has changed since the last time it worked to determine whether something changed caused the error. If you still don't find it (and you know no one has changed the configuration from the working one), don't spend a lot of time reworking configuration files; consider hardware.

- Remember that many services have a debugging switch that allows you to pass in parameters and/or increases the number of messages that the service logs to `/var/log/messages`. Also use the verbose switch wherever it exists to ensure that you receive the most information possible about what the service is doing. Some services have syntax checkers (for example, `tcpchk` for networking) to determine whether the configuration files have errors. `tcp` has a great utility called `tcpmatch`, which allows you to see whether your system would accept connections from a hostname that you pass as a parameter.

- Remember many services depend on the ability to look up an IP address from a hostname with `nslookup` or even look up a hostname in reverse with `nslookup` (reverse lookup).

Login programs are often due to an error in the related PAM file:

```
login      /etc/pam.d/login
rlogin    /etc/pam.d/rlogin
KDM       /etc/pam.d/kdm
GDM       /etc/pam.d/gdm
XDM       /etc/pam.d/xdm
SSH       /etc/pam.d/sshd
```

- When specifying a library path, ensure that you've spelled everything correctly and that the case is correct.

- The compiler never lies, although it can obfuscate. If you have an error message that you don't understand, there is a problem in the code. The compiler may interpret the true source of the problem as being OK, though, and report an error on some lines later, when the compiler's interpretation finally breaks down. Compiler messages are also just plain cryptic. Look to determine what the error means. To confuse the issue a bit, bad hardware sometimes cause the compiler to give you an error that might send you down the wrong path.

![](img/4fb617eb648f87def380ef5d9205d01_634_0.png)

- Simply rebooting is not a good fix. If you dont know what caused the problem and rebooting fixes it, you still won't know what caused it the next time. Find the problem and fix it. You might need to restart a service or a daemon, but at least if it fixes, it guides you into the problem space, allowing you to find the solution.

- Join a Linux user group if there is one in your area. If isnt one, start one. The exposure you get to different problems will help you avoid those problems.

- Remember to sync any changes you make in rescue mode before you exit. This writes any residual information to the hard drive. Do not making your "fix" to be lost after a reboot.

- Don't be afraid of the system. Very few things that are going to break the computer (except getting madd and throwing it on the floor). Experiment a bit. Log each step so that you can undo what you do.

- Make sure you have a boot disk or rescue disk or CD-ROM. Of course you dont want to delete files with reckless, but it is OK to copy something to another partition and remove the suspect file to see if it fixes the problem. If you mess badly, boot into rescue mode and copy the files where they go and reboot.

The rest of the chapter looks at common problems and their solutions, distribution-independent. There are many Frequently Asked Questions (FAQ) documents that provide information about specific areas. Look for a FAQ whenever you are preparing to configure something for the first time. If there is not, rely instead on a HOWTO.

## Boot Problems

The problems discussed in this section prevent the system from booting fully. Boot problems are among the most frustrating, but they are also the easiest to troubleshoot since the problem space is relatively restricted. If you know the boot process inside out, the symptoms of the problem tend to point to one or two possible solutions. At that point, troubleshooting the problem becomes easy. Find some indicator of which problems you are dealing with and fix it.

## LILO Messages and Their Meanings

Chapter 18 briefly discussed the fact that on startup, LILO prints one letter for each task it has to do. Therefore, if only one or two letters print out, the process aborted at whatever it was trying to accomplish. To begin troubleshooting, you have to take a closer look at the meaning of LILO's startup display.

| Display | Diagnosis |
| :--- | :--- |
| LILO hasn't been loaded | It may not be installed, or some process failed. For instance, the Linux partition might not be active or might have been selected by an earlier boot loader. |
| (nothing) | The main part of LILO has loaded, but is unable to locate the second-stage boot loader, /boot/b. The two-digit error code can help further diagnose the problem, as detailed in LILO documentation. |
| error-code | The main part of LILO has loaded and can locate the second-stage boot loader, /boot/b; but this second-stage loader won't run. This problem is frequently caused by a mismatch between the BIOS's disk geometry settings and those used by Linux. (See below for a description of disk geometry.) |
| LILO | When LILO returns a string at bootup, the problem is that LILO can't locate your kernel image. This is usually caused by recompiling the kernel and copying the new one over the old without running LILO again. Since LILO only reads /etc/lilo.conf and writes a new boot sector onto your hard drive when you run it, if the system boots, it must be rerun to update that boot sector /etc/lilo.conf changes. If you forget to do this, the system will not boot. To fix this, use an install/rescue floppy, mount the root directory on /mnt and rerun with LILO using the command lilo -r /mnt. An alternative is to boot from an install/rescue floppy, mount the root directory on /mnt, rerun the command chroot /mnt to make the system treat /mnt as the root directory, and run LILO normally. |
| LILO, etc. | The second-stage boot loader runs but can't function properly. This frequently indicates a geometry mismatch or a problem with the hard disk. |
| LILO | LILO has loaded the second-stage boot loader into the wrong address. This is usually caused by moving /boot/boot.b without rerunning LILO. |
| LILO? | LILO has detected a damaged descriptor table, /boot/map. This can be caused by disk geometry mismatch or by moving the descriptor file without rerunning LILO. |
| LILO- | The program has loaded and run correctly. Subsequent problems are likely related to the kernel or other Linux startup files. |

![](img/4fb617eb648f87def380ef5d9205d01_636_0.png)
![](img/4fb617eb648f87def380ef5d9205d01_636_1.png)

NOTE Hard disks are composed of one or more platters, each of which has associated one or two heads. These heads move across several different tracks, forming virtual cylinders across the stacked platters. Each cylinder is broken into multiple sectors, each of which holds 512 bytes on most hard disks. Early hard disks could be defined by the number of cylinders, heads, and sectors they used; hence the term CHS geometry or disk geometry. The x86 BIOS and the standard x86 partitioning table use this method of describing a disk. The trouble is that all modern hard disks lie about their CHS geometries. Furthermore, the lies told by them sometimes cause problems; BIOSes and OSs frequently change these lies to others. With such fabrication occurring, the situation sometimes lapses in chaos when two different software components believe different things about the disk's geometry. This can be the source of some LILO problems, if LILO uses one CHS geometry setting and another tool using another setting.

## Making the System Boot a New Kernel

To change the boot kernel from linux to linux_new, edit the /etc/lilo.conf file to change the `default=` line to `default=linux_new`. If you don't see a default line, simply add one. Not long ago, lilo simply took the first listed kernel image as the default image; older lilo.conf files won't have the default parameter. Don't forget to rerun /sbin/lilo after you make any changes to the /etc/lilo.conf file.

Here is a sample /etc/lilo.conf file:

```
boot=/dev/hda
map=/boot/map
root=/dev/hda1
install=/boot/boot.b
prompt
timeout=50
message=/boot/message
linear
default=linux
image=/boot/vmlinuz-2.2.16-22
label=linux
read-only
```
