/bin  A link to /usr/bin.

/boot  **Static files of the boot loader** Contains all of the files needed to boot the system.

/dev  **Device files** Contains all files that represent peripheral devices, such as disk drives, terminals, and printers. Previously this directory was filled with all possible devices. The *udev* utility (page 516) provides a dynamic device directory that enables /dev to contain only devices that are present on the system. See also /dev on page 503.

/etc  **Machine-local system configuration files** Holds administrative, configuration, and other system files.

/etc/opt  **Configuration files for add-on software packages kept in /opt**

/etc/X11  **Machine-local configuration files for the X Window System**

/home  **User home directories** Each user’s home directory is typically one of many subdirectories of the /home directory. As an example, assuming that users’ directories are under /home, the absolute pathname of Zach’s home directory is /home/zach. On some systems the users’ directories might not be found under /home but instead might be spread among other directories such as /inhouse and /clients.

/lib  A link to /usr/lib.

/lib64  A link to /usr/lib64.

/lib/modules  **Loadable kernel modules**

/mnt  **Mount point for temporarily mounting filesystems**

/opt  **Add-on (optional) software packages**

/proc  **Kernel and process information virtual filesystem**

/root  **Home directory for the root account**

/run  **Runtime (volatile) data** A tmpfs filesystem (mounted, but stored in RAM) that holds startup files previously hidden in /dev and other directories. For more information see lists.fedoraproject.org/pipermail/devel/2011-March/150031.html.

/sbin  A link to /usr/sbin.

/sys  **Device pseudofilesystem** See *udev* on page 516 for more information.

/tmp  **Temporary files**

/usr  **Installed system** Includes subdirectories that contain information used by the system. Files in subdirectories do not change often and can be shared by several systems.

/usr/bin  **Most user commands** Contains the standard Linux utility programs.

/usr/sbin  **Essential system binaries** Utilities used for system administration.

/usr/games  Games and educational programs

/usr/include  **Header files included by C programs**

/usr/lib  **Shared libraries (32-bit)**