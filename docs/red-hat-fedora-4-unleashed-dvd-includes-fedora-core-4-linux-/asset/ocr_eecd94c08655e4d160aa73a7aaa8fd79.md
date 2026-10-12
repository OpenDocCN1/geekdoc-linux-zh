directory. For example, if you create a user named *bernice*, the user’s home directory is `/home/bernice`.

> **NOTE**
> 
> In this chapter, you learn how to manage users from the command line. See Chapter 13 for more information on user administration with Fedora using graphical administration utilities, such as the system-config-users client.

Use the *useradd* command, along with a user’s name to quickly create a user:

```
# useradd andrew
```

After creating the user, you must also create the user’s initial password with the *passwd* command:

```
# passwd andrew
Changing password for user andrew.
New password:
Retype new password:
passwd: all authentication tokens updated successfully.
```

Enter the new password twice. If you do not create an initial password for a new user, the user won’t be able to log in.

You can view *useradd*’s default new user settings by using the command and its -D option like this:

```
# useradd -D
GROUP=100
HOME=/home
INACTIVE=-1
EXPIRE=
SHELL=/bin/bash
SHELL=/etc/skel
```

These options display the default group ID, home directory, account and password policy (active forever with no password expiration), the default shell, and the directory containing defaults for the shell.

The *useradd* command has many different command-line options. The command can be used to set policies and dates for the new user’s password, assign a login shell, assign group membership, and other aspects of a user’s account.

# ## Deleting Users

Use the *userdel* command to delete users from your system. This command will remove a user’s entry in the system’s `/etc/passwd` file. You should also user the command’s -r