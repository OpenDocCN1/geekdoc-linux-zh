| Prompt | Description | |
| :--- | :--- | |
| `L<span>` | `nn` represents one of 16 disk-error codes. | |
| `LI` | The second-stage bootloader loaded, but could not run. | |
| `LIL` | The descriptor table could not be read. | |
| `LIL?` | The second-stage bootloader loaded at an incorrect address. | |
| `LIL` | LILO found a corrupt descriptor table. | |
| `LILO` | LILO ran successfully. | |

Disk error codes can indicate problems such as an open floppy door, a drive timeout, a controller error, a media problem, a BIOS error, or even transient read problems (which can be overcome by rebooting). Overall, some common problems with LILO include

+   - Not rerunning /sbin/lilo following a kernel change
+   - Incorrect use of /sbin/lilo in creating a new boot map
+   - Installing and booting Linux from a very large (2GB+) partition
+   - Installing another operating system (such as Windows 95, which overwrites the MBR) after installing Linux and LILO
+   - Errors in /etc/lilo.conf after manual edits
+   - A corrupted MBR
+   - Installation of LILO in a Linux swap partition (which should be impossible)
+   - A missing Linux kernel image (error in /etc/lilo.conf)
+   - Installing Linux on and booting from a DOS partition and then defragmenting the DOS partition
+   - Passing incorrect kernel messages at the LILO: prompt

If you run into trouble, definitely pursue Almesberger's readme file, found under the `/usr/share/doc/lilo` directory. Take his advice: Don't panic! With a little forethought, detection, and perseverance, you should be able to avoid or overcome problems.

# Using LOADLIN.EXE to Boot Linux

LOADLIN.EXE is a program that uses the DOS MBR to boot Linux. This handy program by Hans Lermen also passes along kernel options. LOADLIN.EXE is very helpful when you must boot from DOS to properly initialize modems or sound cards to make them work under Linux.