# Part 1: The Linux Command Line

**TIP**
A common security practice is to look for instances where SUID and SGID are used in programs and try to remove those permissions due to the security risks they present.

# ## Using Access Control Lists

The basic Linux method of permissions has one drawback in that it’s somewhat limited. You can assign permissions for a file or directory only to a single group or user account. In a complex business environment with different groups of people needing different permissions to files and directories, that doesn’t work.

Linux developers have devised a more advanced method of file and directory security called an **_access control list_ (ACL)**. The ACL allows you to specify a list of multiple user or groups and the permissions that are assigned to them. Just like the basic security method, ACL permissions use the same read, write, and execute permission bits but can now be assigned to multiple users and groups.

To use the ACL feature in Linux, you use the **_setfacl_** and **_getfacl_** commands. The **_getfacl_** command allows you to view the ACLs assigned to a file or directory:

```
```
$ touch test
$ ls -l
total 0
-rw-r---- 1 rich rich 0 Apr 19 17:33 test
$ getfacl test
# file: test
# owner: rich
# group: rich
user::rw-
group::r--
other::---
$```

```

If you’ve only assigned basic security permissions to the file, those still appear in the **_getfacl_** output, as shown in this example.

To assign permissions for additional users or groups, you use the **_setfacl_** command:

```
```
setfacl [options] rule filenames```

```

The **_setfacl_** command allows you to modify the permissions assigned to a file or directory using the **_-m_** option, or remove specific permissions using the **_-x_** option. You define the **_rule_** with three formats:

```
```
u[ser]:uid:perms
g[roup]:gid:perms
o[ther]::perms```

```