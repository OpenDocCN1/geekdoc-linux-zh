If you are in a graphical desktop environment, click on the terminal icon to open a text terminal. (See Figure 2.1.)

![](bbox=[0.04, 0.16, 0.84, 0.23])

A terminal window will open. It will contain a prompt that looks something like this:

```
[dave@machine dave]$ s
```

Your prompt will look slightly different because it is based on your user name, machine name, and working directory. In the examples in this book, we will show the shell prompt like this:

```
$ .
```

If you log in as root, the dollar sign ($) in the prompt will be replaced with a pound sign (#) to remind you that you are root. Be extra vigilant when operating as root because a mistake can wipe out your system.

# ## Logging Out

To log out of KDE, click on the logout icon to close your KDE session. (See Figure 2.2.)

![](bbox=[0.04, 0.68, 0.84, 0.75])

If you are not in graphics mode or simply wish to log out of the terminal you opened (but not KDE as a whole), type **exit** in the terminal:

```
$ exit
```

# ## Changing Your Password

It is important to keep your password secret. A strong password is the first and best line of defense against an attack on your Linux system.

If you ever need to change your password, follow this procedure.

+   1. Open a terminal window by clicking on the terminal icon as described earlier.
+   2. Enter the command: `passwd`
+   3. Enter your old password when prompted.