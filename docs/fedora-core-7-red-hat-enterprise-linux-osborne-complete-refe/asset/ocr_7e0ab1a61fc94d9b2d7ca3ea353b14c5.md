user changes the group name for **today** and **weekend** to the **forecast** group. The `ls -l` command then reflects the group change.

```
```
$ chgrp forecast today weekend
$ ls -l
-rw-rw-r-- 1 chris forecast 568 Feb 14 10:30 today
-rw-rw-r-- 1 chris forecast 308 Feb 17 12:40 weekend
```
```

You can combine the `chgrp` operation in the `chown` command by attaching a group to the new owner with a colon.

```
```
$ chown george:forecast tomorrow
-rw-rw-r-- 1 george forecast 568 Feb 14 10:30 tomorrow
```
```

# Setting Permissions: Permission Symbols

The symbolic method of setting permissions uses the characters **r**, **w**, and **x** for read, write, and execute, respectively. Any of these permissions can be added or removed. The symbol to add a permission is the plus sign, **+**. The symbol to remove a permission is the minus sign, **-**. In the next example, the `chmod` command adds the execute permission and removes the write permission for the **mydata** file for all categories. The read permission is not changed.

```
```
$ chmod +x-w mydata
```
```

Permission symbols also specify each user category. The owner, group, and others categories are represented by the **u**, **g**, and **o** characters, respectively. Notice the owner category is represented by a **u** and can be thought of as the user. The symbol for a category is placed before the plus minus sign preceding the read, write, and execute permissions. If no category symbol is used, all categories are assumed, and the permissions specified are set for the user, group, and others. In the next example, the first `chmod` command sets the permissions for the group to read and write. The second `chmod` command sets permissions for other users to read. Notice no spaces are between the permission specifications and the category. The permissions list is simply one long phrase, with no spaces.

```
```
$ chmod g+rw mydata
$ chmod o+r mydata
```
```

A user may remove permissions as well as add them. In the next example, the read permission is set for other users, but the write and execute permissions are removed:

```
```
$ chmod o+r-wx mydata
```
```

Another permission character exists, **a**, which represents all the categories. The **a** character is the default. In the next example, the two commands are equivalent. The read permission is explicitly set with the **a** character denoting all types of users: other, group, and user.

```
```
$ chmod a+r mydata
$ chmod +r mydata
```
```

One of the most common permission operations is setting a file's executable permission. This is often done in the case of shell program files. The executable permission indicates