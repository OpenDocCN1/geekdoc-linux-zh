# # User Accounts

A user account in Debian consists of:

+   1. Username: A unique identifier for the user.
+   2. User ID (UID): A numeric identifier assigned to each user.
+   3. Primary Group ID (GID): The main group to which the user belongs.
+   4. Home Directory: The user's personal directory, typically /home/username.
+   5. Login Shell: The command interpreter assigned to the user.

# # Group Accounts

Groups are used to organize users and manage permissions collectively. Each group has:

+   1. Group Name: A unique identifier for the group.
+   2. Group ID (GID): A numeric identifier assigned to each group.
+   3. Member List: Users who belong to the group.

# # Important User and Group Files

+   1. /etc/passwd: Contains user account information.
+   2. /etc/shadow: Stores encrypted user passwords.
+   3. /etc/group: Defines groups and their members.
+   4. /etc/gshadow: Contains encrypted group passwords (rarely used).

# # Adding, Removing, and Modifying Users

# ## Adding Users

To add a new user, use the `adduser` command:

```
```bash
sudo adduser username
```
```