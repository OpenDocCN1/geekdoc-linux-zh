An example of use is:

```samba
veto oplock files = ./.SEM/
```

**vfs object** This parameter is a synonym for *vfs objects*.

**vfs objects (S)** Default: *No default*

Example: *vfs objects = extd.audit recycle*

This parameter specifies the backend names which are used for Samba VFS I/O operations. By default, normal disk I/O operations are used but these can be overloaded with one or more VFS objects.

**volume (S)** Default: *volume = the name of the share*

This allows you to override the volume label returned for a share. Useful for CDROMs with installation programs that insist on a particular volume label.

**wide links (S)** Default: *wide links = yes*

This parameter controls whether or not links in the UNIX file system may be followed by the server. Links that point to areas within the directory tree exported by the server are always allowed; this parameter controls access only to areas that are outside the directory tree being exported.

Note that setting this parameter can have a negative effect on your server performance due to the extra system calls that Samba has to do in order to perform the link checks.

**winbind cache time (G)** Default: *winbind cache time = 300*

This parameter specifies the number of seconds the winbindd(8) daemon will cache user and group information before querying a Windows NT server again.

> **NOTE**
> This does not apply to authentication requests, these are always evaluated in real time.

**winbind enum groups (G)** Default: *winbind enum groups = yes*