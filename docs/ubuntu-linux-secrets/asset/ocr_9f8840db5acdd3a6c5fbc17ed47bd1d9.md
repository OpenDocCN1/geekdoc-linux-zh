# Deleting Groups

If you need to remove an existing group, just select it in the Group Settings dialog box and click the Delete button. Ubuntu will produce the warning message seen in Figure 17-10.

![](bbox=[0.22, 0.3, 0.62, 0.6])

Figure 17-10: Deleting a group.

When you delete a group, any files that are assigned to the group retain the group ID value. That just means the group ID isn't assigned a group name. When you list the files, they'll appear with the group ID number instead of a group name.

# User and Group Files

Ordinarily, it's a good idea to let the Ubuntu graphical utilities do all the hard work on the workstation, but user and group management is one of those areas where it helps to know what's happening under the hood. You may run into situations where you have only the command line available, and it helps to know how to manually add or modify a user account or group.

This section walks through the basics of the user and group system on the Ubuntu workstation.

# The Users File

Ubuntu uses a system called shadow passwords to keep the encrypted passwords for each user in a secure location. This system requires using two separate files to track user account information.

# The /etc/passwd File

The primary user account file is the /etc/passwd file. Despite what it says, that's not where user account passwords are stored. This file is set to be readable by every account on the system, because applications often need to know the users on the system.

A sample entry in the /etc/passwd file is

```
rblum:x:506:506:Rich Blum:/home/rich:/bin/bash
```