
# setfacl 1259

```
group::perms
```

Group owner permissions.

```
other::perms
```

Permission for users other than the file owner or members of file group

```
mask::perms
```

The ACL mask specifying the maximum permissions permitted for users (other than the owner) and groups. The mask is a quick way to change permissions on all users and groups.

```
user::uid::perms
```

Permissions for a specific user. For uid, use either a username or a numeric ID.

```
group::gid::perms
```

Permissions for a specific group. For gid, use either a group name or a numeric GID.

```
default::user::uid::perms
```

Default file owner permissions.

```
default::group::perms
```

Default group owner permissions.

```
default::other::perms
```

Default permissions for users other than the file owner or members of the file group owner.

```
default::mask::perms
```

Default ACL mask.

```
default::user::uid::perms
```

Permissions for a specific user. For uid, use either a username or a numeric ID.

```
default::group::gid::perms
```

Default permissions for a specific group. For gid, use either a group name or a numeric ID.

The -d option, acl-entries is one or more comma-separated ACL entries without permissions, selected from the following Options list. Note that the entries for file owner, owning group, file group class, and others cannot be deleted.

# 1260

# setfac

# Options

- -s acl-entries

Set the ACL for a file. Remove all old ACL entries, and replace with the newly specified ACL. You can specify the entries in any order. They are rarely sorted by the command before being applied to the file.

Required entries:

- * Exactly one user entry specified for the owner of the file.
- * Exactly one group entry for the owning group of the file.
- * Exactly one other entry specified.

If there are additional user and group entries:

- * Exactly one mask entry specified for the file group class of the file.
- * Must not be duplicate user entries with the same uid
- * Must not be duplicate group entries with the same gid

If file is a directory:

- * Exactly one default:user entry for the owner of the file.
- * Exactly one default:group entry for the owning group of the file.
- * Exactly one default:mask entry for the file group class of the file.
- * Exactly one default:other entry.

You can specify additional default:user entries and additional default:group entries, but there cannot be duplicate additional default:user entries with the same uid duplicate duplicate group entries with the same gid. The entries need not be in any specific order. They are sorted by the command before being applied to the file.

- -m acl-entries

Add one or more new ACL entries to the file, and/or modify one or more existing ACL entries on the file. If an entry already exists for the user gid, replace the current permissions with the specified permissions. If an entry does not exist for the specified user gid, create it.

The first time you use the -m option to modify a default ACL, you must specify a complete default ACL (user, group, other, mask, and any additional entries).

- -d acl-entries

Delete one or more entries from the file. For the file owner, the owning group, and others from the ACL. Note that deleting an entry does not necessarily have the same effect as removing all permissions from the entry.

- -f acl-file

Set the ACL for a file, using the ACL entries contained in the file named acl-file. The same constraints on specified entries hold as with the -s option. The entries are not required to be in any specific order in the file.

![](img/185d23104c385dfb6a62d64cc96b8997_1289_0.png)

# setfacl

You can use the # character in an acl-file to indicate a comment.
Starting with the #, all characters until the end of the line are ignored.
Note that if the acl-file has been created as the output of the getfacl(1) command, any effective permissions that follow a # are ignored.

Recalculate the permissions for the group class entry, that is, the mask entry. Ignore the permissions specified in the group class entry, and replace them with the maximum permissions needed to grant access in any additional user, owning group, and additional group entries in the ACL. Leave the permissions in the additional user, owning group, and additional group entries unchanged.

- -r

# Examples

The following example lists the permissions on file foo. It adds one ACL entry to file foo, using ray read permission option and lists the permissions again. The + at the end of the permission list from the ls -1 command shows that an ACL exists for the file. Then, the example uses the getfacl command to list the ACL information for the file.

```
castle$ ls -1 foo
-rw-r--r-- 1 winsor staff      0 Apr 2 14:23 foo
castle$ setfacl -m user:ray:r-- foo
caste$ ls -1 foo
-rw-r--r-- 1 winsor staff      0 Apr 2 14:23 foo
castle$ getfacl foo
```

```
# file: foo
# owner: winsor
# group: staff
user::rw-
user:ray:r--           #effective:r--
group:r--              #effective:r--
mask:r--
other:r--
castele%
```

The following example replaces the entire ACL for the file foo, adding an entry for user ray read/write access, for the file owner allowing all access, an entry for the group allowing read only access, an entry for the group class allowing read/write, and an entry for others disregarding all access.

```
castle$ setfacl -s user:ray:rw-,user::rw,group:r--,mask:rw-,other:---
caste$ getfacl foo
```

```
# file: foo
# owner: winsor
# group: staff
user::rw-
user:ray:rw--           #effective:rw--
group:r--              #effective:r--
mask:r--
other:w--ncastele%
```

# 1262

Note — Following this command, the file permission bits are set to
rwx

Even though the file-owning group has only read permission, the maximum permissions available to all user ACL entries are read and write because the mask entry specifies these. The following example sets the same ACL on bar as:

```
castle% getfacl foo | setfacl -f -
castle% bar
```

```
# file: foo
# owner: winsor
# group: staff
user::rw-
user:ray:rw--           #effective:rw--
group:r--              #effective:r--
mask:r--
other-----castle::
```

```
#effective:rw-
#effective:r--
```

# Files

/etc/passwd Password file.
/etc/group Group file.

# Attributes

See attributes(5) for descriptions of the following attributes:

| Attribute Type | Attribute Value |
| Availability | SUMicu |

# See Also

chmod(1), getfacl(1), umask(1), aclcheck(3), aclsort(3), group(4),
passwd(4), attributes(5)

# setpgrp — Set Process Group ID

# Synopsis

```
/bin/setpgrp command [arg...]
```

# Description

Use the setgrp command, new in the Solaris 9 Environment, to set the
process ID. If the current process is not already a session leader, the setpgrp
command sets the process group ID and session ID to the current process and does an
exec() of command and its argument(s) if any.

# settime 1263

# Operands

+   command The name of a command to be invoked.
- arg An option or argument to command.

# Exit Status

+   1 Error executing the setpgrp command or during exec() of command.
Otherwise, the exit status is that of command.

# Attributes

See attributes(5) for descriptions of the following attributes:

| Attribute Type | Attribute Value |
| Availability | SUMcsu |

# See Also

exec(2), setpgrp(2), attributes(5)

# settime — Change File Access and Modification Times

# Synopsis

/usr/bin/settime [-f ref-file] file...

# Description

See touch(1).

# sftp — Secure File Transfer Program

# Synopsis

```
/bin/sftp [-vc] [-o ssh_option] [hostname | user@hostname]
```

# Description

Use the sftp command, new in the Solaris 9 Operating Environment, as an interactive
file transfer program with a user interface similar to ftp(1). sftp uses the ssh command
to create a secure connection to the server.
sftp implements the SSH File Transfer Protocol as defined in IETF draft-ietf-secch-slexer. There is no relationship between the protocol used by sftp and the FTP protocol (RFC9959) provided by ftp(1).

# Options

+   -C Enable compression with the -C option in ssh(1).
