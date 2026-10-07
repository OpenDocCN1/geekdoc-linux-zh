# File Permissions

We talked about file permissions in Chapter 3 and Chapter 6, but this topic is worth revisiting in the context of security. As you remember from our discussion of the chmod command in Chapter 4, each file is assigned a permission string. This string determines the type of access granted to the file's owner, to members of the file's group, and to others in the outside world. The types of access that can be granted are read (r), write (w), and execute (x). Here is a sample permission string:

```
-rwxrxr-xr 1 owner group 240 May 1 11:00 file
```

Under Linux, each file is assigned an owner and a group. In this example, the owner is called owner, and the group is called group. Ownership is completely separate from group membership, which is to say that the owner does not belong to the file's group. Permission strings specify permission in the following order: owner, group, and others. Looking at the permission string, we see that the owner of file has read, write, and execute permissions for it. Members of the group group have read and execute permissions as well.

Under Hat Linux, when a user is created, a group of the same name is created with only the named user as a member. Red Hat calls these user private groups. Chapter 6 describes this practice.

To set appropriate access levels for a file or directory, you need to consider the use(s) that will be made of it. For example, if you plan to execute the  ls command on a directory, you need to assign that directory read permission. Obviously, a file that is to be viewed requires read access. Likewise, a file that is to be changed requires write access. A file that is to be run as an executable will, of course, need execute permission. When the file is a directory, however, these requirements might not be so obvious. Generally, any directory that you want to search or whose contents you want to list will need read access. Any directory contents are to be changed requires write access. If you wish to change your present directory to the target directory, the directory will have to allow you execute privileges. Table 7.1 lists some commands and the required file/directory permissions.