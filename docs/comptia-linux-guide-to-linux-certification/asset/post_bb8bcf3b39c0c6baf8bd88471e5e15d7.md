
The list of shared library directories (/etc/ld.so.conf) and the list of shared libraries (/etc/ld.so.cache) are updated. Alternatively, you can create a variable in your BASH shell called LD_LIBRARY_PATH that lists the directories that contain the shared libraries.

Processes are restricted by a number of constraints that can also prevent them from executing properly. Recall that all processes require a PID from the system process table. Too many processes running on the system can use all available PIDs in the process table; this is typically the result of a large number of zombie processes. Killing the parent process of the zombie processes then frees several entries in the process table.

In addition, processes can initiate numerous connections to files on the filesystem in addition to Standard Input, Standard Output, and Standard Error. These connections are called file handles. The shell restricts the number of file handles that programs can open to 1024 by default; to increase the maximum number of file handles to 5000, you can run the command `ulimit -n 5000`. The `ulimit` command can also be used to increase the number of processes that users can start in a shell; this might be required for programs that start a great deal of child processes. For example, to increase the maximum number of user processes to 30000, you can use the command `ulimit -u 30000`.

To isolate application problems that are related to missing dependencies or restrictions, you should first check the log file produced by the application. Most application log files are stored in the /var/log directory or subdirectories of the /var/log directory named for the application. Even if an application stores its log files elsewhere, it usually hard links its log files to files within the /var/log directory. For example, to view the errors for the Apache daemon, you can view the appropriate log files created by the Apache daemon under the /var/log/httpd directory (Fedora 20) or /var/log/apache2 directory (Ubuntu Server 14.04).

Applications might run into difficulties gaining resources during execution and stop functioning. Often, restarting the process using a SIGHUP solves this problem. This condition might also be caused by another process on the system that attempts to use the same resources. To determine if this is the case, attempt to start the application when fewer processes are loaded, such as in single user-mode (runlevel 1). If resource conflict seems to be the cause of the problem, check the Internet for a newer version of the application or an application fix.

## Operating System-Related Problems

Many software-related problems are related to the operating system itself. These typically include problems with X Windows, boot loaders, and filesystems.

There are many different video card and monitor models today. As a result, some video cards and monitors may not be detected properly by the kernel, or an updated video driver may be required to properly use them with the Linux kernel. If you configure custom display settings and your X Windows or gnome fails to start, you can usually resolve the problems by viewing the Xorg or XFree86 configuration file, or by executing the xwininfo command.

As discussed in Chapter 8, boot loaders can encounter problems while attempting to load the operating system kernel. For the LILO boot loader, placing the word “linear” and removing the word “compact” from the /etc/lilo.conf file usually remedies the problem. For the GRUB and GRUB2 boot loaders, errors are typically the result of a missing file in the /boot directory. Also, ensuring that the Linux kernel resides below the 1024th cylinder of the hard disk and that 32-bit large block addressing (lba32) keyword is specified in the boot loader configuration file typically eliminates BIOS problems with large hard disks.

## Resolving Common System Problems

![](img/c27875544958897d817484d558c208c8_662_0.png)

Because the operating system transfers data to and from the hard disk frequently, the filesystem can become corrupted over time; a corrupted filesystem can be identified by very slow write requests, errors printed to the console, or failure to mount. If the filesystem on a partition mounted to a noncritical directory, such as /home or /var, becomes corrupted, you should perform the following troubleshooting steps:

- Unmount the filesystem if mounted.
- Run the `fsck` command with the `-f` (full) option on the filesystem device.
- If the `fsck` command cannot repair the filesystem, use the `mkfs` command to re-create the filesystem.
- Restore the original data for the filesystem using a backup utility.

![](img/c27875544958897d817484d558c208c8_662_1.png)

If the / filesystem becomes corrupted, the system is unstable and must be turned off. Following this, you can perform the following troubleshooting steps:

- Boot your system from your installation or live media to perform system rescue, as described in Chapter 6.
- At the BASH shell prompt during system rescue, use the `mkfs` command to recreate the filesystem on the appropriate partition or volume that originally hosted the / filesystem.
- At the BASH shell prompt during system rescue, use the appropriate utility (e.g., `tar`, `restore`, or `cpio`) to restore the original data to the recreated / filesystem.
- Boot your system normally following the system rescue.

Some Linux administrators prefer to download a bootable CD, DVD, or USB flash drive-based Linux distribution that contains more filesystem repair utilities than the Fedora installation media. Many small Linux distributions are available on the Internet that are designed for this purpose; one example is Knoppix Linux (www.knoppix.net). Simply download the ISO image for the Linux distribution and write the image to a CD, DVD, or USB flash drive. Following this, you can boot your computer using this CD, DVD, or USB flash drive, and use the utilities on it to repair your / filesystem and restore the files from backup.

## User Interface-Related Problems

Because of the large number of open source productivity software applications available, Linux desktop environments are fast becoming popular within organizations as an alternative to the Windows operating system.

*Note: GRUB2 automatically sets lba32.*

![](img/c27875544958897d817484d558c208c8_663_0.png)

Figure 14-3 The Universal Access utility

In order to use productivity software properly, Linux users need to understand how to use their desktop environment as well as modify it to suit their needs. As a Linux administrator, you may need to assist users with desktop problems. The tools that users can use to modify their desktop experience are collectively called **assistive technologies**. You can configure assistive technologies within Fedora 20 using the **Universal Access utility**, as shown in Figure 14-3. To start this utility within the GNOME desktop environment, open the Activities menu and navigate to Show Applications, Settings, Universal Access.

If you turn on the Always Show Universal Access Menu option shown within Figure 14-3, you can enable and disable each assistive technology using the Universal Access icon in the upper right of the GNOME desktop. Following is a list of the assistive technologies that you can configure within the Universal Access utility or desktop icon:

- High Contrast, which modifies the color scheme to suit those with low vision
- Large Text, which increases the font size of text to suit those with low vision
- Zoom, which allows you to enable magnification for parts of the screen that your mouse follows, as well as modify the color and crosshair effects during magnification
- Screen Reader, which narrates the text on the active window on the screen
- Sound Keys, which beeps when the Num Lock or Caps Lock keys are pressed
- Visual Alerts, which displays a visual alert in place of beep sounds
- Screen Keyboard, which displays an on-screen keyboard that can be used with a mouse
- Typing Assist, which provides three keyboard assistive features:
  - Sticky keys, which simulate simultaneous key presses when two keys are pressed in sequence
  - Slow keys, which add a delay following each key press
  - Bounce keys, which ignore fast duplicate key presses
- Mouse keys, which allow the user to control the mouse using the cursor keys on the keyboard
- Click Assist, which can be used to simulate a right-click by holding down a left-click for a period of time, or trigger a left-click by hovering the mouse pointer over an area of the desktop
