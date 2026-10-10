
# Part 1: The Linux Command Line

**TIP**
A common security practice is to look for instances where SUID and SGID are used in programs and try to remove those permissions due to the security risks they present.

## Using Access Control Lists

The basic Linux method of permissions has one drawback in that it’s somewhat limited. You can assign permissions for a file or directory only to a single group or user account. In a complex business environment with different groups of people needing different permissions to files and directories, that doesn’t work.

Linux developers have devised a more advanced method of file and directory security called an **_access control list_ (ACL)**. The ACL allows you to specify a list of multiple user or groups and the permissions that are assigned to them. Just like the basic security method, ACL permissions use the same read, write, and execute permission bits but can now be assigned to multiple users and groups.

To use the ACL feature in Linux, you use the **_setfacl_** and **_getfacl_** commands. The **_getfacl_** command allows you to view the ACLs assigned to a file or directory:

```
$ touch test
$ ls -l
total 0
-rw-r---- 1 rich rich 0 Apr 19 17:33 test
$ getfacl test
# file: test
# owner: rich
# group: rich
user::rw-
group::r--
other::---
```

If you’ve only assigned basic security permissions to the file, those still appear in the **_getfacl_** output, as shown in this example.

To assign permissions for additional users or groups, you use the **_setfacl_** command:

```
setfacl [options] rule filenames
```

The **_setfacl_** command allows you to modify the permissions assigned to a file or directory using the **_-m_** option, or remove specific permissions using the **_-x_** option. You define the **_rule_** with three formats:

```
u[ser]:uid:perms
g[roup]:gid:perms
o[ther]::perms
```

## Chapter 7: Understanding Linux File Permissions

To assign permissions for additional user accounts, use the user format; for additional groups, use the group format; and for others, use the other format. For the uid or gid values, you can use the numerical user ID or group ID, or the names. Here’s an example:

```
$ setfacl -m g:sales:rw test
$ ls -l
total 0
-rw-rw----+ 1 rich rich 0 Apr 19 17:33 test
```

This example adds read and write permissions for the sales group to the test file. Notice there’s no output from the setfacl command. When you list the file, only the standard owner, group, and other permissions are shown, but note that there’s a plus sign (+) added to the permissions list. This indicates that the file has additional ACLs applied to it. To view the additional ACLs, use the getfacl command again:

```
$ getfacl test
# file: test
# owner: rich
# group: rich
user::rw-
group::r--
group:sales:rw-
mask::rw-
other::---
```

The getfacl output now shows that there are permissions assigned to two groups. The default file group (rich) is assigned read permissions, but now the sales group has read and write permissions to the file. To remove the permissions, use the -x option:

```
$ setfacl -x g:sales test
$ getfacl test
# file: test
# owner: rich
# group: rich
user::rw-
group::r--
mask::r--
other::---
```

Linux also allows you to set a default ACL on a directory that is automatically inherited by any file created in the directory. This feature is called *inheritance*.

To create a default ACL on a directory, start the rule with d: followed by the normal rule definition. That looks like this:

```
$ sudo setfacl -m d:g:sales:rw /sales
```

This example assigns the read and write permissions to the sales group for the /sales directory. Now all files created in that folder will automatically be assigned read and write permissions for the sales group.

# Summary

This chapter discussed the command-line commands you need to know to manage the Linux security on your system. Linux uses a system of user IDs and group IDs to protect access to files, directories, and devices. Linux stores information about user accounts in the /etc/passwd file and information about groups in the /etc/group file. Each user is assigned a unique numeric user ID, along with a text login name to identify the user in the system. Groups are also assigned unique numerical group IDs, and text group names. A group can contain one or more users to allow shared access to system resources.

Several commands are available for managing user accounts and groups. The useradd command allows you to create new user accounts, and the groupadd command allows you to create new group accounts. To modify an existing user account, use the usermod command. Similarly, the groupmod command is used to modify group account information.

Linux uses a complicated system of bits to determine access permissions for files and directories. Each file contains three security levels of protection: the file’s owner, a default group that has access to the file, and a level for everyone else on the system. Each security level is defined by three access bits: read, write, and execute. The combination of three bits is often referred to by the symbols rwx; for read, write, and execute. If a permission is denied, its symbol is replaced with a dash (such as r-- for read-only permission).

The symbolic permissions are often referred to as octal values, with the three bits combined into one octal value and three octal values representing the three security levels. The umask command is used to set the default security settings for files and directories created on the system. The system administrator normally sets a default umask value in the /etc/profile file, but you can use the umask command to change your umask value at any time.

The chmod command is used to change security settings for files and directories. Only the file’s owner can change permissions for a file or directory. However, the root user can change the security settings for any file or directory on the system. The chown and chgrp commands can be used to change the default owner and group of the file.

The chapter also discussed how to use the set GID bit to create a shared directory. The SGID bit forces any new files or directories created in a directory to use the default group name of the parent directory, not that of the user who created them. This provides an easy way to share files between users on the system.

Finally, the chapter provided a primer on using the Linux access control list (ACL) feature to assign more detailed and advanced permissions to files and directories. The getfacl and setfacl commands provide access to this feature.

Now that you’re up to speed with file permissions, it’s time to take a closer look at how to work with the actual filesystem in Linux. The next chapter shows you how to create new partitions in Linux from the command line and then how to format the new partitions so that they can be used in the Linux virtual directory.

# Managing Filesystems

## CHAPTER 8

**IN THIS CHAPTER**

- Exploring Linux filesystems
- Working with filesystems
- Managing logical volumes

**W**hen you're working with your Linux system, one of the decisions you'll need to make is what filesystem to use for the storage devices. Most Linux distributions provide a default filesystem for you at installation time, and most beginning Linux users just use it without giving the topic another thought.

Although using the default filesystem choice isn't necessarily a bad thing, sometimes it helps to know the other options available to you. This chapter discusses the different filesystem options you have available in the Linux world and shows you how to create and manage them from the Linux command line.

## Exploring Linux Filesystems

Chapter 3, “Basic Bash Shell Commands,” discussed how Linux uses a *filesystem* to store files and folders on a storage device. The filesystem provides a way for Linux to bridge the gap between the ones and zeros stored in the hard drive and the files and folders you work with in your applications.

Linux supports several types of filesystems to manage files and folders. Each filesystem implements the virtual directory structure on storage devices using slightly different features. This section walks you through the strengths and weaknesses of common filesystems used in the Linux environment as well as some history regarding them.

### Exploring the Linux filesystem evolution

The original Linux system used a simple filesystem that mimicked the functionality of the UNIX filesystem. This section discusses its improvements through time.
