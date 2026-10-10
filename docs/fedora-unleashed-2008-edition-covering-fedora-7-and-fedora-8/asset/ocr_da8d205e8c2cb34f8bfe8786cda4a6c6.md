# NOTE

In this chapter, you learn how to manage users from the command line. See Chapter 10 for more information on user administration with Fedora using graphical administration utilities, such as the **system-config-users** client.

Use the **useradd** command, along with a user's name, to quickly create a user:

```
# useradd andrew
```

After creating the user, you must also create the user's initial password with the **passwd** command:

```
# passwd andrew
Changing password for user andrew.
New password:
Retype new password:
passwd: all authentication tokens updated successfully.
```

Enter the new password twice. If you do not create an initial password for a new user, the user cannot log in.

You can view **useradd's** default new user settings by using the command and its **-D** option, like this:

```
# useradd -D
GROUP=100
HOME=/home
INACTIVE=-1
EXPIRE=
SHELL=/bin/bash
SKEL=/etc/skel
CREATE_MAIL_SPOOL=yes
```

These options display the default group ID, home directory, account and password policy (active forever with no password expiration), the default shell, and the directory containing defaults for the shell.

The **useradd** command has many different command-line options. The command can be used to set policies and dates for the new user's password, assign a login shell, assign group membership, and manage other aspects of a user's account.

# ## Deleting Users

Use the **userdel** command to delete users from your system. This command removes a user's entry in the system's */etc/passwd* file. You should also use the command's **-r** option to remove all the user's files and directories (such as the user's mail spool file under */var/spool/mail*):

```
# userdel -r andrew
```