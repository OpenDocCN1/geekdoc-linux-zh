+   - The /var/log directory contains log files while /var/spool contains mail and printing files.

+   - The /bin directory holds binaries used during setup, and /sbin has binaries used by the root user.

+   - The / directory is the root directory, and it contains all other directories. The /root directory is the home directory for the root user. The /home directory contains the users’ home directories. /boot stores the kernel and other files used by the boot loader. The /dev directory stores the devices used on the system, and the /proc directory is a virtual directory containing system information.

+   - The find utility is used to locate files matching the specified criteria.

+   - The locate utility uses the slocate database to index and search for files on the system. This database is updated using the updatedb command.

+   - The which utility is used to display the path of a specified command.

+   - The whereis command searches specific locations for the specified file and manual page entries.

+   - Links function as pointers to files. Hard links cannot span file systems, and changes to a soft link occur in all links to that file.

+   - Permissions are granted to users and group accounts using numeric and letter values.

+   - The chown command is used to change ownership of files and directories while the chgrp command is used to change the group assignment of files and directories.

+   - The chmod command is used to change permissions on files and directories.

+   - The umask is used to set the default permissions for newly created files.

+   - The SUID and SGID permissions allow files to be executed using a different user or group account.

+   - The sticky bit is used to allow only an owner to delete files and directories while allowing other users to write to them.

+   - The tar utility allows files to be archived as a single file and for this file to be compressed or uncompressed in one step.

+   - The gzip, gunzip, compress, and bzip2 utilities are used to compress and uncompress files.

+   - Quotas are viewed with quota and repquota. They are enabled with quotaon, disabled with quotaoff, and edited using edquota.