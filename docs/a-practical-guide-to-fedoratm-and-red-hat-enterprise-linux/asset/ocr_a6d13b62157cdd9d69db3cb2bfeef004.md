When Zach checks his access permissions on info, he finds he has both read and execute access to the directory. Now `ls -l` displays the contents of the **info** directory, but he still cannot read **financial**. (This restriction is an issue of file permissions, not directory permissions.) Finally, Zach tries to create a file named **newfile** using `touch`. If Max were to give him write permission to the info directory, Zach would be able to create new files in it:

```
```
$ ls -l /home/max/info
drwx --r-x. 2 max pubs 4096 08-21 09:31 /home/max/info
$ ls -l /home/max/info
total 8
-rw--------. 1 max pubs 34 08-21 09:31 financial
-rw-r---. 1 max pubs 30 08-21 09:32 notes
$ cat /home/max/info/financial
cat: financial: Permission denied
$ touch /home/max/info/newfile
touch: cannot touch '/home/max/info/newfile': Permission denied
```
```

# ## ACLS: ACCESS CONTROL LISTS

ACLs (Access Control Lists) provide finer-grained control over which users can access specific directories and files than do traditional Linux permissions (page 191). Using ACLs you can specify the ways in which each of several users can access a directory or file. Because ACLs can reduce performance, do not enable them on filesystems that hold system files, where the traditional Linux permissions are sufficient. Also, be careful when moving, copying, or archiving files: Not all utilities preserve ACLs. In addition, you cannot copy ACLs to filesystems that do not support ACLs.

An ACL comprises a set of rules. A rule specifies how a specific user or group can access the file that the ACL is associated with. There are two kinds of rules: **access rules** and **default rules**. (The documentation refers to *access ACLs* and *default ACLs*, even though there is only one type of ACL: There is one type of list [ACL] and there are two types of rules that an ACL can contain.)

An access rule specifies access information for a single file or directory. A default ACL pertains to a directory only; it specifies default access information (an ACL) for any file in the directory that is not given an explicit ACL.

# ### Most utilities do not preserve ACLs

> caution
> When used with the -p (preserve) or -a (archive) option, `cp` preserves ACLs when it copies files. The `mv` utility also preserves ACLs. When you use `cp` with the -p or -a option and it is not able to copy ACLs, and in the case where `mv` is unable to preserve ACLs, the utility performs the operation and issues an error message:
> 
> ```
> $ mv report /tmp
> mv: preserving permissions for '/tmp/report': Operation not supported
> ```
> Other utilities, such as `tar`, `cpio`, and `dump`, do not support ACLs. You can use `cp` with the -a option to copy directory hierarchies, including ACLs.

You can never copy ACLs to a filesystem that does not support ACLs or to a filesystem that does not have ACL support turned on.