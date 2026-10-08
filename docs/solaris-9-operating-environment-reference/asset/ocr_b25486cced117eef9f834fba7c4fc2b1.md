# getfacl 449

# Attributes

See attributes(5) for descriptions of the following attributes:

| Attribute Type | Attribute Value |
| --- | --- |
| Availability | SUNWcsu |

# See Also

pathconf(2), confstr(3C), sysconf(3C), attributes(5), environ(5), largefile(5)

# getfacl — Display Discretionary File Information

# Synopsis

```
/usr/bin/getfacl [-ad] file...
```

# Description

Access Control Lists (ACLs) are extensions to standard UNIX file permissions. The ACL information is stored and associated with each file individually. You can determine if a file has an ACL with the getfacl command. For each argument that is a regular file, special file, or named pipe getfacl displays the owner, the group, and the ACL. For each directory argument getfacl displays the owner, the group, and the ACL and/or the default ACL. Only directories contain default ACLs.

You can execute getfacl on a file system that does not support ACLs. It reports the ACL based on the base permission bits.

If you specify no options, getfacl displays the file name, the owner, the group, and both the ACL and the default ACL.

# Options

+   -a Display the file name, the owner, the group, and the ACL of the file.
-d Display the file name, the owner, the group, and the default ACL of the file if it exists.

# Operands

+   - file The path name of a regular file, special file, or named pipe.

# Output

The format for ACL output is as follows.

```
# file: filename
# owner: uid
# group: gid
user::perm
user:uid:perm
group::perm
group:gid:perm
```