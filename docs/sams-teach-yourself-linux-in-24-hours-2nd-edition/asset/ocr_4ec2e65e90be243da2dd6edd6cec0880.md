This shows that the user, bball, belongs to the group users. As the root operator, you belong to the group root, for example:

```
# groups
root
```

To find out who belongs to a group, look at the /etc/group file, or use the name of a user:

```
# groups cloobie
cloobie : users
```

This shows that cloobie belongs to at least one group, called users. To assign one of your files to the users group, and give cloobie access, you can use the chown command's syntax of user:group:

```
# chown :users myfile
# ls -l myfile
-rw-r--r-- 1 bball users 0 Dec 26 15:19 myfile
```

You might think that to assign specific ownership, you can use the following:

```
# chown cloobie:users myfile
chown: myfile: Operation not permitted
```

What happened? This shows why Linux has groups. You can assign access of one of your files to a group, but unless you're the root operator, you cannot assign one of your files to appear to have been either created by or owned by another user. Make sure you're logged in as the root operator, and use

```
# chown cloobie:cloobie myfile
# ls -l myfile
-rw-rw-r-- 1 cloobie cloobie 0 Dec 26 15:19 myfile
```

As you can see, even though the file myfile was created by the user bball, as the sysadmin, you can assign ownership to any users and any group. If you just want to change the group ownership of a file or directory, you can use the chgrp command, and if you want to change your users or your own group, you can use the newgrp command.

# Changing Groups and Ownerships with the chgrp and newgrp Commands

The chgrp (change group) command, found in the /bin directory, is used only to change group ownerships. In this regard, it is not as flexible as the chown command, which can do both. The chgrp command accepts a group name or group ID (GID), for example:

```
# ls -l myfile
-rw-r--r-- 1 bball users 0 Dec 26 15:26 myfile
```