```
security mask = <default=create mask>
```

```
directory security mask = <default=directory mask>
```

The next level of file and directory permission parameters allows you to force the setting of permission bits through bit-wise OR'ing with the results of the first level parameters. This ensures that certain owner, group and world permission bits will always be applied when a file or directory is created. Second-level parameters include force create mode (DOS), force directory mode (DOS), force security mode (NT), and force directory security mode (NT). Refer to the smb.conf (5) man page for additional information.

```
force create mode = <default=000>
```

```
force directory mode = <default=000>
```

```
force security mode = <default=force create mode>
```

```
force directory security mode = <default=force directory mode>
```

In some instances you may want to force the assignment of a particular effective UNIX user or group to be used when operating on objects in the share. This is useful when multiple users are sharing access to a file share. By specifying a UNIX user name and group name as values to the force user and force group parameters, you can ensure that all file operations on the service will be performed using the named user and group for permissions checking and assignment:

```
force user = <user name>
```

```
force group = <group name>
```

As of Samba 2.0.5, the force group parameter allows a "+" character to be added as a prefix to the group name value. What this means is that a connecting user only operates under the specified effective group if it is already listed as a member of that group in the /etc/groups file (Example 11.7). All other users will operate under their own default primary UNIX groups.

# Example 11.7 2.0.5 Force Group Enhancement

```
force group = +sys
```

Power users that require full administrative privileges for a share are designated with the admin users parameter. This basically gives these users root privileges when operating on files and directories within the share.

```
admin users = <user list>
```

# Hiding Files & Directories