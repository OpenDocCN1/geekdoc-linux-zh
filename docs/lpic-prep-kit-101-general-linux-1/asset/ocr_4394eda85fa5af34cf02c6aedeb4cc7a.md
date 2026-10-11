Table 9.1 | Options That Can Be Used with the chown Command
Option | Action
-- | --
-c | Displays information on all changed files
-V | Displays information on all files whether or not the ownership change was successful
-f | Does not display error messages
-R | Applies changes recursively down the directory tree

# Changing the Group

Groups are merely a way to organize users. Because every file has a group associated with it and permissions can be applied to groups, groups are an excellent tool for managing access to files and directories. Groups and group management are covered in Chapter 7, “Users and Groups.”

You can change the group for a file using either the chown or chgrp command. You must be the owner or root to change a file’s group.

As the owner of a file, if you want to change a file from one group to another, you must be a member of the new group. Root, however, can change the group to any group, regardless of whether root is a member of that group.

Performing an ls -l on the file MyFile shows you the current owner and group, as in

```
-rw-rw-r-- 1 hadden user 370 Sep 5 14:42 MyFile
```

To use the chown command to change the owner and group, you must separate the owner and group names by a colon, as in the following:

```
chown martinez:wp MyFile
```

This will change the owner of the file MyFile to martinez, as well as change its group from user to wp. Now, when you perform an ls -l on MyFile you see

```
-rw-rw-r-- 1 martinez wp 370 Sep 5 14:42 MyFile
```

You could have changed only the group on MyFile by issuing the following command:

```
chown :wp MyFile
```

This would have changed the group to wp without changing the owner of the file. An ls -l command would now show

```
-rw-rw-r-- 1 hadden wp 370 Sep 5 14:42 MyFile
```