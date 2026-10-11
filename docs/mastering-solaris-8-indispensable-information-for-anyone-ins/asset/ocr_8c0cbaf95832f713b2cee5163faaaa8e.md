![](bbox=[0.08, 0.12, 0.22, 0.19])

![](bbox=[0.3, 0.12, 0.77, 0.45])

You might have to change the boot device after you install Solaris 8. For example, a Sunstalion 5 workstation boots to the device c0t3 by default, but it can also be set up to boot to c0t0 if a second hard drive is installed in the workstation.

The boot command has several boot options:

**boot -s** The command boot -s starts the server or desktop in the single-user mode. Single-user mode allows the system administrator to enter run level 1 (the default run level is 3).

**boot cdrom -s** One of the most useful commands is boot cdrom -s, entered at the OK prompt with a bootable Solaris disk in your CD-ROM drive. This command runs a memory-based operating system from which you can mount the hard drives and perform system administration.

**boot -a** The command boot -a starts the operating system in interactive mode. This presents the system administrator with several questions regarding the boot process.

**boot -r** The command boot -r checks for new devices and rebuilds the /dev and /devices directories.

**boot -d** The command boot -d runs a very extensive series of diagnostic tests. This topic is covered in Chapter 21, “Troubleshooting.”