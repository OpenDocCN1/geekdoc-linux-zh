+   i ACL type, allow or deny
+   j Command argument, a filename or directory name specification

# Format of ls -V output for the preceding files command

```
%ls -V filename
traditional permissions header
    user:bob:rw-------:-------:allow filename
    owner@ ----------default------------------
    group@ ----------default------------------
    everyone@ ----------default------------------
```

Use the following sample entry as a reference to understand the elements that comprise an ACL entry. These elements apply to both trivial and nontrivial ACLs.

```
0:user:mansoor:read_data/write_data:file_inherit:allow
```

Index: A number at the beginning of the entry, such as the number zero (0) in the example. The index identifies a specific entry and distinguishes the entry from others in the ACL. The index appears in the long format output of ACL entries given by the ls -V command.

ACL entry type: The user category. In trivial ACLs, only entries for owner@, group@, and everyone@ are set. In nontrivial ACLs, user:username and group:groupname are added. In the example, the entry type is user:mansoor.

Access privileges: Permissions that are granted or denied to the entry type. In the example, user mansoor's permissions are read_data and write_data.

Inheritance flags: An optional list of ACL flags that control how permissions are propagated downward in a directory structure. In the sample entry, file_inherit is also granted to user mansoor.

Permission control type: Determines whether the permissions in an entry are allowed or denied. In the example, the permissions for mansoor are allowed.

Table 24.1 describes each ACL entry type.
Table 24.2 describes ACL access privileges.

# TABLE 24.1 ACL Entry Types

| ACL Entry Type | Description |
|---|---|
| owner@ | Specifies the access granted to the owner of the object |
| group@ | Specifies the access granted to the owning group of the object |
| everyone@ | Specifies the access granted to any user or group that does not match any other ACL entry |
| user | With a user name, specifies the access granted to an additional user of the object |
| group | With a group name, specifies the access granted to an additional group of the object |