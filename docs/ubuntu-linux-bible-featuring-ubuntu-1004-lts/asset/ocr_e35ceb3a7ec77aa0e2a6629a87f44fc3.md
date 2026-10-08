# Chapter 27: Managing Users, Groups, and Authentication

The operation of the sudo command is controlled by the file /etc/sudoers, which is a text file that cannot be viewed by mortals for security reasons. To view this file, you should therefore use the sudo command to display it, using a command like the following:

```
$ sudo visudo
```

The sudo command is a special version of the vi command that ensures that only one person is modifying the /etc/sudoers file at a time. You do not need to identify the file /etc/sudoers as an argument—the sudo command knows what file it is to edit. You can, of course, open this file in any text editor, but you won't get the protection against simultaneous edits that the sudo command provides.

As you will see, the /etc/sudoers file can contain blank lines (which are ignored) and comments—any characters that follow the traditional hash mark (#) are interpreted as a comment. The meaningful entries in /etc/sudoers file on a standard Ubuntu system are the following:

```
Defaults env_reset
root ALL=(ALL) ALL
$ admin ALL=(ALL) ALL
```

The first of these lines specifies default options for how the sudo command behaves. The only option in the Ubuntu /etc/sudoers file is the following:

+   - env_reset: Resets the environment to only contain the LOGNAME, SHELL, USERNAME, and SUDO_* environment variables. This prevents the propagation of other environment variables to privileged environments.

One that you may want to change in the /etc/sudoers file is the default period of time for which sudo or sudo caches the credentials of the root user so that you don't have to enter your password within a certain period of time. By default, these commands cache credential for 15 minutes, which many administrators view as being too long. To explicitly set this cache period (known as the time-out period), modify (or add) the Defaults entry in your /etc/sudoers file to look like the following:

```
Defaults env_reset, timestamp_timeout=XX
```

Change XX to be the number of minutes for which you want your privileges to be cached without requiring you to enter your password again. To require all users to enter a password when entering any of these commands, set XX to 0.

The next two lines are the really interesting ones. The following entry states that root can do-anything and execute any command on the system:

```
root ALL=(ALL) ALL
```