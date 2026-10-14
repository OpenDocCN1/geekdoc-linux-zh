# Character Devices

You're best off leaving many of these options set, including Virtual terminal and Support for console on virtual terminal (not setting these will cause a system to break).

# Standard/Generic (Dumb) Serial Support

These are the standard PC serial ports that come with almost every computer. Modems, serial mice, UPS devices, and other gadgets hook up to serial ports (or emulate a serial interface).

# Parallel Printer Support

Enables I/O to printers on a parallel port. This only shows up if you select Parallel port support (and most likely will only be useful if you select PC-style hardware as well) under General setup.

# PROBLEM 80

> Symptom: Upon installation of a new kernel, the printer doesn't work anymore.
> 
> Problem: Renamed the printer device.
> 
> Fix: Starting with production release 2.2, printers begin at /dev/lp0 instead of /dev/lp1, so your former /dev/lp1 device file is now /dev/lp0. Usually the only place you have to change this is /etc/printcap.

# Mouse Support (not serial mice)

Selecting this enables a Mice submenu. Most modern mice use the so-called PS/2 port, for which the device is /dev/psaux. This submenu is not for mice that hook up to a serial port.

# Filesystems

It's fairly safe to compile most filesystems as modules, except for the second extended and /proc filesystems (see below); you will almost certainly need to compile these directly into the kernel (in fact, you're not even allowed to build /proc as a module).

# DOS FAT fs Support

Selecting this enables a few filesystems that use FAT, including the MS-DOS file system, UMSDOS (an extended MS-DOS filesystem), and the newer VFAT.