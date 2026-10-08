# 450 getfacl

```
mask::perm
other::perm
default:user::uid::perm
default:user:gid::perm
default:group::perm
default:group:gid::perm
default:mask::perm
default:other::perm
```

When you specify multiple files on the command line, a blank line separates the ACLs
for each file.
The ACL entries are displayed in the order in which they are evaluated when an
access check is performed. The default ACL entries that may exist on a directory have no
off effect on access checks.
The first three lines display the file name, the file owner, and the file-owning group.
Note when you specify only the -d option and the file has no default ACL, only these
three lines are displayed.

The user entry without a user ID indicates the permissions that are granted to
owner of the file. One or more additional user entries indicate the permissions that are
to the specified users.
The group entry without a group ID indicates the permissions that are granted to
The owning group of the file. One or more additional group entries indicate the
permissions that are granted to the specified groups.

The mask entry indicates the file mask permissions. These are the maximum
permissions allowed to any user entries, except the file owner, and to any group entries,
including the owning group. These permissions restrict the permissions specified in
of entries.
The other entry indicates the permissions that are granted to others.
The default entries exist only for directories and indicate the default entries
that are added to a file created within the directory.
The uid is a login name or a user ID if there is no entry for the uid in the system
password file; /etc/passwd. The gid is a group name or a gid if there is no entry
for the gid in the system group file; /etc/group. The permission is a three-character string
composed of the letters representing the separate access r:(read,w
(write), x:(execute/search), or the placeholder character -. The permission is displayed in the
 order rwx. If permission is not granted by an ACL entry, the placeholder
character is used.
The file-owner permission bits represent the access of the owning user ACL.
The file-group class bits represent the most access that any additional user
entries, additional group entries, or the owning group may grant. The file
other-class permission bits represent the access that the other ACL has. If a user
invokes the chmod(1) command and the file group class permission bits, the
access granted by additional ACL entries may be restricted.
to indicate that the file-group permission bits restrict an ACL entry, getfacl
displays an additional Tab character, a pound sign (#), and the actual permissions
granted, following the entry.

> Note The output of getfacl is in the correct format for input to the
setfacl command. If the output of getfacl is redirected to a file, the file
can be used as input to setfacl. In this way, you can easily assign one file's
ACL to another file.