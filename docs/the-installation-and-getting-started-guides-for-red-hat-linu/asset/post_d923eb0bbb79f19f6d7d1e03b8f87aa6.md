
## Appendix C: Package List

### etcskel — (Version 1.6, 2K)

[B]

The etcskel package is part of the basic Red Hat system. Etcskel provides the /etc/skel directory's files. These files (.Xdefaults, .bash_logout, .bash_profile, .bashrc) are then placed in every new user's home directory when new accounts are created.

### filesystem — (Version 1.3.4, 80K)

[B]

The filesystem package is one of the basic packages that is installed on a Red Hat Linux system. Filesystem contains the basic directory layout for a Linux operating system, including the correct permissions for the directories.

### genromfs — (Version 0.3, 12K)

Genromfs is a tool for creating romfs filesystems, which are lightweight, read-only filesystems supported by the Linux kernel.

### info — (Version 3.12f, 245K)

[B]

The GNU project uses the texinfo file format for much of its documentation. The info package provides a standalone TTY-based browser program for viewing texinfo files. You should install info, because GNU's texinfo documentation is a valuable source of information about the software on your system.

### initscripts — (Version 3.98, 148K)

[B]

The initscripts package contains the basic system scripts used to boot your Red Hat system, change run levels, and shut the system down cleanly. Initscripts also contains the scripts that activate and deactivate most network interfaces.

board address and interrupt assignments. The cards also contain descriptions of the resources which need to be allocated. The BIOS on your system, or isapnp tools, uses a protocol described in the specification to find all of the PnP boards and allocate the resources so that none of them conflict. Note that the BIOS doesn't do a very good job of allocating resources. So isapnptools is suitable for all systems, whether or not they include a PnP BIOS. In fact, a PnP BIOS adds some complications. A PnP BIOS may already activate some cards so that the drivers can find them. Then these tools can unconfigure them or change their settings, causing all sorts of nasty effects. If you have PnP network cards that already work, you should read through the documentation files very carefully before you use isapnptools. Install isapnptools if you need utilities for configuring ISA PnP cards.

### kbdconfig — (Version 1.9, 40K)

[B]

The kbdconfig utility is a terminal mode program for setting the keyboard map for your system. Keyboard maps are necessary for using any keyboard besides the US default keyboard. Kbdconfig will load the selected keymap before exiting and configure your machine to use that keymap automatically after rebooting. You should install kbdconfig if you need a utility for changing your keyboard map.

### ld.so — (Version 1.9.5, 247K)

[B]

This package contains the shared library configuration tool, ldconfig, which is required by many packages. It also includes the shared library loader and dynamic loader for Linux libc 5.

### ldconfig — (Version 1.9.5, 223K)

[B]

Ldconfig is a basic system program which determines run-time link bindings between ld.so and shared libraries. Ldconfig scans a running system and sets up the symbolic links that are used to load shared libraries properly. It also creates a cache (/etc/ld.so.cache) which speeds the loading of programs which use shared libraries.

### lilo — (Version 0.21, 1,095K)

[B]

LILO (Linux LOader) is a basic system program which boots your Linux system. LILO loads the Linux kernel from a floppy or a hard drive, boots the kernel and passes control of the system to the kernel. LILO can also boot other operating systems.

### logrotate — (Version 3.1, 52K)

[B]

The logrotate utility is designed to simplify the administration of log files on a system which generates a lot of log files. Logrotate allows for the automatic rotation compression, removal and mailing of log files. Logrotate can be set to handle a log file daily, weekly, monthly or when the log file gets to a certain size. Normally, logrotate runs as a daily cron job. Install the logrotate package if you need a utility to deal with the log files on your system.

### losetup — (Version 2.9, 8K)

[B]

Linux supports a special block device called the loop device, which maps a normal file onto a virtual block device. This allows for the file to be used as a "virtual file system" inside another file. Losetup is used to associate loop devices with regular files or block devices, to detach loop devices and to query the status of a loop device.

### mailcap — (Version 2.0.1, 34K)

[B]

The mailcap file is used by the metamail program. Metamail reads the mailcap file to determine how it should display non-text or multimedia material. Basically, mailcap associates a particular type of file with a particular program that a mail agent or other program can call in order to handle the file. Mailcap should be installed to allow certain programs to be able to handle non-text files.

### man — (Version 1.5f, 217K)

[B]

The man package includes three tools for finding information and/or documentation about your Linux system: man, apropos and whatis. The man system formats and displays on-line manual pages about commands or functions on your system. Apropos searches the whatis database (containing short descriptions of system commands) for a string. Whatis searches its own database for a complete word. The man package should be installed on your system because it is the primary way for finding documentation.

### mgetty — (Version 1.1.14, 845K)

The mgetty package contains a "smart" getty which allows logins over a serial line (i.e., through a modem). If you're using a Class 2 or 2.0 modem, mgetty can receive faxes. If you also need to send faxes, you'll need to install the sendfax program. If you'll be dialing in to your system using a modem, you should install the mgetty package. If you'd like to send faxes using mgetty and your modem, you'll need to install the mgetty-sendfax program. If you need a viewer for faxes, you'll also need to install the mgetty-viewfax package.
