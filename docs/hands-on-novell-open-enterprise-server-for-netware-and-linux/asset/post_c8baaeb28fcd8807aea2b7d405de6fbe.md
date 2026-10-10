
15. The CA service is used to do which of the following?
- a. encrypt passwords
- b. authenticate users
- c. configure the LDAP server
- d. none of above

16. Which of the following can't be changed in the user account's Properties dialog box?
- a. default home directory
- b. shell
- c. group memberships
- d. default background

17. Settings for the graphics card and monitor can be changed during the ____________ installation step.
- a. network configuration
- b. service configuration
- c. installation settings
- d. hardware configuration

18. The name "Kicker" is also used for which of the following?
- a. KDE desktop
- b. KDE menu
- c. KDE Control Panel
- d. Linux boot loader

19. All virtual desktops share the same background and icons. True or False?

20. Which of the following is the main KDE file-management utility?
- a. YaST
- b. Konqueror
- c. Control Panel
- d. Kicker

## CASE PROJECTS

### Case Project 12-1: Selecting a Linux Server

Wiggins and Son Heating and Air Conditioning is planning to set up a network system based on a SUSE Linux server and has asked you to create specifications for the server. The manager wants to ensure a high level of protection from system and power failures and keep the total hardware cost under $5000. Write a brief report listing the minimum SUSE Linux requirements and recommending a system that you think will best meet the company's needs.

### Case Project 12-2: Preparing for Linux Installation

In this project, document the essential steps for installing SUSE Linux on the server you identified in Case Project 12-1.

## HANDS-ON PROJECTS

### Hands-on Project 12-1: Using Konqueror

To get started using the system, Wiggins and Son wants you to create the following directory structure on the new SUSE Linux server: a main directory called WHA and subdirectories called Shared, Accounting, and Marketing.

Use Konqueror to create this directory structure off the root of the file system. Copy a file from your local computer to the Shared directory, and have your instructor check the directory structure after you have completed it.

## CHAPTER 13

## MANAGING LINUX ENVIRONMENTS

After reading this chapter and completing the activities, you will be able to:
- Create and manage Linux users and groups
- Work with command-line utilities from a Linux shell
- Manage Linux applications with run levels and RedHat Package Manager
- Work with the Linux file system, including file system permissions, partitions, and logical volumes

In Chapter 12, you learned how to perform a basic installation of SUSE Linux, including disk partitioning and working with the YaST and KDE graphical environments. In this chapter, you learn how to integrate a Linux desktop system into your network environment by creating local Linux user accounts, setting up file system security, accessing network resources, and installing software applications. You also learn how to use the YaST utility to manage system configuration and the command-line interface to run common Linux commands.

## CREATING AND MANAGING LINUX USERS AND GROUPS

Because Linux is a multiuser system, you must log in with a valid user name and password before working with a Linux system. As you learned in Chapter 12, the root user has all rights to the Linux system; other user names can be given limited access permissions. If possible, you should avoid logging in with the root user account to reduce the risk of damaging the system or data accidentally. During the Linux installation, administrators can create additional standard user accounts for themselves and other users. As in NetWare, user accounts are often granted rights and permissions by being part of a group. In this section, you learn how to use the YaST utility and the useradd and groupadd commands to create and modify user and group accounts.

### Local Group Accounts

In Linux, there are two major types of groups: local and system. Network administrators use local groups to assign rights and permissions to users, and the operating system uses system groups to grant rights to access certain system resources. To view local or system groups, use the Set Filter button in the YaST utility. Figure 13-1 shows an example of using YaST to view the default system groups.

![](img/840007e8f98ea6653e5877e945c27dc6_539_0.png)

The root group is important because it can be used to grant all rights to the Linux system. Notice that the root user is a member of the root group. You can use the root group to create a backup administrator account by making another user account a member of the root group.

Although a number of system groups are created during Linux installation, only one local group named users is created (see Figure 13-2) to give members of this group basic permissions to the system. In SUSE Linux, when a user account is created, it's assigned to a primary or default local group. The system defaults to placing new users in the users group, but network administrators can select another local or system group as a new user's default group.

Linux administrators often create other groups to grant users rights to certain files and resources. If you plan to create a number of new users who will belong to a special default group, creating that group before creating the user accounts is easier because you can simply select that group as the default group for user account creation instead of changing the default group assignment for all user accounts later. In Activity 13-1, you use YaST to create a new local group and then make it the default group for new users.

![](img/840007e8f98ea6653e5877e945c27dc6_540_0.png)

Figure 13-2 The default SUSE Linux local group

### Local User Accounts

In addition to a user name and password, each Linux user account needs to be assigned a user ID (UID), a home directory, a default command shell, and password setting parameters. Because computers handle numbers more efficiently than alphabetic characters, all user accounts are assigned a UID number. The root user is assigned a UID of 0, and other user accounts are given randomly generated UIDs.

As in the NetWare and Windows environments, each user account in Linux should be given a home directory. When users log in, their default file system paths are directed to their home directories. During installation, a directory structure named /home is created in the root partition for the purpose of storing user home directories.

The Linux command-line interface (CLI) is referred to as the shell, which is actually a program that runs on the Linux kernel to provide a command-line environment for starting other programs. When you create a user account, that user is assigned a default command shell. Table 13-1 lists some common command shells that can be assigned to user accounts.

Table 13-1 Common Linux shells

| Shell Name | Program Name | Description |
| --- | --- | --- |
| Bourne shell | sh | The original UNIX shell, which has been replaced in Linux with the Bash shell. |
| Bourne Again (Bash) shell | bash | An enhanced and extended version of the shell created by the GNU project for use on many UNIX and Linux systems. Commonly referred to as the Bash shell instead of its full name. Bash is the default Linux shell. |
| C shell | csh | This shell, developed by Bill Joy in the 1970s, was the first to contain features such as history and tab completion. Because of its additional complexity, it's not as popular with users and developers as the Bash shell. |
| Korn shell | ksh | A proprietary (not freely available) shell written by David Korn. This revision of the Bash shell includes the interactive features of the C shell but maintains the Bash shell programming syntax. |

![](img/840007e8f98ea6653e5877e945c27dc6_540_1.png)

Because the Bash shell is the default in Linux, it's used for command lines in this book's activities.

Local user accounts are stored in two files named *shadow* and *passwd* in the */etc* directory structure. The */etc/shadow* file is used to store encrypted case-sensitive passwords, and the */etc/passwd* file contains the user name, UID, home directory path, and default shell. All users can read the *passwd* file, but for security purposes, only the root user can read the *shadow* file. Figure 13–3 shows sample lines for the EKenton user account in the *passwd* and *shadow* files.

### Passwd file entry for Eric Kenton

```
ekenton::x:1001:100:Network administrator:/home/ekenton:/bin/bash
```

- User name
- Password (“x” means the password is in the shadow file)
- UID
- Primary group ID
- Comment
- Home directory path
- Default shell

### Shadow file entry for Eric Kenton:

```
ekenton:r5ECmuZ.ht0qo:13061:0:99999:7:-1::
```

- User name
- Encrypted password
- Date of last change (# of days from 1/1/1970)
- Date after which password can be changed
- Date after which password must be changed
- How many days before password expiration user should be warned
- Number of days that password is valid after expiration (grace period)
- Day on which account is locked

Note: The information under each file entry describes the fields from left to right.

### Figure 13–3 *passwd* and *shadow* file entries

In the sample shadow file entry, the *Date of last change* field indicates when the password was last changed and is expressed using the number of days from January 1, 1970 (a date prior to Linux being released). The *date after which the password can be changed* and *date after which the password must be changed* are used to set password change restrictions. The “-1” entry for the day on which the account is locked means that the account hasn’t been locked.

### Activity 13-1: Creating User and Group Accounts in YaST

**Time Required:** 10 minutes

**Objective:** Use the YaST utility to create local user and group accounts.

**Requirements:** Completion of Activity 12-1, a local Linux user name created during installation, and access to the root user password

**Description:** Now that a SUSE Linux system has been installed in the Engineering Department, Eric Kenton wants you to create some local user and group accounts so that Engineering and Manufacturing users can share the Linux system. In this activity, you use YaST to create local group accounts and then add Engineering and Manufacturing user accounts.

1. If necessary, log in to your SUSE Linux server with the user name and password you created for yourself during the Activity 12-1 installation.
2. Start the YaST utility by clicking the Start application icon (a red “N” in a green circle) in the Control Panel, clicking System, and then clicking the YaST option.
