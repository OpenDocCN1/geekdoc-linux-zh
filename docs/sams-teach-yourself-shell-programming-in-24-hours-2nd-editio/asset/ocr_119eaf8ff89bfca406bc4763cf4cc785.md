column of the output of ps. If more than one process has the requested name, this function displays each process ID.

Readers who are using Linux or BSD systems have to change this function in order for it to run properly. The value of the variable PSOPTS should be set to -auxw instead of -ef on these systems. In Chapter 23, you will see how to incorporate these changes into the function so that it runs without modification under any version of UNIX.

The following command illustrates the use of getPID:

```
getPID httpd
```

The output of this command is a list of process IDs, similar to the following:

+   - 330
+   - 331
+   - 332
+   - 333
+   - 334

# Getting a User's Numeric User ID

Some shell scripts need to determine whether a user has sufficient permissions to execute commands. For example, a startup script might need to run as root (UID 0) to modify system files correctly.

A user's ID can be checked by using the id command. The default for this command is to output information about the current user:

```
$ id
uid=500(ranga) gid=100(users) groups=100(users),101(ftpadmin)
```

If a username is supplied as an argument, the id command outputs information for that user:

```
$ id vathsa
uid=501(vathsa) gid=100(users) groups=100(users)
```

This chapter's function supports both modes.

```
# Name: getUID
# Desc: outputs a numeric user id
# Args: $1 -> a user name (optional)
```

```
getUID() {
  id $1 | sed -e 's/.*uid=//' -e 's/(.*//'
}
```

This function executes the id command and then uses sed to filter all the unimportant information.