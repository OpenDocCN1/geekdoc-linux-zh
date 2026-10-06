192 Chapter 4 • Managing Files

mkdir, rmdir supports few options, the most important of which handle these tasks:

Ignore Failures on Non-empty Directories Normally, if a directory contains files or other directories, rmdir doesn't delete it and returns an error message. With the --ignore-fail-on-non-empty option, rmdir still doesn't delete the directory, but it doesn't return an error message.

Delete Tree The -p or --parents option allows rmdir to delete an directory tree. For instance, typing rmdir -p one/two/three deletes one/two/three, then one/two, and finally, provided no other files or directories are present.

![](bbox=[0.137, 0.323, 0.203, 0.368])

When you're deleting an empty directory tree filled with files, you should use rm -R rather than rmdir. This is because rm -R deletes files within the specified directory by rmdir doesn't, so rmdir can't do the job.

# # Managing File Ownership

Security is an important topic that cuts across many types of commands and Linux subsystems. In the case of files, security is built on file ownership and file permissions. These two topics are closely intertwined; ownership is meaningless without permissions to use it, and permissions rely on the existence of ownership.

Ownership is two-tiered: Each file has an individual owner and a group with which it's associated (sometimes called the group owner, or simply the file's group). Each group can contain an arbitrary number of users, as described in Chapter 7, "Administering the System." The two types of ownership enable you to provide three tiers of permissions to control access to files: by the file's owner, by file's group, and to all other users. The commands to manage these two types of ownership are similar, but they are not identical.

# # Assessing File Ownership

You can learn about ownership of a file with the ls -l long listing, which was described earlier. In particular, command's -l option produces a long listing, which includes both ownership and permission information:

```
$ ls -l
total 1141
-rw-r--r-- 1 rodsmith users 219648 Mar 8 13:06 4425ch02.doc
-rw-r--r-- 1 rodsmith users 942590 Mar 6 23:31 f0201.tif
```