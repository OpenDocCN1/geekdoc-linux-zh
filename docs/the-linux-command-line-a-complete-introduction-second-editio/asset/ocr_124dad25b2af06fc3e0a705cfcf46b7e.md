Now we test to see whether the new permissions fix the problem. bill sets his umask to 0002, removes the previous test file, and creates a new test file and directory.

```
[bill@linuxbox ~]$ umask 0002
[bill@linuxbox ~]$ rm /usr/local/share/Music/test_file
[bill@linuxbox ~]$ > /usr/local/share/Music/test_file
[bill@linuxbox ~]$ mkdir /usr/local/share/Music/test_dir
[bill@linuxbox ~]$ ls -l /usr/local/share/Music
drwxrwxr-x 2 bill music 4096 2018-03-24 20:24 test_dir
-rw-rw-r-- 1 bill music 0 2018-03-24 20:22 test_file
[bill@linuxbox ~]$
```

Both files and directories are now created with the correct permissions to allow all members of the group music to create files and directories inside the Music directory.

The one remaining issue is umask. The necessary setting lasts only until the end of session and must be reset. We'll look at making the change to umask permanent in Chapter 11.

# Changing Your Password

The last topic we'll cover in this chapter is setting passwords for yourself (and for other users if you have access to superuser privileges). To set or change a password, use the passwd command. The command syntax looks like this:

```
passwd [user]
```

To change your password, just enter the passwd command. You will be prompted for your old password and your new password.

```
[me@linuxbox ~]$ passwd
(current) UNIX password:
New UNIX password:
```

The passwd command will try to enforce use of “strong” passwords. This means it will refuse to accept passwords that are too short, are too