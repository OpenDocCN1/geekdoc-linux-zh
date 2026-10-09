store date, time, and other system setup parameters. The CMOS requires power applied to the chip to retain its information. The power required is provided by a small battery on the main board. After the bootable media containing the Linux operating system is found, the BIOS looks for the Master Boot Record (MBR), loads its contents into memory, and passes control to it.

In Chapter 3 we learned that the boot loader was installed in the MBR. The MBR contains instructions on how to load GRUB or LILO, depending on the boot loader you installed. The boot loader takes over the boot process, displays the boot options selected during installation, and allows for user input on which operating system to start up.

# NOTE

The boot loader program contains the boot instructions obtained during installation and stored in /etc/lilo.conf or /boot/grub/grub.conf configuration files. These configuration files are discussed in Chapter 6.

The Linux kernel is loaded into memory and control is passed to it. The kernel contains only the most basic instructions and provides no way for a user to provide input to the system. To continue loading the operating system the init program is executed.

# Init

The Linux kernel finds init in /sbin/init and executes it. The init command controls the remainder of the boot process.

The first thing init does is read the /etc/inittab file. This file contains information on how init should proceed with starting the computer. The /etc/inittab file should have a “sysinit” configuration. This script sets the environment, such as path, starting swap, checking file systems, and other required operating system values. Anything needed to start the system is accomplished by rc.sysinit using the /etc/sysconfig configuration files and scripts to initialize the clock, serial port, and other devices to be used by Linux.

After the sysinit script has completed, init looks in the /etc/inittab file to determine the system’s default runlevel. (Runlevels are discussed later in this chapter.) The inittab performs several tasks, including running the /sbin/update script, which is used to flush dirty buffers back to disk (write all unwritten data to disk).

When the runlevel changes, init uses the scripts in the /etc/rc.d/init.d/ directory to start and stop various services, such as DNS, FTP, DHCP, and others. Init uses the source function library, which spells out how to start or kill a program and how to find out the process ID of a program. Init then determines the current and the previous runlevels. Next, init starts all of the background processes necessary for the system to run by looking in the appropriate rc directory for that runlevel. The rc directory is one of seven directories named /etc/rc.d/rcN.d/, where N is a numerical value between 0 and 6 that represents one of the seven runlevels. The init command then runs each of the kill scripts (kill script names start with a K) with a stop parameter. Init then runs all of the start scripts (start script names begin with an S) in the appropriate runlevel directory with a start so that all services and applications are started correctly.

None of the scripts that actually start and stop the services are located in the /etc/rc.d/rcN.d directory. The scripts in the directory are symbolic links that point to the