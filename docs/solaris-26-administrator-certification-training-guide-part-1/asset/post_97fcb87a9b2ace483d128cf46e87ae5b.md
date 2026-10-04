
## Displaying Directory Size Information

By using the df command, you displayed file system disk use. You can use the du command to display the disk use of a directory and all of its subdirectories in 512-byte blocks.

The du command shows you the disk use of each subdirectory. To get a list of subdirectories in a file system, cd to the pathname associated with that file system and run the following pipeline:

```
$ du | sort -r -n
```

This pipeline, which uses the reverse and numeric options of the sort command, pinpoints large directories. Use ls -l to examine the size (in bytes) and modification times of files within each directory. Old files or text files over 100KB often warrant storage offline.

## Controlling User Disk Space Use

Quotas enable system administrators to control the size of UFS file systems by limiting the amount of disk space individual users can acquire. Quotas are especially useful on the file systems where user home directories reside. After the quotas are in place, they can be changed to adjust the amount of disk space or number of inodes users can consume. Additionally, quotas can be added or removed as system needs change. In addition, quota status can be monitored. Quota commands enable administrators to display information about quotas on a file system or to search for users who have exceeded their quotas.

After you have set up and turned on disk and inode quotas, you can check for users who exceed their quotas. You can also check quota information for entire file systems by using the following commands:

| Command | Description |
|---|---|
| quota | Displays the quotas and disk use within a file system for individual users on which quotas have been activated. |
| repquota | Displays the quotas and disk use for all users on one or more file systems. |

You won’t see quotas in use much today, as the cost of disk space continues to fall. In most cases, the system administrator simply watches disk space to identify users who might be using more than their fair share. As we saw in this section, you can easily do this by using the du command. On a large system with many users, disk quotas can be an effective way to control disk space use.

This chapter described disk file systems and how they are managed. The system administrator will spend a great deal of time managing and fine-tuning file systems to improve system efficiency.

## CHAPTER

## 4

## System Security

The following are the test objectives for this chapter:

- Understanding the superuser account and its importance to system administration
- Understanding the format of the /etc/passwd, /etc/shadow, and /etc/group files and their importance to system security
- Changing ownership and access permissions on files and directories
- Displaying and changing default permissions (umask)
- Setting access control lists (ACLs) on files
- Monitoring system and user activity
- Modifying system defaults to control and monitor superuser access to the system
- Monitoring and restricting access to the root account
- Understanding how the setuid and setgid permissions relate to system security
- Understanding how the sticky permission protects files and directories

![](img/85737305a4c9aeecbcadd9986d604c02_89_0.png)

Keeping the system's information secure is one of the primary tasks for the system administrator. System security involves protecting data against loss due to a disaster or system failure. In addition, it is the system administrator's responsibility to protect systems from the threat of an unauthorized intruder and to protect data on the system from unauthorized users. Some of the worst disasters I've seen have come from authorized personnel—even system administrators—destroying data unintentionally. Therefore, the system administrator is presented with two levels of security: protecting data from accidental loss and securing the system against intrusion or unauthorized access.

The first scenario, protecting data from accidental loss, is easy to achieve with a full system backup scheme you run regularly. Regular backups provide protection in the event of a disaster. If a user accidentally destroys data, the hardware malfunctions, or a computer program simply corrupts data, the system administrator can restore files from the backup media.

The second form of security, securing the system against intrusion or unauthorized access, is more complex. This chapter cannot cover every security hole or threat, but it does discuss UNIX security fundamentals. Protection against intruders involves

- Physical security—Limiting physical access to the computer equipment
- Access to data—Limiting user access via passwords and permissions
- Network security—Protecting against access through phone lines, serial lines, or the network
- Superuser access—Reserving superuser access for system administration use only

## Physical Security

Physical security is simple: Lock the door. Limit the people who have physical access to the computer equipment to prevent theft or vandalism. In addition, limit access to the system console. Anyone who has access to the console ultimately has access to the data. If the computer contains sensitive data, keep it locked in a controlled environment with clean power and adequate protection against fire, lightning, flood, or other building disasters. Restrict access to protect against tampering with the system and its backups. Anyone with access to the backup media could steal it and access the data. Furthermore, if a system is logged in and left unattended, anyone who can use that system can gain access to the operating system and the network. Make sure your users log out or "lock" their screens before walking away. In sum, you need to be aware of your users' computer surroundings and you need to physically protect them from unauthorized access.

## Controlling System Access

Controlling access to systems involves using passwords and appropriate file permissions. To control access, all logins must have passwords, and the passwords must be changed frequently. Password aging is a system parameter set by the system administrator requiring users to change their passwords after a specific number of days. Password aging enables you to force users to change their passwords periodically or to prevent users from changing a password before a specified interval. Set an expiration date for a password to prevent an intruder from gaining undetected access to the system through an old and inactive account. For a high level of security, you should require users to change their passwords every six weeks. Once every three months is adequate for lower levels of security. Change system administration logins (such as root and sys) monthly, or whenever a person who knows the root password leaves the company or is reassigned.

Several files that control default system access are stored in the /etc/default directory. These files limit access to specific systems on a network. Table 4-1 summarizes the files in the /etc/default directory.

**Table 4-1 Files in /etc/default Directory**

| File | Description |
|---|---|
| /etc/default/login | Controls system login policies, including root access. The default is to limit root access to the console. |
| /etc/default/passwd | Controls default policy on password aging. |
| /etc/default/su | Specifies where attempts to su to root are logged and where these log files are located. The file also specifies whether attempts to su to root are displayed on a named device (such as a system console). |

You can set default values in the /etc/default/passwd file to control user passwords. See Table 4-2 for the list of options that can be controlled through the /etc/default/passwd file.

**Table 4-2 Flags in /etc/default/passwd**

| Flag | Description |
|---|---|
| MAXWEEKS | Maximum time period password is valid |
| MINWEEKS | Minimum time period before the password can be changed |
| PASSLENGTH | Minimum length of password, in characters |
| WARNWEEKS | Time period until warning of password's ensuing expiration date |

The system administrator’s job is to ensure that all users have secure passwords. Improper passwords can be broken by a system cracker and could put the entire system at risk.
