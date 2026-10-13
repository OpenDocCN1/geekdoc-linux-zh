description is available from IBM at www.ibm.com/developerworks/aix/library/au-filesys_NFSv4ACL/index.html.

Frequently, the /home directory is taken from a shared NFS directory. In fact, NFS-based ACLs are more fine-grained than standard ACLs. This feature was introduced with NFS version 4, the standard for RHEL 6. To that end, the nfs4_getfacl command can display the ACLs associated with files on a shared directory. Based on the ACLs previously given, Figure 4-3 shows the output to the nfs4_getfacl command.

The output is in the following format:

```
type:flags:principal:permissions
```

where the settings are delineated by the colon. Briefly, the two types shown either allow (A) or deny (D) the noted principal (a user or group) the specified permissions. No flags are shown in Figure 4-3, which can provide relatively fine-grained control. The principal may be a regular user or group, in lowercase. It may also be a generic user such as the file OWNER, the GROUP that owns the file, or other users, as specified by EVERYONE. The permissions as shown in Table 4-4, are more fine-grained. The effect varies depending on whether the object is a file or a directory.

The configuration of NFS as a client is covered in Chapter 6, with other local and network filesystems. The configuration of an NFS server is an RHCE objective covered in Chapter 16.

# FIGURE 4-3

NFS version 4 ACLs

```
[michael@server1 ~]$ nfs4_getfacl /test/examprep/
A::OWNER@:rwatxTCy
A::michael@localdomain:xtcy
A::GROUP@:tcy
A::EVERYONE@:tcy
[michael@server1 ~]$ nfs4_getfacl /test/examprep/TheAnswers
D::OWNER@:x
A::OWNER@:rwatTCcy
A::michael@localdomain:rwaxtcy
A::GROUP@:rwatcy
A::EVERYONE@:tcy
[michael@server1 ~]$
```