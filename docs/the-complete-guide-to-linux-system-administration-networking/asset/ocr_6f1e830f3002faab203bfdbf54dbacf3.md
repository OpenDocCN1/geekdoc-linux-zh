+   Downloaded archive files are typically created and accessed using the tar command. The cpio command is a newer utility that is used (along with tar) to create simple backup files in Linux.

+   By using the find command with tar or cpio, complex file archives can be created with a single command.

# COMMAND SUMMARY

| Command | Description | Example |
|---|---|---|
| chgrp | Changes the group assigned to a file or directory; only root can use this command | chgrp managers report.doc |
| chmod | Changes the access mode (file permissions) of a file or directory, using either character codes or a numeric value | chmod g=rw report.doc |
| chown | Changes the owner and optionally the group assigned to a file or directory, only root can use this command | chown j.taylor.managers report.doc |
| cpio | Creates archives; also reads archive files created by the tar command | cpio -idv < /dev/fd0 |
| df | Displays file system summary information such as device, mount point, percentage used, and total capacity | df -h |
| fdformat | Formats a 3.5-inch disk | fdformat /dev/fd0 |
| find | Searches the file system for files matching given characteristics | find /home -name "report.doc" -print |
| groups | Lists all the groups of which the currently effective UID (current user) is a member | groups |
| gunzip | Uncompresses a file that has been compressed using gzip | gunzip archive.gz |
| gzip | Compresses files on a Linux system | gzip archive |
| id | Displays the currently effective UID, GID, and groups of which the effective UID is a member | id |
| ln | Creates a hard or symbolic (soft) link | ln -s /etc/profile /home/nwells/main_profile |
| logname | Displays the user name used to log in to Linux (which may differ from the currently effective UID as displayed by the whoami or id commands) | logname |