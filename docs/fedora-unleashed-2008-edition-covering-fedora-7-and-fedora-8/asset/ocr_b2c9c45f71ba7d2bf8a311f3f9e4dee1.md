# TIP

It is never a good idea to use an *Internet Relay Chat* (IRC) client as the root user, and you might not want to run it using your regular user account. Just create a special new user just for IRC and so that user in a terminal window to launch your IRC client.

The `su` command spawns a new shell, changing both the UID and GID of the existing user and automatically changes the environmental variables associated with that user. This behavior is known as *inheriting the environment*. See Chapter 4, “Command-Line Quick Start,” for more information on environmental variables.

The syntax for the `su` command is this:

```
$ su option username arguments
```

The man page for `su` gives more details, but some highlights of the `su` command are as follows:

+   - `-C, --command COMMAND`
+       	    pass a single COMMAND to the shell with `-c`
+   
+   - `-m, --preserve-environment`
+       	    do not reset environment variables
+   
+   - `-l` a full login simulation for the substituted user,
+       	    the same as specifying the dash alone

You can invoke the `su` command in different ways that yield diverse results. By using `su` alone, you can become root, but you keep your regular user environment. You can verify this by using the `printenv` command before and after the change. Note that the working directory (you can execute `pwd` as a command line to print the current working directory) has not changed. By executing the following, you become root and inherit root’s environment:

```
$ su -
```

By executing the following, you become that user and inherit the super user’s environment—a pretty handy tool. (Remember: Inheriting the environment comes from using the dash in the command; omit that, and you keep your “old” environment.) To become another user, specify a different user’s name on the command line:

```
$ su - other_user
```

When leaving an identity to return to your usual user identity, use the `exit` command. For example, while logged on as a regular user, use this:

```
$ su -
```