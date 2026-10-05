/etc Machine–local system configuration files Holds administrative, configuration, and other system files. The most important is /etc/passwd, which contains a list of all users who have permission to use the system.

/etc/opt Configuration files for add-on software packages kept in /opt

/etc/X11 Machine–local configuration files Each user's home directory is typically one of many subdirectories of the /home directory. As an example, assuming users' directories are under /home, the absolute pathname of Zach's home directory is /home/zach. On some systems the users' directories may not be found under /home but instead might be spread among other directories such as /inhouse and /clients.

/lib Shared libraries

/lib/modules Loadable kernel modules

+   - /mnt Mount point for temporarily mounting filesystems

+   - /opt Add-on (optional) software packages

+   - /proc Kernel and process information virtual filesystem

+   - /root Home directory for the root account

+   - /sbin Essential binaries Utilities used for system administration are stored in /sbin and /usr/sbin. The /sbin directory includes utilities needed during the booting process, and /usr/sbin holds utilities used after the system is up and running. In older versions of Linux, many system administration utilities were scattered directories that often included other system files (/etc, /usr/bin, /usr/adm, /usr/include).

+   - /sys Device pseudofsystem udev on page 502 for more information.

+   - /tmp Temporary files

+   - /usr Second hierarchy Traditionally includes subdirectories that contain information used by the system. Files in /usr subdirectories do not change often and may be shared by several users.

+   - /usr/bin Most commands Contains the standard Linux utility programs—that is, binaries that are not needed in recovery mode (page 445).

+   - /usr/games Games and educational programs

+   - /usr/include Header files included by C programs

+   - /usr/local Local hierarchy Holds locally important files and directories that are added to the system. Subdirectories include bin, games, include, lib, sbin, and src.

+   - /usr/sbin Nonvolatile system administration binaries Seesbin.

+   - /usr/share Architecture-independent data Subdirectories can include dict, doc, games, info, locale, man, misc, termino, and zoneinfo.