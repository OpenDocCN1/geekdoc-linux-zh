/dev/rdsk Raw disk device files.

/dev/rmt Remote tape management files.

/dev/sad Links to the STREAMS Administrative Driver (SAD).

/dev/sound Audio device files.

/dev/swap Default swap device.

/dev/term Terminal devices.

/devices directory Contains device files subtrees. There are links in /dev that point to the files in this directory.

/etc directory The /etc directory (pronounced "e-tee-c" or "et-ec-cee," but never "etcetera") stores platform-dependent local administrative and configuration files that define a system’s local identity. In this directory, you will find files such as passwd, a system user database; vstab, a list of devices that the file system can mount; hosts, a correlation file for system names and their related IP addresses and the location of the IP address provider; and profile, the system shell configuration file. Some of the important files found in the /etc directory, albeit not all of them, are listed here:

/etc/aliases Here the mail system sendmail creates aliases for users. The /etc/aliases directory is a symbolic link to the /etc/mail/aliases directory.

/etc/dumpdates Contains information about the use of ufsdump backups.

/etc/group This file contains group information.

/etc/inittab This file contains an initialization table that specifies processes to run at boot-up, as well as the run level the system boots up into.

/etc/magic This file lists file types and assignments.

/etc/mntab The mount table lists all mounted devices.

/etc/passwd This file that stores the list of users for a system and the location of the users’ home directories and the shells that they use. Passwords are now kept in a shadow directory.

/etc/power.conf This file is used for power management.

/etc/printers.conf This file is used to control the printer subsystem.

/etc/profile The profile file used by the system login shell initialization script (Bourne and Korn shells).

/etc/.login The .login file is used by the system login shell initialization script (C shell).