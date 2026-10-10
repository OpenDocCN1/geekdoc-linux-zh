# # id

**Purpose:** Display information about a user's identity.

**Usage syntax:** `id [OPTIONS] [USER]`

```
# id
uid=0 (root) gid=0 (root) groups=0 (root)
```

Displaying user and group information for the current user

The **id** command displays user and group information for the specified user. Executing **id** with no options displays the current user's information as displayed in the above example. The next example demonstrates using the **id** command to display information about a specific user.

```
# id nick
uid=1000 (nick) gid=1000 (nick) groups=4 (adm), 20 (dialout), 24 (cdrom), 46 (plugdev), 106 (lpadmin), 121 (admin), 122 (sambashare), 1000 (nick)
```

Displaying user and group information for a specific user

> > **Note**: Unix, Linux, and BSD systems assign a numerical UID (User ID) and GID (Group ID) for each user and group on the system. A user friendly name is also assigned to each UID and GID which is displayed in parenthesis next to each ID number. This information is stored in `/etc/passwd` for users and `/etc/group` for groups.

+   - **Common usage examples:**
+     - `id` | Display the current user's ID information
+     - `id [USER]` | Display user and group information for the specified user