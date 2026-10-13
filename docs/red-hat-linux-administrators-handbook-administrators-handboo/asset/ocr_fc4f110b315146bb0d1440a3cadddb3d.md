want to override a system default, you can specify a command-line option. To override the default home directory, use the -d newdirectory option (where newdirectory is the name of your directory). For example,

```
useradd newuser -d /www/newuser
```

The new user (newuser) will be created, and her home directory will be set to /www/newuser. Note that useradd will create only the final directory, not the entire path. For example, if you specify -d /some/new/dir/myuser as the option, useradd will create myuser only if /some/new/dir already exists.

When the new home directory is created, files contained in the /etc/skel directory are copied to the new home directory. These files are typically the dot configuration files for the default shell. For example, if the default shell is /bin/bash, you should have default versions of .bashrc, .bash_profile, and .bash_login in the /etc/skel directory so that the new user's home directory can be automatically set up with these files.

The useradd that comes with Red Hat Linux creates a private group for the user with the same name as the username. For example, if you run useradd kabir, then a new user named kabir will be created in the /etc/passwd file, and a new group called kabir will be created in the /etc/group file. This method allows the new user to be totally isolated from the rest of the users, and therefore ensures greater privacy for the user. Whenever the new user creates a new file, by virtue of this private group, the file is accessible only by the new user. The user has to change the file permissions explicitly to allow someone else to see the file.

However, if your user account philosophy clashes with this kind of private group idea, you can override it by using the -g group option (where group is the name of your group). For example,

```
useradd mjkabir -g users
```

makes useradd create the new user (mjkabir) with the default group set to the users.

![](bbox=[0.1, 0.78, 0.18, 0.9])

# Tip

You can use the groups username command to find out which user belongs to what group.