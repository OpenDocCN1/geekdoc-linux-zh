+   18. Shared libraries are located in /lib, /usr/lib, and /usr/X11/lib by default. When a library error occurs, run the ldconfig program, which reads the /etc/ld.so.conf file for library locations and writes a common cache of library locations in /etc/ld.so.cache. The ld program reads a binary and reports back its library dependencies. If a user needs to reference a library, she uses the LD_LIBRARY_PATH variable.

+   19. Debian Package Management uses the dpkg program to install, delete, and query packages. The dselect program is a front end for the dpkg program, providing a menu for all options. The apt-get program is for automated updates and reads the sources from /etc/apt/sources.list file. The Debian package database is kept in /var/lib/dpkg.

+   20. Red Hat Package Management uses the RPM program to install, remove, and query packages. The RPM database is kept in /var/lib/rpm and is rebuilt with rpm -rebuild. RPM packages come in precompiled and source packages.

# GNU and Unix Commands

+   21. Commands take the following format: command -options arguments, and some options can be placed at the end of the command.

+   22. Commands use > redirection for input and write standard output to a file with > redirection.

+   23. sed can search and replace words and phrases, but tr can only do individual characters.

+   24. grep uses -i for case insensitivity, -r for recursive searches, -n for line numbering, and -v for reversing the output.

+   25. stdin is Stream 0, stdout is stream 1, and stderr is stream 2. You can redirect any and all with 1> and 2>, but to send both stdout and stderr to the same place, you use 2>&1.

+   26. Use & after a command to send it to the background, Ctrl+z to suspend a running program, and bg to send it to the background. A job in the jobs command output with a + symbol is the current job (the one with the - symbol is the previous job. Any fg or bg command acts on the current job by default. Kill a job, where $j is the job number to end a job.

+   27. Start a job with a lowered priority with the nice command, and alter a running command's priority with the renice command. By default, nice drops the priority by a value of 10 and renice sets a priority and doesn't take a default. Programs are started by default with a priority, and priorities range from -20 (highest) to 20 (lowest).

+   28. vi uses hjkl for cursor movement. Remember h = left, j = down, k = up, and l = right. vi offers three modes: command, insert, and lastline or ex mode.

# Devices, Linux File Systems, and FHS

+   29. mkefs is a front end for the mkfs— file system-specific tools. Use mke2fs /dev/hd10 to create a default ext2 file system on device /dev/hdb. Use the -m option to reserve space for the root user. Use the -j option to create an ext3 journal for the file system.

+   30. fsck checks file systems when they are mounted read-only or unmounted. fsck has five passes and can ask for manual intervention.

+   31. The /etc/fstab file has six columns (device, mount point, file system type, options, dump time, and fsck order) and is used by the root user to set options for file systems, and to allow users to mount and unmount file systems.

+   32. The user keyword in the /etc/fstab options column allows only the user who mounted a file system to unmount it, whereas the users (plural) keyword allows any valid user with the right permissions to the mount yield to mount and unmount the file system.

+   33. The /etc/mtab file is a table of mounted file systems. The mount command by itself, the cat /proc/mounts command, and cat /etc/mtab show the mounted file systems for the machine.

+   34. Quotas are on a file system-by-file system basis. The a quota.user and a quota.group files must be created in the root of the file system. Edit the /etc/fstab and put the usrquota and grpquota in the options column for the file system, and then remount the file system. Then run the quotacheck program to populate quota.user/quota.group. Run edquota -u username to set the user's quota limits, use the -o option for a grace period, and then run quotao -u or quotoa.filesystem to start the quota subsystem. Users can check their own quotas with quota, and the root user can check all quotas with repquota.

+   35. File permissions are arranged in three trios: user, group, and other. Permissions are read from left to right, and the first match of your UID or group ID is the set of permissions you are locked into.

+   36. There must be a user owner and group owner for any file object. Change the ownership with the chown command, can act on user or group ownership, or change both the group owner with the chgrp command. If a SGID special bit is set on a directory, the group ownership of the directory cascades to all created objects.

+   37. Hard links are multiple names for the same inode and file; soft or symbolic links are a separate object with its own inode that points to another file. Hard links cannot span file systems, whereas symbolic links can span file systems and enable you to move data without disrupting users' access.

+   38. The find command is a real-time command and relatively slow but very accurate. The locate command is database-driven and very fast but returns a hit for every instance of the search term, wherever it occurs. find uses many options and can execute commands on the items it finds with the -exec option. locate can be configured to not show files or directory trees by configuring the /etc/updatedb.conf file.