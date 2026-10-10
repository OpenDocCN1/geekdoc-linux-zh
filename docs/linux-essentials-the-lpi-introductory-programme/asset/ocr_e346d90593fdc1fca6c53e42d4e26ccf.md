# 13.3.4  Changing User Accounts and Group Assignment

User accounts and group assignments are traditionally changed by editing the /etc/passwd and /etc/group files. However, many systems contain commands like usermod and groupmod for the same purpose, and you should prefer these since they are safer and—*most*—more convenient to use.

The usermod program accepts mostly the same options as useradd, but changes existing user accounts instead of creating new ones. For example, with

```
usermod -g <group> (user_name)
```

you could change a user’s primary group.

*Caution!* If you want to change an existing user account’s UID, you could edit the *(UID)* field in /etc/passwd directly. However, you should at the same time transfer that user’s files to the new UID using *chown*: “*chown -R tux /home/tux*”—re-confers ownership of all files below user *tux*’s home directory to user *tux*, after you have changed the UID for that account. If “*ls -l*” displays a numerical UID instead of a textual name, this implies that there is no user name for the UID of these files. You can fix this using *chown*.

# 13.3.5  Changing User Information Directly—vipw

The *vipw* command invokes an editor (*vi* or a different one) to edit /etc/passwd directly. At the same time, the file in question is locked in order to keep other users from simultaneously changing the file using, e.g., *passwd* (which changes would be lost). With the *-s* option, /etc/shadow can be edited.

> The actual editor that is invoked is determined by the value of the VISUAL environment variable, alternatively that of the EDITOR environment variable; if neither exists, *vi* will be launched.

# Exercises

+   13.10 [2] Create a user called test. Change to the test account and create a few files using *touch*, including a few in a different directory than the home directory (say, /tmp). Change back to root and change test’s UID. What do you see when listing user test’s files?

+   13.11 [2] Create a user called test1 using your distribution’s graphical tool (if available), test2 by means of the useradd command, and another, test3, manually. Look at the configuration files. Can you work without problems using any of these three accounts? Create a file using each of the new accounts.

+   13.12 [2] Delete user test2’s account and ensure that there are no files left on the system that belong to that user.

+   13.13 [2] Change user test1’s UID. What else do you need to do?

+   13.14 [2] Change user test1’s home directory from /home/test1 to /home/user/test1.

# 13.3.6  Creating, Changing and Deleting Groups

Like user accounts, you can create groups using any of several methods. The “*manual*” method is much less tedious here than when creating new user accounts: Since groups do not have home directories, it is usually sufficient to edit the /etc/group file using any text editor, and to add a suitable new line (see below for *vigr*). When group passwords are used, another entry must be added to /etc/gshadow.