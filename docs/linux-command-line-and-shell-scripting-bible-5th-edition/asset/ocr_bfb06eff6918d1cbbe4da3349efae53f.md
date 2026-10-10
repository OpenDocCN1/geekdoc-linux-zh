on a set date, without your having to remember to delete them! Expired accounts are similar to locked accounts. The account still exists, but the user can't log in with it.

# ## Using Linux Groups

User accounts are great for controlling security for individual users, but they aren't so good at allowing groups of users to share resources. To accomplish this, the Linux system uses another security concept, called *groups*.

Group permissions allow multiple users to share a common set of permissions for an object on the system, such as a file, directory, or device (more on that later in the “Decoding File Permissions” section).

Linux distributions differ somewhat on how they handle default group memberships. Some Linux distributions create just one group that contains all the user accounts as members. You need to be careful if your Linux distribution does this, because your files may be readable by all other users on the system. Other distributions create a separate user account for each user to provide a little more security.

Each group has a unique GID, which, like UIDs, is a unique numerical value on the system. Along with the GID, each group has a unique group name. There are a few group utilities you can use to create and manage your own groups on the Linux system. This section discusses how group information is stored and how to use the group utilities to create new groups and modify existing groups.

# ## The /etc/group file

Just like user accounts, group information is stored in a file on the system. The /etc/group file contains information about each group used on the system. Here are a few examples from a *typical* /etc/group file on a Linux system:

```
```text
root:x:0:root
bin:x:1:root,bin,daemondaemon:x:2:root,bin,daemondaemonsys:x:3:root,bin,adminadm:x:4:root,adm,daemonrich:x:500:mama:x:501:katie:x:502:jessica:x:503:mysql:x:27:test:x:504
```
```

Like UIDs, GIDs are assigned using a special format. Groups used for system accounts are assigned GIDs below 500, and user groups are assigned GIDs starting at 500. The /etc/group file uses four fields:

+   - The group name
+   - The group password