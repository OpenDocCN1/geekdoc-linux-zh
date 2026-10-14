# # Objective 4—Perform Tasks as a Different User

Some tasks can only be done from the root user account. Sometimes root might want to delegate tasks to normal users. This objective covers both scenarios:

+   - Perform Administrative Tasks as root
+   - Delegate Administrative Tasks with sudo

# ## Perform Administrative Tasks as root

As a system administrator, you are advised to log in as a normal user and only switch to root to perform tasks that require root permissions.

To switch between a normal user and root while performing administrative tasks, you can do the following:

+   - Start Programs from GNOME as Another User
+   - Switch to Another User with su
+   - Switch to Another Group with newgrp

# ## Start Programs from GNOME as Another User

In GNOME, you can start any program with a different UID (as long as you know the password), using the program gnomesu.

From the GNOME desktop, open a command-line dialog by pressing Alt+F2; then enter gnomesu. You are prompted for the root password. After entering it, a terminal window appears. The path is still that of the user logged in to GNOME; if you need the standard environment for root, enter su - in the terminal window.

You can specify a different user than root and also start a program directly with the following syntax: gnomesu --user command. If the command is not in the path of the user logged in to GNOME, you have to enter the full path, such as gnomesu /sbin/yast2, which starts YaST after the root password is entered.

![](bbox=[0.095, 0.604, 0.287, 0.681])

For some programs, you do not need to use gnomesu after entering **Alt+F2**. For example, when you enter yast2 directly, you are automatically prompted for the root password.

# ## Switch to Another User with su

You can use the su (*switch user*) command to assume the UID of root or of other users.

The following is the su syntax:

```
su[options]...[−]user[argument]
```

For example, to change to the user geeko, enter su geeko. To change to the user root, enter su root or su (without a username). If you want to start a login shell when changing to another user account, enter su − username.

![](bbox=[0.094, 0.86, 0.286, 0.936])

Root can change to any user ID without knowing the user's password.