using touch. If Alex were to give her write permission to the info directory, Jenny would be able to create new files in it:

```
$ ls -ld /home/alex/info
drwx--r-x  2 alex pubs 512 Aug 21 09:31 /home/alex/info
$ ls -l /home/alex/info
total 8
-rw------- 1 alex pubs 34 Aug 21 09:31 financial
-rw-r--r-- 1 alex pubs 30 Aug 21 09:32 notes
$ cat /home/alex/info/financial
cat: financial: Permission denied
$ touch /home/alex/info/newfile
touch: cannot touch '/home/alex/info/newfile': Permission denied
```

# ACLs: ACCESS CONTROL LISTS

Access Control Lists (ACLs) provide finer-grained control over which users can access specific directories and files than do traditional Linux permissions (page 202). Using ACLs you can specify the ways in which each of several users can access a directory or file. Because ACLs can reduce performance, do not enable them on file systems that hold system files, where the traditional Linux permissions are sufficient. Also be careful when moving, copying, or archiving files: Not all utilities preserve ACLs. In addition, you cannot copy ACLs to file systems that do not support ACLs.

# Most utilities do not preserve ACLs

When used with the -p (preserve) or -a (archive) option, cp preserves ACLs when it copies files. Another utility that is supplied with Fedora/RHEL that preserves ACLs is mv. When you use cp with the -p or -a option and if it is able to copy ACLs, and in the case where mv is unable to preserve ACLs, the utility performs the operation and issues an error message:

```
$ mv report /tmp
mv: preserving permissions for '/tmp/report': Operation not supported
```

Other utilities, such as tar, cpio, and dump, do not support ACLs. You can use cp with the -a option to copy directory hierarchies, including ACLs.

You can never copy ACLs to a file system that does not support ACLs or to a file system that does not have ACL support turned on.

An ACL comprises a set of rules. A rule specifies how a specific user or group can access the file that the ACL is associated with. There are two kinds of rules: access rules and default rules. (The documentation refers to access ACLs and default ACLs, even though there is only one type of ACL: there is one type of list [ACL] and there are two types of rules that an ACL can contain.)

An access rule specifies access information for a single file or directory. A default ACL pertains to a directory only; it specifies default access information (an ACL) for any file in the directory that is not given an explicit ACL.