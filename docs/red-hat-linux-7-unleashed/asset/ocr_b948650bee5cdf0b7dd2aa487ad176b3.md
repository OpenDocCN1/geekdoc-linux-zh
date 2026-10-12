letter coding system, they are referred to as u for user, g for group, o for other, and a for all. The three basic types of permissions you can change are r for read, w for write, and x for execute. These three permissions can be changed by using the plus (+) and minus (\-) signs. For example, you would issue the following command to add read and execute to owner and group of the file test1:

```
chmod ug+rx test1
```

To remove the read and execute permissions from the user and group of the test1 file, you would change the plus (+) sign to a minus (\-) sign:

```
chmod ug-rx test1
```

This is referred to as making relative changes to the mode of the file.

When using the numeric coding system, you always have to give the absolute value of the permissions, regardless of their previous permissions. The numeric system is based on three sets of base 2 numbers—one set for each category of user, group, and other. The values are 4, 2, and 1, where 4 equals read, 2 equals write, and 1 equals execute. These values are added together to give the set of permissions for that category. With numeric coding, you always specify all three categories. Therefore, to give read, write, and execute permissions to the owner of the file test1, and no permissions to anyone else, you would use the value 700, like this:

```
chmod 700 test1
```

To make the same file readable and writable by the user, and readable by both the group and others, you would use the following mathematical logic. For the first set of permissions—the user—the value for readable is 4 and the value for writable is 2. The sum of these two is 6. The next set of permissions—the group—only gets readable, so that is 4. The setting for others, as for the group, is 4. Therefore, the command would be as follows:

```
chmod 644 test1
```

The format for the command, using either method, is the same. You issue the chmod command followed by the permissions, either absolute or relative, followed by the objects for which you want the mode changed:

```
chmod <permissions> <file>
```

# chown

This command is used to change the user ID (owner) associated with the permissions of the file or directory. The owner of the file (and, of course, root) has the authority to change the user associated with the file. The format for the command is simply this:

```
chown new user id file
```

![](bbox=[0.88, 0.7, 0.98, 1.0])