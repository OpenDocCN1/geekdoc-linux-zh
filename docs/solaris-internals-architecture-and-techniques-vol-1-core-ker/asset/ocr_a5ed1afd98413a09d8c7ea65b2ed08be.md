To overcome this drawback, some operating systems use an access control list (ACL), where lists of users with different permissions can be assigned to a file. Solaris introduced the notion of access control lists in the B1 secure version, known as Trusted Solaris, in 1993. Trusted Solaris ACLs were later integrated with the commercial Solaris version in 1995 with Solaris 2.5.

Solaris ACLs allow the administrator to assign a list of Unix user IDs and groups to a file using the setfacl command and review the ACLs by using the getfacl command, as shown below.

```
# setfacl -m user:jon:rw- memtool.c
# getfacl memtool.c

# file: memtool.c
# owner: rmc
# group staff
user:
user:jon:rw- #effective:r-
group:r-- #effective:r-
mask:r--nother:--

# ls -l memtool.c -r--r--r--+ 1 rmc staff 638 Mar 30 11 memtool.c
```

For example, we can assign access to a file for a specific user using the setfacl command. Note that the Unix permissions on the file now contain a +, signifying that an access control list is assigned to this file.

Multiple users and groups can be assigned to a file, offering a flexible mechanism for assigning access rights. ACLs can be assigned to directories as well. Note that unlike some other operating systems, access control lists are not inherited from a parent, so a new directory created under a directory will not have an ACL assigned by default. Table 12-7 lists file system support for ACLs.

**Table 12-7** File System ACL Support

| File System | ACL Support? |
|--- |--- |
| Solaris 2.0-2.4 UFS | No |
| Solaris 2.5 UFS | Yes |
| VxFS | Yes |
| QFS | No |

# 12.3.5 File Systems Logging (Journaling)

Important criteria for commercial systems are reliability and availability, both of which may be compromised if the file system does not provide the required level of robustness. We have become familiar with the journaling to mean just one