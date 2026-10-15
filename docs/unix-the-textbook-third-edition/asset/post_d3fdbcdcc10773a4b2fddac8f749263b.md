
The account is now set to expire October 15, 2022. Notice the entry made to the /etc/shadow file:

```
smsarwar:$5$WVZPYaFo$EWDwt4h/NVxegGOjNI0jA99G/U.6aQTlVdA0c.GGin3:15593::::::15593:
```

The last field for the smsarwar entry in the /etc/shadow file is 15593. This is an absolute date expressed as the number of days since the UNIX epoch (January 1, 1970). When this number is reached, the login is expired.

## 23.3.3.6 Deleting User Accounts

You can use the userdel command, similar to PC-BSD rmuser, to delete a user's login account from the system. You can specify options to save or remove the user's home directory. The syntax for the userdel command is as follows.

```
userdel [-r] [-S repository] <login-name>
```

The option -r removes the user's home directory from the local file system. If this option is not specified, only the login is removed; the home directory remains intact.

Make sure you know where the user's home directory is located before removing it. Some users have / as their home directory, and removing their home directory would remove important system files.

The following example removes the login account for smsarwar but does not remove the home directory:

```
# userdel smsarwar
```

## 23.3.3.7 Adding Group Accounts

You use the groupadd command to add new group accounts on the local system. This command adds an entry to the /etc/group file. The syntax for the groupadd command is as follows.

```
groupadd [-g gid [-o]] [-S repository] [-U user1[,user2..] ] group
```

Table 23.5 describes the groupadd command options.

The following example adds to the system a new group named acct with a GID of 1000:

```
# groupadd -g 1000 acct
```

## 23.3.3.8 Assigning a GID

If the -g option is not used to specify a GID, the GID defaults to the next available number above the highest number currently assigned. For example, if GIDs 100, 110, and 200 are already assigned to group names, the next GID that is automatically assigned is 201.

## TABLE 23.5 groupadd Command Options

| Option | Description |
| --- | --- |
| -g <gid> | Assigns the GID <gid> for the new group |
| -o | Allows the GID to be duplicated |
| -s | Specifies which name service repository will be updated |
| -u | Adds a list of users to a group |

## 23.3.3.9 Modifying Group Accounts

You use the groupmod command to modify the definitions of a specified group. The syntax for the groupmod command is as follows.

```
groupmod [-S [files | ldap]] [-U user1[,user2]] [-g gid [-o]] [-n name] group
```

Table 23.6 describes the groupmod command options.

The following example changes the engrg group GID from 200 to 2000:

```
# groupmod -g 2000 engrg
```

Any files that had the group ownership of engrg are now without a group name. A long listing would show a group ownership of 200 on these files, the previous GID for the engrg group. The group 200 no longer exists on the system, so only the GID is displayed in a long listing.

## 23.3.3.10 Deleting Group Accounts

You use the groupdel command to delete a group account from the local system. The syntax for the groupdel command is as follows.

```
groupdel [-S repository] <group-name>
```

The -S option allows the name service to be specified. The valid repositories that can be specified are files and ldap. When the repository is not specified, groupdel reads the file nsswitch.conf.

## TABLE 23.6 groupmod Command Options

| Option | Description |
| --- | --- |
| -g <gid> | Assigns the new GID <gid> for the group. |
| -o | Allows the GID to be duplicated. |
| -n <name> | Specifies a new name for the group. |
| -S | Valid repositories are files and ldap. The repository specifies the name service to be updated |
| -U | Updates the list of users for the group as follows: + adds, - removes, null replaces. |

The following example deletes the group named acct from the local system:

```
# groupdel acct
```

## EXERCISE 23.8

You have an air-gapped Solaris computer in a room. You want only certain users in a defined group named proj to be able to access files in a directory named proj1 in your account on the file system of that computer. Use the text-based commands shown previously to add those certain users, and yourself, to the group proj. Create the proj1 directory. Then, set the permission bits appropriately on your home directory, the proj1 directory, and any files put in that directory, so that only those certain users can read, write and execute the files in it. The room is open to the public, but to login to the computer, each individual user has to use her own password.

## 23.4 ADDING A HARD DISK TO THE SYSTEM

A common task done by a UNIX system administrator is to add various hardware components any significant time after the system has been installed and configured. To help the administrator of a UNIX system with that task, the following sections will detail:

- Some preliminary considerations that need to be made, such as the availability of software device drivers for the new hardware to be added
- How the hardware will be recognized, configured and deployed on the system
- Identification of possible paths to replacement and upgrading of existing hardware

In this section, we will illustrate how to add disk drives for use with the ZFS file system, and for other file system types as well. ZFS is described completely in Chapter 24. The additions will be done for SATA hard disks installed internally, and USB removable media such as external, enclosure-mounted hard drives.

Generally, when you add a SATA hard disk inside the computer case some significant time after you have installed the operating system on the computer, you will want to format it to ZFS. But when you add an external USB medium, such as a thumb drive or hard disk, it will already be formatted to FAT32 (in the case of most popular commercially available USB thumb drives), or to some other format depending on the hard disk media. You will format either kind of media to ZFS, as shown in Chapter 24.

If all you want to use a FAT32-formatted USB thumb drive for is to transfer files (such as text files, C program code, LibreOffice documents, etc.), to and from the computer, then the automatic mounting (in Solaris) and semiautomatic mounting (in PC-BSD) of USB thumb drives will help you to accomplish this. In both systems, unmounting of USB thumb drives is done manually. In Solaris, right-click on the USB thumb drive icon on the Gnome desktop, and make the choice Unmount. In PC-BSD, use the Mount Tray icon, and make the Unmount choice for the USB thumb drive.
