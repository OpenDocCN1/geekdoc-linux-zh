
10. Which file system type supports journalizing?
- a. ext2
- b. ext3
- c. swap
- d. vfat
- e. LVM

11. True or False: The three usable classes of IP addresses are A, C, and E.

12. Which file system type supports dynamic sizing?
- a. ext2
- b. ext3
- c. swap
- d. vfat
- e. LVM

13. The ______ boot loader is a DOS-based utility to load the Linux kernel.
- a. GRUB
- b. LILO
- c. SYSLINUX
- d. LOADLN

14. True or False: By default, the High setting for Linux firewall allows only DNS and DHCP connections.

15. The class ______ IP address range is from 192.0.0.0 to 223.255.255.255.
- a. A
- b. B
- c. C
- d. D
- e. E

16. True or False: MD5 passwords allow up to eight character passwords.

17. True or False: The server used for the X windowing system is xfree86.

18. The four leftmost bits of a class A address are ______. (An X represents any number.)
- a. 0XXX
- b. 10XX
- c. 110X
- d. 1110
- e. 1111

19. The superuser account is called ______.
- a. /
- b. root
- c. administrator
- d. super_user

20. Which of the following is a centralized hierarchical database used for authentication?
- a. Shadow passwords
- b. MD5 passwords
- c. NIS
- d. LDAP
- e. Kerberos

21. The command used to halt the system immediately is ______.
- a. shutdown -n now
- b. shutdown -r now
- c. shutdown -h now
- d. reboot -r now

22. True or False: A pixel is a single point in a graphic image.

## Linux System
Administration Basics

CHAPTER 4

### CHAPTER OBJECTIVES
- Create and delete users
- Modify existing users
- Create, modify, and delete groups
- Change permissions and modes with chmod, chown, and chgrp commands
- Manage and navigate the Linux hierarchy
- Manage and navigate the standard Linux file system
- Perform administrative tasks while logged in as root using the su command
- Mount and manage file systems and devices
- Manage runlevels using init and shutdown

## THE BOOT PROCESS, INIT, AND SHUTDOWN

All Linux distributions have an interesting method of starting and stopping the operating system. Linux uses runlevels to specify which programs will start and stop. These runlevels define which programs will be started during the boot process and the processes that are required to perform a graceful shutdown. Understanding the boot process, init, and shutdown will help in troubleshooting the Linux operating system.

### The Boot Process

The first thing a computer does when it powers up is perform Power On Self Test (POST). POST checks memory, ATA and SCSI devices, video, keyboard, and other devices. If a problem exists within the computer, a message is displayed and, depending on the severity of the error, you are prompted to press a key to continue system startup. POST is performed by the Basic Input/Output System (BIOS).

The BIOS is built-in software that determines what a computer can do without accessing programs from a disk. On PCs, the BIOS contains all the code required to control the keyboard, display screen, disk drives, and other devices attached to the computer.

The ROM is stored on a Read Only Memory (ROM) chip on the computer's main board. ROM chips contain permanently written software. Using the ROM to store the BIOS ensures that the BIOS program is always available. ROM programs load much quicker than disk-based programs and are not subject to mechanical errors. The BIOS program performs work that typically will never change for the life of the PC. The BIOS has changed very little since it was first used in PCs, but newer PCs use Plug-and-Play (PnP) devices that require periodic changes to work with certain operating systems. PnP BIOS systems use a flash memory chip, which can be updated if necessary.

After testing the system, BIOS will look for bootable media that contains instructions defining the next steps in the boot process. The order of the bootable media can be set in the PC's Complementary Metal Oxide Semiconductor (CMOS). CMOS is used by PCs to store date, time, and other system setup parameters. The CMOS requires power applied to the chip to retain its information. The power required is provided by a small battery on the main board. After the bootable media containing the Linux operating system is found, the BIOS looks for the Master Boot Record (MBR), loads its contents into memory, and passes control to it.

In Chapter 3 we learned that the boot loader was installed in the MBR. The MBR contains instructions on how to load GRUB or LILO, depending on the boot loader you installed. The boot loader takes over the boot process, displays the boot options selected during installation, and allows for user input on which operating system to start up.

### NOTE

The boot loader program contains the boot instructions obtained during installation and stored in /etc/lilo.conf or /boot/grub/grub.conf configuration files. These configuration files are discussed in Chapter 6.

The Linux kernel is loaded into memory and control is passed to it. The kernel contains only the most basic instructions and provides no way for a user to provide input to the system. To continue loading the operating system the init program is executed.

### Init

The Linux kernel finds init in /sbin/init and executes it. The init command controls the remainder of the boot process.

The first thing init does is read the /etc/inittab file. This file contains information on how init should proceed with starting the computer. The /etc/inittab file should have a “sysinit” configuration. This script sets the environment, such as path, starting swap, checking file systems, and other required operating system values. Anything needed to start the system is accomplished by rc.sysinit using the /etc/sysconfig configuration files and scripts to initialize the clock, serial port, and other devices to be used by Linux.

After the sysinit script has completed, init looks in the /etc/inittab file to determine the system’s default runlevel. (Runlevels are discussed later in this chapter.) The inittab performs several tasks, including running the /sbin/update script, which is used to flush dirty buffers back to disk (write all unwritten data to disk).

When the runlevel changes, init uses the scripts in the /etc/rc.d/init.d/ directory to start and stop various services, such as DNS, FTP, DHCP, and others. Init uses the source function library, which spells out how to start or kill a program and how to find out the process ID of a program. Init then determines the current and the previous runlevels. Next, init starts all of the background processes necessary for the system to run by looking in the appropriate rc directory for that runlevel. The rc directory is one of seven directories named /etc/rc.d/rcN.d/, where N is a numerical value between 0 and 6 that represents one of the seven runlevels. The init command then runs each of the kill scripts (kill script names start with a K) with a stop parameter. Init then runs all of the start scripts (start script names begin with an S) in the appropriate runlevel directory with a start so that all services and applications are started correctly.

None of the scripts that actually start and stop the services are located in the /etc/rc.d/rcN.d directory. The scripts in the directory are symbolic links that point to the actual scripts located in the /etc/rc.d/init.d directory. A symbolic link is just a file that points to another file. Symbolic links are used in the runlevel directories so that the files can be created and deleted without affecting the actual script. The order in which the scripts are executed is determined by the number after the K or S in the script filename. To execute one script before another, simply number the first script with a smaller number than the second. In Figure 4–1 the program S12syslog is executed before S13partmon, and so on.

![](img/37f079cee226b270f2e09b37a2e4a05d_93_0.png)

After init has progressed through all of the runlevels, the /etc/inittab script forks a getty process for each virtual console for each runlevel (runlevels 2 through 5 get all six consoles; runlevel 1 gets only one console; runlevels 0 and 6 get no virtual consoles). A getty is a program that handles the login process from a text-mode console or serial port. The /etc/inittab also tells init how to handle a user hitting the Ctrl+Alt+Delete key sequence. By default most Linux distributions execute the command /sbin/shutdown -h -r now, which cleanly shuts down the system and prevents disk corruption. The /etc/inittab also tells init what it should do in case of power failures when a compatible UPS is attached to the system. If there is an Uninterruptible Power Supply (UPS), it can run the system until power gets so low that it can no longer guarantee the system will stay running; then it shuts down the system without user intervention.

Depending on the runlevel set, the system will be at either a GUI or a command-line login prompt.

### Runlevels

By providing multiple runlevels, Linux can easily be optimized for peak performance depending on its current use. Running the Linux operating system from a GUI interface takes a lot of system resources. On a server, the GUI is seldom used and can be eliminated by using runlevel 3. If system maintenance, such as fixing a hard disk problem, is required, run-level 1 can be entered to prevent networking, and thus no other users can be on the system. By assigning services to start in particular runlevels different modes can be entered without worrying about manually starting or stopping services.

Linux usually operates in runlevel 3 or 5. Runlevel 3 is full multiuser mode with a command-line interface, and runlevel 5 is the same with a GUI. The following runlevels are available in Linux:

- 0 Halt
- 1 Single-user mode
- 2 Not used (user-definable)
- 3 Full multiuser mode
- 4 Not used (user-definable)
- 5 Full multiuser mode with an X-based login screen (GUI)
- 6 Reboot

The default runlevel is configured in the /etc/inittab file. If you view the file, a line similar to `id:5:initdefault:` appears near the top, as seen in Figure 4–2. To change the runlevel, change the number 5 to whatever runlevel you want to typically start the system.
