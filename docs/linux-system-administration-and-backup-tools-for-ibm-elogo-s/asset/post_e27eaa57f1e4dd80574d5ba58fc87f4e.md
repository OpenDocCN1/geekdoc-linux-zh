
## 5.5.2 Adding new users

| Username | UID | GID | Password | Home Dir |
|---|---|---|---|---|
| root | 0 | 0 | Normal | /root |
| bin | 1 | 1 | Disabled | /bin |
| daemon | 2 | 2 | Disabled | /sbin |
| adm | 3 | 4 | Disabled | /var/adm |
| lpd | 4 | 7 | Disabled | /var/spool/lpd |
| spdc | 5 | 0 | Disabled | /sbin |
| shutdown | 6 | 0 | Disabled | /sbin |
| halt | 7 | 0 | Disabled | /sbin |
| mail | 8 | 12 | Disabled | /var/spool/mail |
| news | 9 | 13 | Disabled | /var/spool/news |

Figure 155. Select User window

Above you see a human readable form of the user information stored in the file /etc/passwd.

The information in Figure 155 is organized in columns by:

- **Username.** This is the unique name that a user types at the login prompt. It can also be called the login name, ID, user login, or user account.
- **UID.** This is the number the system uses to identify each user. Each user on a particular system has a unique UID.
- **GID.** This is the unique number assigned to a group. Every user has a default group. In TurboLinux the default GID is 100.
- **Password.** This does not contain the password but tells you the information about its state. The column is either:
    - Shadowed. It means it is using the shadow password file to store the password instead of /etc/passwd.
    - Disabled. The account is disabled, or is a service. Services are assigned a UID but no password, as they do not log in in the same way humans do.
- **Home Dir.** This is the user's home directory. It is the first place a user goes when logging in. It contains files and programs that are owned and used by that user.

In addition there are several choices for adding or configuring users that are given to you in the boxes along the bottom. They are:

- Configure. This allows you to change the characteristics that were set up when the ID was created.
- Add. Allows you to add users, which will be discussed later.
- Remove. Allows you to remove the user. You can optionally remove the home directory.
- Options. Allows you to configure options for the user such as file space quotas if they have been enabled.
- Done. Will allow you to quit and save unsaved information.
- Cancel. Will allow you to quit and not save any information.

![](img/4e6a76e57a4105be55d8a1cc0750b023_161_0.png)

Figure 156. User Options window

To add a user select the Add option at the bottom of the window. You will then see a window asking you to give the name of the new user, and specify the home directory for this user. We recommend you accept the default location of /home/<username>.

You will then come to the window Figure 156. The information that can be added for each user includes:

- UID
- GID
- Full Name
- Office
- Office Phone
- Home Dir
- Home Dir

The buttons at the bottom of the window allow you to modify the following:

- Passwords must be at least 4 characters long.
- Disk Quotas can be defined per users if you have file systems on this server that have quotas enabled.
- The default Shell, bash, will suffice for almost all users. On occasion, some users may prefer a different shell. You can set the user's default shell here.

Here is a brief description of the included shells:

- /bin/bash. This is the Bourne Again Shell, which is an extension to the Bourne Shell. This is the most popular shell for Linux.
- /bin/sh. This is the standard Bourne Shell that has been around almost the beginning of UNIX.
- /bin/ash. This is another version of the Bourne Shell.
- /bin/bash. This is the same as /bin/ash to which it is linked.
- /bin/ksh. This is the standard Korn Shell the is the most popular shell for UNIX administration.
- /bin/tcsh. This is a public domain extension of the C Shell.
- /bin/csh. This is the standard C Shell that was originated by the University of California at Berkeley.
- /bin/zsh. This is another extension of the Bourne Shell.

Your choice of shells is strictly a matter of preference, but generally UNIX admins prefer Bourne or Korn Shell programs, whereas programmers tend to prefer C Shell-based programs.

## 5.6 Administering file systems and the boot record

![](img/4e6a76e57a4105be55d8a1cc0750b023_163_0.png)

Figure 157. Select Function window

Running the command `turbofcfg` generates the menu you see Figure 157. From here the administrator can manage almost all issues that touch the DASD attached to this system. To view all the DASD attached to this system, select the Storage option. That will display a window similar to Figure 158.

![](img/4e6a76e57a4105be55d8a1cc0750b023_161.png)

Figure 158. Storage window

150 Linux System Administration and Backup for IBM @serverX and Netfinity

Running the command `turbofcfg` generates the menu you see Figure 157. From here the administrator can manage almost all issues that touch the DASD attached to this system. To view all the DASD attached to this system, select the Storage option. That will display a window similar to Figure 158.

## 5.6 Managing file systems

Below is a list of your configured filesystems:

| Device | Mount Point | Type | Permissions | FSCK |
|---|---|---|---|---|
| /dev/fd0 | /floppy | ext2 | RW | 0 |
| /dev/hda1 | | ext2 | RW | 1 |
| /dev/hda2 | /var | ext2 | RW | 2 |
| /dev/hda3 | /tmp | ext2 | RW | 2 |
| /dev/hda4 | /home | ext2 | RW | 1 |
| /dev/hda5 | /proc | ext2 | RW | 0 |
| /dev/hda6 | /cdrom | iso9660 | RW | 0 |
| /dev/hda7 | | ext2 | RW | 2 |
| /dev/hda8 | | ext2 | RW | 1 |
| /dev/hda9 | /swap | ext2 | RW | 0 |

Figure 159. Configure Filesystems window

Running the command `turbofcfg` generates the menu you see Figure 157. From here the administrator can manage almost all issues that touch the DASD attached to this system. To view all the DASD attached to this system, select the Storage option. That will display a window similar to Figure 158.

In addition to the columns of information, there are several options at the bottom of the window. We now address them:

- (Mount) toggle the status of file systems. With this option you can mount filesystems that are currently mounted, and unmount nonsensical filesystems.
- Check allows you to force FSCK to run now. You can only run FSCK against mounted filesystems.
- Edit allows you to change various attributes of the mount point. For example, the window below was generated by highlighting the first line in the table (the floppy drive) and choosing Edit. In the next few windows, we show how to change the default file system to MSDOS.

152 Linux System Administration and Backup for IBM @serverX and Netfinity

Chapter 5. TurboLinux basic system administration

- Permissions options. Whether the file system is readable and/or writable.
- FSCK options. These two numbers determine the system should be dumped if the system crashes (0 for no, 1 for yes), and the priority FSCK use when running (0 indicates the file system should not be checked, 1 indicates that FSCK should check this file system first, 2 indicates that FSCK should check all the file systems numbered 1 have been completed.

That example is given at step 3 on page 154 when we discuss the Edit option.

![](img/4e6a76e57a4105be55d8a1cc0750b023_165_0.png)

Figure 160. User Options window
