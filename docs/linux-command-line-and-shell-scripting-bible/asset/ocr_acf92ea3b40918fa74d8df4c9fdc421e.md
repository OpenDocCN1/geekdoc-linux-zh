# Understanding Linux File Permissions

# TABLE 6-4

| Parameter | Description |
| - | - |
| -d | Set the number of days since the password was last changed. |
| -E | Set the date the password will expire. |
| -I | Set the number of days of inactivity after the password expires to lock the account. |
| -m | Set the minimum number of days between password changes. |
| -W | Set the number of days before the password expires that a warning message appears. |

# The chage Command Parameters

# Using Linux Groups

User accounts are great for controlling security for individual users, but they aren't good at allowing groups of users to share resources. To accomplish this, the Linux system uses another security concept, called groups.

Group permissions allow multiple users to share a common set of permissions for an object on the system, such as a file, directory, or device (more on that later in the "Decoding File Permissions" section).

Linux distributions differ somewhat on how they handle default group memberships. Some Linux distributions create one group which contains all of the user accounts as members. You need to be careful if your Linux distribution does this, as your files may be readable by all other users on the system. Other distributions create a separate user account for each user, to provide a little security.

Each group has a unique GID, which, like UIDs, is a unique numerical value on the system. Along with the GID, each group has a group name. There are a few group utilities you can use to create and manage your own groups on the Linux system. This section discusses how group information is stored, and how to use the group utilities to create new groups and modify existing groups.

# The /etc/group file

Like user accounts, group information is stored in a file on the system. The /etc/group file contains information about each group used on the system. Here are a few examples from the /etc/group file on my Linux system:

```
root:x:0:root
bin:x:1:root,bin,daemon
```