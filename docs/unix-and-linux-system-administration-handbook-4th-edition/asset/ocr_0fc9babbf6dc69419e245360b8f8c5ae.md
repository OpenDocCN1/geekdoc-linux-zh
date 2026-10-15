POSIX ACLs are a mostly straightforward extension of the standard 9-bit UNIX permission model. Read, write, and execute permission are the only capabilities that the ACL system deals with. Embellishments such as the setuid and sticky bits are handled exclusively through the traditional mode bits.

ACLs allow the rwx bits to be set independently for any combination of users and groups. Table 6.8 shows what the individual entries in an ACL can look like.

# Table 6.8  Entries that can appear in an access control list

| Format | Example | Sets permissions for |
|---|---|---|
| `user::perms` | `user::rw-` | The file’s owner |
| `user:username:perms` | `user:trent:rw-` | A specific user |
| `group::perms` | `group::r-x` | The group that owns the file |
| `group:groupname:perms` | `group:staff:rw-` | A specific group |
| `other::perms` | `other::---` | All others |
| `mask::perms` | `mask::rwx` | All but owner and otherᵃ |

ᵃ. Masks are somewhat tricky and are explained later in this section.

Users and groups can be identified by name or by UID/GID. The exact number of entries that an ACL can contain varies with the filesystem implementation and ranges from a low of 25 with XFS to a virtually unlimited number with ReiserFS and JFS. The ext* filesystems allow 32 entries, which is probably a reasonable limit for manageability in any case.

# Interaction between traditional modes and ACLs

Files with ACLs retain their original mode bits, but consistency is automatically enforced and the two sets of permissions can never conflict. The following example (which uses the Linux command syntax) demonstrates that the ACL entries update automatically in response to changes made with old-style **chmod**:

```
```text
$ touch /tmp/example
$ ls -l /tmp/example
-rw-rw-r--  1 garth  garth  0 Jun 14 15:57 /tmp/example
$ getfacl /tmp/example
getfacl: Removing leading '/' from absolute path names
# file: tmp/example
# owner: garth
# group: garth
user::rw-
group::rw-
other::r--
$ chmod 640 /tmp/example
$ getfacl --omit-header /tmp/example
user::rw-
group::r--
other::---
```
```