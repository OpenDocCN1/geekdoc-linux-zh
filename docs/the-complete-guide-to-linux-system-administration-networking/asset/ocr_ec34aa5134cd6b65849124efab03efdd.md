| Command | Description | Example |
|---|---|---|
| mount | Makes a logical or physical device (such as a CD-ROM or 3.5-inch diskette) available as a file system in the Linux directory structure | mount /mnt/cdrom |
| newgrp | Temporarily changes the effective group of a logged in user analogous to the su command, but for group membership rather than user identity | newgrp managers |
| stat | Displays information about a file or directory taken from the corresponding inode, such as the file size, permissions, last access and modification times, and the device where the file is stored | stat /etc/profile |
| su | Changes your effective UID, taking on the identity of a different user than the one used to log in; (stands for substitute user) | su - |
| tar | Creates a single file that contains many other files, often compressed to save space | tar cvzf home_archive.tgz /home |
| umask | Blocks default file permissions that would otherwise be assigned when creating a new file or directory | umask -S |
| umount | Unmounts a file system that is currently accessible as part of the Linux directory structure | umount /mnt/cdrom |
| vigr | Safely edits the /etc/group file | vigr |
| vipw | Safely edits the /etc/passwd file | vipw |
| w | Lists all users currently logged in, with details about the programs each is running | w |
| who | Lists all users currently logged in, with details about from where each is logged in | who |
| whoami | Displays the currently effective UID | whoami |

# Key Terms

/etc/group — A configuration file in which group information (group names and membership lists) is stored.

/etc/passwd — A configuration file in which user account information is stored.