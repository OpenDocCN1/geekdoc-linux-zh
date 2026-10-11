# Primary Group

+   - Every user is associated with exactly one primary group

+   - The primary group for a user is defined in the 4th field of the file /etc/passwd as listed by the GID field

+   - The primary group is the group owner of any new file that is created by a user

+   - The primary group number by default for a user is the same number as the user. The primary group is also known as the User Private Group (UPG) as it has only the user as a member of it

# Supplementary Group

+   - A user can be a part of zero or more supplementary groups

+   - Supplementary groups exist so that a user is not restricted to one group, and resources can be allocated to users based on their groups

# The Superuser

This section is about the superuser of a Linux system commonly known as the root user.

# The Root User

Every operating system has one user that is known as the superuser with all access and rights to the operating system. If you have used a Windows operating system before, you may have heard about the superuser known as the administrator. Similarly, in Linux operating systems, the superuser is known as the **root user**. The root user has complete privilege to do anything in the Linux system and is usually used to manage the system. The root user can only perform tasks that modify the operating system for everyone such as installing or uninstalling software, managing files and directories, etc.

A root user can only manage additional devices attached to an operating system. There are certain exceptions, such as USB drives that can be managed by a regular user as well. A regular user can add or remove files