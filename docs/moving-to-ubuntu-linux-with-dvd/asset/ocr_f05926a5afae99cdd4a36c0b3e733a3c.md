Each of these letters can be referenced by a number. They are r, w, x, and s. Their numerical representations are 4, 2, 1, and “it depends.” To understand all that, you need to do a little binary math.

Reading from right to left, think of the x as being in position 0. The w, then, is in position 1 and the r is in position 2. Here’s the way it works:

+   2 to the power of 0 equals 1 (x is 1)
+   2 to the power of 1 equals 2 (w is 2)
+   2 to the power of 2 equals 4 (r is 4)

To specify multiple permissions, you can add the numbers together. If you want to specify both read and execute permissions, simply add 4 and 1 and you get 5. For all permissions (rwx), use 7.

File permissions are referenced in groups of three rwx sections. The r stands for read, the w means write, and the x denotes that the file is executable.

Although these permissions are arranged in three groups of three rwx combinations, their meaning is the same in all cases. The difference has to do with who they represent rather than the permissions themselves. The first of these three represents the user, the second trio stands for the group permissions, and the third represents everybody that doesn’t fit into either of the first two categories.

The commands you use for changing these basic permissions are chmod, chown, and chgrp.

+   chmod  C**H**ange the M**O**De of a file (a.k.a. its permissions)
+   chown  C**H**ange the O**W**Ner of the file or directory
+   chgrp  C**H**ange the G**R**OuP of the file or directory

# ## User and Group Ownership

Let’s pretend you have a file called mail_test and you want to change its ownership from the root user to natika. Because root is the only user that can make that change, you need to prepend your command with sudo. This is very simple.

```
sudo chown natika mail_test
```