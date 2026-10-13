The [homes] section is a special share service provided by Samba to allow Windows client users to access their UNIX home directories. When an SMB connection setup request is received, Samba first scans the set of specifically named shares. If a match is not found, it will then scan the passwd database attempting to locate a match for the client user name. If a user name match is found and the client has supplied the correct password, Samba grants access to a temporary [user name] share created by cloning the [homes] section definitions. If a path parameter has not been supplied, the user's home directory path is used as specified in the UNIX passwd database.

A sample [homes] definition is provided in Example 11.2. Take special note of the write access parameters used in the example [homes] definition. The use of write list = %S versus writable = yes eliminates the possibility that another user could gain read access to a home directory set with world read permission.

# Example 11.2 Sample [homes] Section Definition

```
[homes]
comment = User Home Directories
browseable = no
writable = no
write list = %S
```

[homes] user directory shares can be accessed by providing the user name as the share name or by specifying homes as the share name. In the latter case, the user name is derived from the requesting client setup request. This feature is useful when configuring a logon script to setup a common desktop environment on a multi-user workstation. Be aware that some Windows clients will not unmount the home directory share when a user logs out. You may want to force an unmount as part of the logout environment clean-up process:

```
C:\ NET USE H: \\<server name>\<user name>
```

```
C:\ NET USE H: \\<server name>\homes
```

Other [homes] section considerations include specifying an alternate user directory using the path parameter to separate UNIX user directories and Windows client user directories (Example 11.3). Also, note that even though the browseable parameter is disabled, individual users will still see their home directories listed as folders in a browse list.

# Example 11.3 [homes] Share with Alternate Directory Path

```
[homes]
comment = User Home Directories
browseable = no
writable = no
write list = %S
path = /home/samba/%u
```