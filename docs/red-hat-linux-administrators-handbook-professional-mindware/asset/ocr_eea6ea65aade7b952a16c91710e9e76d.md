Each type of permission is represented with a single character (in paren-theses). To create a permission string, you need to specify the following:

+   ■ Who it affects. Your choices are u (user), g (group), o (others), or a (all).
+   ■ The type of permission that needs to be set. Your choices are r (read), w (write), x (execute), s (set-UID or set-GID), or t (sticky bit).
+   ■ The action type. Indicate whether you're setting the permission or removing it. When setting the permissions, you need to specify + to specify an addition, and - to specify a removal.

For example, to allow the file owner read-access to the file, you need to specify a permission string such as u+r. To allow everyone to read and execute a file, you need a permission string such as a+rx. Similarly, to make a file set-UID, you need u+s; to set it as set-GID, you need g+s.

# Changing file/directory permission modes using chmod

The chmod utility allows you to change permission modes and hence is called chmod. You can use either the octal or the string method with this nifty utility. For example,

```
chmod 755 *.pl
```

changes permissions for files ending with extension .pl. Each of the PL files is set as read, write, and execute (7 = 4 [read] + 2 [write] + 1 [execute]) by the owner. The files are also set to be readable and executable (5 = 4 [read] + 1 [execute]) by the group and others.

You can accomplish the same result by using the string method as follows:

```
chmod a+rx,u+w *.pl
```

Here a+rx is used to allow read (r) and execute (x) permissions for all (a), and u+w is used to allow the file owner (u) to write (w) to the file. Note that when multiple access strings need to be used, each pair of strings needs to be separated by a comma. Also, note that no space is allowed between the permission strings.