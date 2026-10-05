
Each line in the /etc/group file contains information about one group. Each group entry is divided into four colon-separated fields. Here is an example of a line from /etc/group:

```
group01:x::10000:user01,user02,user03
```

- Group Name for this group (group01).
- Obsolete group password field. This field should always be x.
- The GID for the group (10000).
- A list of users who are members of this group as a supplementary group (user01, user02, user03). Primary (or default) and supplementary groups are discussed later in this section.

# Primary Groups and Supplementary Groups

Every user has exactly one primary group. For local users, this is the group that will own new files created by the user in the /etc/passwd file. By default, this is the group ID given by GID.

Normally, when you create a new user, a new group with the same name as that user is created. That group is the primary group for the new user, and that user is the only member of this User Private Group. It turns out that this helps management of file permissions, which will be discussed later in this course.

Users may also have supplementary groups. Membership in supplementary groups is granted access to files based on whether any of their groups have access. It doesn't matter if the group or groups that have access are primary or supplementary for the user.

For example, if the user user01 has a primary group user01 and supplementary groups wheel and webadmin, then user can read files readable by any of these three groups.

The id command can also be used to find out about group membership for a user.

```
[user03@host ~]$id
uid=1003(user03) gid=1003(user03) groups=1003(user03),10(wheel),10000(group01)
context=unconfined:u:unconfined:r:unconfined:t:s0:s0:c0:1023
```

In the preceding example, user03 has the group user03 as their primary group (gid). The groups item lists all groups for this user, other than the primary group user03, the user has wheel group and group01 as supplementary groups.

REFERENCES
id(!), passwd(5), and group(5) man pages
info libc (GNU C Library Reference Manual)
Section 30: Users and groups
(Note that the glibc-dev package must be installed for this info node to be available.)

# QUIZ

# DESCRIBING USER AND GROUP CONCEPTS

Choose the correct answer to the following questions:

- 1. Which item represents a number that identifies the user at the most fundamental level?
a primary user
b UID
c GID
d username

- 2. Which item represents the program that provides the user's command-line prompt?
a primary shell
b home directory
c login shell
d command name

- 3. Which item or file represents the location of the local group information?
a home directory
b /etc/passwd
c /etc/GID
d /etc/group

- 4. Which item or file represents the location of the user's personal files?
a home directory
b login shell
c /etc/passwd
d /etc/group

- 5. Which item represents a number that identifies the group at the most fundamental level?
a primary group
b UID
c GID
d groupid

- 6. Which item or file represents the location of the local user account information?
a. home directory
b /etc/passwd
c /etc/UID
d /etc/group

- 7. What is the fourth field of the /etc/passwd file?
a. home directory
b UID
c login shell
d primary group

# DESCRIBING USER AND GROUP CONCEPTS

Choose the correct answer to the following questions:

- 1. Which item represents a number that identifies the user at the most fundamental level?
   a. primary user
   b. UID
   c. GID
   d. username

- 2. Which item represents the program that provides the user's command-line prompt?
   a. primary shell
   b. home directory
   c. login shell
   d. command name

- 3. Which item or file represents the location of the local group information?
   a. home directory
   b. /etc/passwd
   c. /etc/group
   d. /etc/group

- 4. Which item or file represents the location of the user's personal files?
   a. home directory
   b. login shell
   c. /etc/passwd
   d. /etc/group

- 5. Which item represents a number that identifies the group at the most fundamental level?
   a. primary group
   b. UID
   c. GID
   d. groupid

- 6. Which item or file represents the location of the local user account information?
  a. home directory
  b. /etc/passwd
  c. /etc/UID
  d. /etc/group

- 7. What is the fourth field of the /etc/passwd file?
  a. home directory
  b. UID
  c. login shell
  d. primary group

# GAINING SUPERUSER ACCESS

# OBJECTIVES

After completing this section, you will be able to switch to the superuser account to manage a Linux system, and grant other users superuser access through the sudo command.

# THE SUPERUSER

Most operating systems have some sort of superuser, a user that has all power over the system. In Red Hat Linux this is the root user. This user has the power to override normal privileges on the file system, and is used to manage and administer the system. To perform tasks such as installing or removing software and to manage system files and directories, users must escalate their privileges to the root user.

The root user only among normal users can control removable devices, but there are a few exceptions. For example, normal users can control removable devices, such as USB devices. Thus, normal users can add and remove files and otherwise manage a removable device, but only root can manage "fixed" drives by default.

This unlimited privilege, however, comes with responsibility. The root user has unlimited power to damage the system: remove files and directories, remove user accounts, add back doors, and so.

# SWITCHING USERS

The su command allows users to switch to a different user. When you use su from a regular user, you will be prompted for the password of the account to which you want to switch.

```
[user01@host ~]$ su user02
Password:
[user02@host ~]
```

The command su starts a non-login shell, while su - starts a login shell. The main distinction between the two commands is that su - sets up the environment as if it were a new login as user, while su just starts a shell as user.

In most cases, administrators should run su - to get a shell with the target user environment. For more information, see the bash(1) man page.

The su is most frequently used to get a command-line interface (shell prompt) when running as another user, typically root. However, with the -c option, it can be used like Windows runas to run an arbitrary program as another user. Run info to view more details.

# RUNNING COMMANDS WITH SUDO

In some cases, the root user's account may not have a valid password at all for security reasons. In this case, users cannot log in to the system as root directly without a password, and cannot su to get an interactive shell. One tool that can be used to get root access in this case is sudo.

Unlike su, sudo normally requires users to enter their own password for authentication, not the password of the user account they are trying to access. That is, users who sudo to run commands as root do not need to know the root password. Instead, they use their own passwords to authenticate access.

Additionally, sudo can be configured to allow specific users to run any command as some other user, or only some commands as that.

For example, when sudo is configured to allow the user01 to run the command usermod as root, user01 could run the following command to lock or unlock a user account:

```
[user01@host ~]$ sudo usermod -l user02
[sudo] password for user01:
[user01@host ~]$
```...
```

If a user tries to run a command as another user, the sudo configuration does not permit it, the command will be blocked, the attempt will be logged, and by default an email will be sent to the root user.
