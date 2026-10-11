which shuts down services associated with the current runlevel and starts scripts associated with the runlevel you're switching to.

I ended the chapter by discussing how to specify which services run at each runlevel. This is done using the *inserv* and *chkconfig* commands. The *inserv* command reads the information in the INIT INFO block of an init script to determine which runlevels the associated service should run in by default. The syntax for using *inserv* is *inserv* *service_name*.

In addition to *inserv*, you can also use the *chkconfig* command to manage a daemon's runlevels. Entering *chkconfig -l* will list all services and the runlevels they are configured to run at. To configure a service to start at a particular runlevel, enter *chkconfig -s* *service_name* *runlevels*. To turn off a service, enter *chkconfig* *service_name* off.

# Accelerated Review

+   - In the BIOS phase, the computer's BIOS chip has control of the system.
+   - The BIOS tests the system hardware using the power-on self-test (POST) routine and then locates a storage device with boot files on it.
+   - In the bootloader phase, the BIOS turns control of the system over to a bootloader.
+   - The bootloader points to and loads your operating system's kernel.
+   - The bootloader can reside in the master boot record (MBR) of the boot device or in the boot partition on the drive.
+   - The Linux bootloader may also create a virtual hard drive in your system's RAM, called a ramdisk, and copy a basic root file system to it.
+   - This virtual file system (called the initrd image) is used by the Linux kernel to load the software it needs to access your real storage devices, check them, and mount them.
+   - In the kernel phase, the bootloader loads the operating system into your system RAM from the hard drive or other boot device.
+   - The Linux kernel is located in /boot and is named vmlinuz-version.gz.
+   - LILO used to be the default bootloader used by most Linux distributions.
+   - If you want to install LILO, you must first create an /etc/lilo.conf configuration file; then enter lilo at the shell prompt.
+   - You can use the -b option with the lilo command to specify where GRUB is installed.
+   - You configure LILO using the /etc/lilo.conf file.
+   - After making any configuration changes in this file, you must re-install LILO by entering lilo at the shell prompt.
+   - If you're using Intel Itanium or Apple Macintosh hardware for your Linux system, you'll need to use ELILO instead of LILO.
+   - ELILO is also backward compatible with standard Intel x86 hardware, so you can use it on your traditional Linux system instead of LILO as well.