This shows that the file belongs to user bball and group users. To change the group ownership and grant access to other members of the group, use

```
```
# groups bball
bball : bball users
# chgrp users myfile
# ls -l myfile
-rw-rw-r-- 1 bball users 0 Nov 23 14:16 myfile
```
```

Now, other members of the users group can access the file. Along with the chgrp command, you can use the newgrp command, which is found in the /usr/bin directory. Although the chgrp command will change group ownership of one of your files or directories to a group you belong to (or if you're the root operator, any group), you can use newgrp to shift your current group membership:

```
```
# groups
bball users
# touch file1
# ls -l file1
-rw-rw-r-- 1 bball bball 0 Nov 23 14:53 file1
# newgrp users
# groups
users bball
# touch file2
# ls -l file2
-rw-rw-r-- 1 bball users 0 Nov 23 14:54 file2
# newgrp bball
```
```

This shows that the user bball originally belonged to the default group bball. This was verified by creating a file showing the current user and group ownership. Next, the user bball changed to the users group, created a file, and verified that the created file has the new group's access. Finally, the user bball changed back to the original group, bball.

![](bbox=[0.32, 0.84, 0.38, 0.9])

> > The newgrp command will launch a new shell, and you must use the shell's exit command to return to your original prompt. If you only need to run a single command as the member of a different group, use the sg command, which will not replace your shell.

As you can see, Linux offers you a great deal of flexibility in assigning file ownerships and permissions. By using different combinations of directory and file ownership and permissions, you can organize your system along lines of types of work, types of users, or types of files.