This section shows you the traditional way of managing users with various command-line tools. As with any command-line tools you can run these tools via a simple text-based remote shell such as a Telnet or ssh connection.

![](bbox=[0.08, 0.3, 0.18, 0.4])

> Graphical tools require support for the X Window System, as well as a window manager.

# Creating a new user account

Creating a new user account is quite easy from the command line: simply run the useradd command. For example, to create a user called newuser, run the following command:

```
useradd newuser
```

where newuser is the name of the user you want to add. This adds a new entry for user newuser in the /etc/passwd file (and in /etc/shadow if you use shadow passwords) using system defaults. After running the preceding command on a Red Hat Linux system, for example, the /etc/passwd file shows a new line like the following:

```
newuser::!!:506:506::/home/newuser:/bin/bash
```

If you remember the /etc/passwd fields from the earlier discussion (see the Note icon in the “Creating multiple superusers” section earlier in this chapter), you will see that the password (second) field is set to !!. This means that this password is not set and newuser cannot log on yet. So, you need to create a password for this user by running the passwd command as follows:

```
passwd newuser
```

You are asked to enter the password twice. After your password is accepted, it is encrypted and added to the user's entry in the /etc/shadow file.

The UID and the GID values will be selected automatically by useradd. Basically, useradd just increments the last UID in /etc/passwd by 1 and the last GID in /etc/group by 1 to create the UID and GID, respectively, for the new user. You can also set the UID and the GID manually by using the command-line switches -u and -g, respectively. The home directory