Both files and directories are now created with the correct permissions to allow all members of the group music to create files and directories inside the Music directory.

The one remaining issue is umask. The necessary setting lasts only until the end of the session and then must be reset. In Chapter 11, we’ll look at making the change to umask permanent.

# Changing Your Password

The last topic we’ll cover in this chapter is setting passwords for yourself (and for other users if you have access to superuser privileges). To set or change a password, the passwd command is used. The command syntax looks like this:

```
passwd [user]
```

To change your password, just enter the passwd command. You will be prompted for your old password and your new password:

```
[me@linuxbox ~]$ passwd
(current) UNIX password:
New UNIX password:
```

The passwd command will try to enforce use of “strong” passwords. This means it will refuse to accept passwords that are too short, are too similar to previous passwords, are dictionary words, or are too easily guessed:

```
[me@linuxbox ~]$ passwd
(current) UNIX password:
New UNIX password:
BAD PASSWORD: is too similar to the old one
New UNIX password:
BAD PASSWORD: it is WAY too short
New UNIX password:
BAD PASSWORD: it is based on a dictionary word
```

If you have superuser privileges, you can specify a username as an argument to the passwd command to set the password for another user. Other options are available to the superuser to allow account locking, password expiration, and so on. See the passwd man page for details.