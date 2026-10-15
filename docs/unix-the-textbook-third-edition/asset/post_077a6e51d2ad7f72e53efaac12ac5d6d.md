
```
# chmod A=everyone@:read_data:allow file.0
```

A- removes an ACL entry.
To universally remove all nontrivial ACL entries for a file, use this operator and specify the file name without listing each entry to be removed. Use the following command syntax to restore a trivial ACL to the file.

```
# chmod A- filename
```

After you issue the command, only the entries for owner@, group@, and everyone@ that comprise a trivial ACL remain.

For modifying existing ACLs: Using the operators without an index has a different effect from using them with an index. For example, chmod A= replaces an entire ACL, while chmod A3= replaces only the existing entry that has index number 3.

Permissions and inheritance flags are represented by unique letters listed in Table 24.2 and Table 24.4.

When you set ZFS ACLs, you can either use the letters that correspond to those permissions (compact mode) or type the permissions in full (verbose mode).

In the following example, both commands grant read and execute permissions to user bob on file.1:

```
# chmod A+user:bob:rx:allow file.0
# chmod A+user:bob:read_data/execute:allow file.0
```

To grant user bob inheritable read, write, and execute permissions for the newly created d.2 and its files, you can use either one of the following commands:

```
# chmod A+user:bob:rwX:fd:allow d.2
# chmod A+user:bob:read_data/write_data/execute:file_inherit/dir_inherit: allow d.2
```

## 24.5.2.1.1 Displaying ACL Information

With the ls command, you can display ACL information in one of two formats: the -v option displays the permissions in full or verbose form; the -V option generates compact output by using letters that represent the permissions and flags.

The following examples show how the same ACL information is displayed in both verbose and compact format:

```
# ls -v file.0
-rw-r--r-- 1 root root 206695 Jul 20 14:27 file.0
0:owner@:read_data/write_data/append_data/read_attributes
/write_xattr/read_xattr/write_attributes/read_acl/write_acl
/write_owner/synchronize:allow
1:group@:read_data/read_attributes/read_xattr/read_acl
/synchronize:allow
```

```
2:everyone@:read_data/append_data/read_xattr/read_acl
/synchronize:allow

# ls -V file.0
-rw-r--r-- 1 root root 206695 Jul 20 14:27 file.0
owner@:rw-p--aARWcCos:------:allow
group@:r---a--a-R-c--s:------:allow
everyone@:r---a--a-R-c--s:------:allow
```

For an explanation of the permissions for each user category, see Table 24.2.

## 24.5.2.2 Modifying ACLs on ZFS Files

This section provides several sample commands for setting and displaying ACLs. We encourage you to do the in-chapter exercises at the end of the following sections to familiarize yourself with these basic Solaris NFSv4 ACL methods. You must run the following examples as superuser, unless otherwise specified.

In the following example, read_set permissions are given to user bob on a newly created file named file.1.

```
root@solaris_11_3:~# touch file.1
root@solaris_11_3:~# chmod A+user:bob:read_set:allow file.1
root@solaris_11_3:~# ls -V file.1
-rw-r--r--+ 1 root root 0 Nov 4 11:58 file.1
user:bob:r-----a--R-c--:------:allow
owner@:rw-p--aARWcCos:------:allow
group@:r-----a--R-c--s:------:allow
everyone@:r-----a--R-c--s:------:allow
```

The next example gives user mansoor read and execute permissions on file.1.

```
root@solaris_11_3:~# chmod A+user:mansoor:rx:allow file.1
root@solaris_11_3:~# ls -V file.1
-rw-r--r--+ 1 root root 0 Nov 4 11:58 file.1
user:mansoor:r-x----------:------:allow
user:bob:r-----a--R-c--:------:allow
owner@:rw-p--aARWcCos:------:allow
group@:r-----a--R-c--s:------:allow
everyone@:r-----a--R-c--s:------:allow
```

In the next example, group@ permissions are changed to read and write for file.1.

```
root@solaris_11_3:~# chmod A3=group@:read_data/write_data:allow file.1
root@solaris_11_3:~# ls -V file.1
-rw-rw-r--+ 1 root root 0 Nov 4 11:58 file.1
user:mansoor:r-x----------:------:allow
user:bob:r-----a--R-c--:------:allow
owner@:rw-p--aARWCos:------:allow
group@:rw------:------:allow
everyone@:r-----a-R-c-s:------:allow
```

In the following example, read_data/execute permissions are added for the user mansoor on the test.dir directory.

```
root@solaris_11_3:~# mkdir test.dir
root@solaris_11_3:~# chmod A0+user:mansoor:rx:allow test.dir
root@solaris_11_3:~# ls -dV test.dir
drwxr-xr-x+ 2 root root 2 Nov 4 12:07 test.dir
    user:mansoor:r-x------:------:allow
    owner@:rwxp-DAARWCos:------:allow
    group@:r-x---a-R-c-s:------:allow
    everyone@:r-x---a-R-c-s:------:allow
```

In the following example, access permissions are removed for user mansoor.

```
root@solaris_11_3:~# chmod A0- test.dir
root@solaris_11_3:~# ls -dV test.dir
drwxr-xr-x 2 root root 2 Nov 4 12:07 test.dir
    owner@:rwxp-DAARWCos:------:allow
    group@:r-x---a-R-c-s:------:allow
    everyone@:r-x---a-R-c-s:------:allow
```

## 24.5.2.3 ACL Interaction with Permission Bits

In ZFS files, the UNIX permission bits correspond to the ACL entries, but are stored in a special cache. When you change a file's permission bits, the file's ACL is updated accordingly. Similarly, modifying a file's ACLs causes changes in the permission bits.

For more information about permission bits, see the man page for chmod.

It would be advisable at this point to review the setting of UNIX permission bits in octal format, presented in Chapter 5, Sections 4 and 5.

The following examples show the relationship between a file or directory's ACLs and the permission bits, and illustrate how permission changes in one affect the other and vice versa.

The first example begins with the following ACL for file.2, whose permission bits are set to 644.

```
root@solaris_11_3:~# touch file.2
root@solaris_11_3:~# ls -V file.2
-rw-r--r-- 1 root root 0 Nov 4 12:09 file.2
    owner@:rw-p--aARWCos:------:allow
    group@:r-----a-R-c-s:------:allow
    everyone@:r-----a-R-c-s:------:allow
```

The following chmod command removes the ACL entry for everyone@ on file.2. The read permission bits for everyone@ are also removed and are changed to 640.
