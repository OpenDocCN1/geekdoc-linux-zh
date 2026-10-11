To change a user's password, use the `passwd` command:

```
sudo passwd username
```

To lock or unlock a user account:

```
# Lock
sudo passwd -l username

# Unlock
sudo passwd -u username
```

# ## User Permissions and Groups

Debian, like other Unix-like systems, uses a permission system based on users and groups to control access to files and directories.

# ### File Permissions

Each file and directory has three sets of permissions:

+   1. Owner permissions
+   2. Group permissions
+   3. Others permissions

Each set can have read (r), write (w), and execute (x) permissions.

To view permissions, use the `ls -l` command: