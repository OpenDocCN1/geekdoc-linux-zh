Many users prefer to use numeric codes, based on octal (base 8) values, to represent permissions. Here's what these values mean:

+   - 4 indicates read permission.
+   - 2 indicates write permission.
+   - 1 indicates execute permission.

In octal notation, the previous example file has a permission setting of 664 (read + write or 4 + 2, read + write or 4 + 2, read-only or 4). Although you can use either form of permissions notation, octal is easy to use quickly after you visualize and understand how permissions are numbered.

> NOTE
> In Linux, you can create groups to assign a number of users access to common directories and files, based on permissions. You might assign everyone in accounting to a group named accounting, for example, and allow that group access to accounts payable files while disallowing access by other departments. Defined groups are maintained by the root operator, but you can use the newgrp command to temporarily join other groups to access files (as long as the root operator has added you to the other groups). You can also allow or deny other groups' access to your files by modifying the group permissions of your files.

# Directory Permissions

Directories are also files under Linux. For example, again use the ls command to show permissions like this:

```
$ mkdir foo
$ ls -ld foo
drwxrwxr-x  2 andrew  andrew  4096 Jan 23 12:37 foo
```

In this example, the mkdir command is used to create a directory. The ls command and its -ld option is used to show the permissions and other information about the directory (not its contents). Here you can see that the directory has permission values of 775 (read + write + execute or 4 + 2 + 1, read + write + execute or 4 + 2 + 1, and read + execute or 4 + 1).

This shows that the owner and group members can read and write to the directory and, because of execute permission, also list the directory's contents. All other users can only list the directory contents. Note that directories require execute permission for anyone to be able to view their contents.

You should also notice that the ls command's output shows a leading d in the permissions field. This letter specifies that this file is a directory; normal files have a blank field