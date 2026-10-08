# CHAPTER 5 | Filesystems, Volumes, and Encryption

Of course, if you want to allow users write access to their home directories, these directives can be changed. If you set up write access in your Samba configuration file, the following directives apply to the creation of files and directories, respectively:

```
create mask = 0700
directory mask = 0700
```

The create mask value sets up read and write permissions for the user owner of new files. The directory mask value sets up read, write, and execute permissions for the user owner of new directories.

While the [homes] share is visible only to the owner of a home directory, anyone can still connect to that home directory by default. You can prohibit such access with the following directive:

```
valid users = %S
```

Other directives associated with shared directories that you might consider or watch out for include those listed in Table 5-5.

Several Samba directives can be configured to point to users. These directives can also point to groups. For example, the following directive write access to the users who are members of the admin group:

```
write list = @admin
```

| TABLE 5-5 Samba directives related to shared directories |
| SAMBA DIRECTIVE | DESCRIPTION |
| acl check permissions | Checks ACL-based permissions from a Microsoft client |
| acl group control | Allows users of a group to change permissions and ACLs |
| admin users | Lists users with full administrative privileges |
| guest ok | Configures the share so no password is required; synonymous with public |
| hosts allow | Sets hostnames or IP addresses of allowed systems; opposite of hosts deny |
| locking | Supports a lock file to prevent simultaneous access to the same file |
| path | Sets a directory path for the share |
| printer admin | Lists users allowed to administer printers |
| write list | Lists users allowed read-write access to a share