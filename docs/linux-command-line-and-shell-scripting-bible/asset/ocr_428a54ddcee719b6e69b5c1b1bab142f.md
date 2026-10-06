# Understanding Linux File Permissions

Some Linux distributions place the Linux user and group utilities in the /usr/sbin directory, which may not be in the PATH environment. If that's the case in your Linux distribution, either add the directory to your PATH or use the absolute filepath to run it.

The -D parameter shows what the useradd command uses if you do not specify them in the command line when creating a new user. This example shows the following default values:

+   - The new user will be added to a common group with group ID 100.
- The new user will have a HOME account created in the directory /home/loginname.
- The account will not be disabled when the password expires.
- The new account will not be set to expire at a set date.
- The new account will use the bash shell as the default shell.
- The system will copy the contents of the /etc/skel to your user's HOME directory.
- The system will create a file for the default user to receive mail.

The next-to-last-value is interesting. The useradd command allows an administrator to create a default HOME directory configuration, then uses that as a template to create the new user's HOME directory. This also allows you to place default files for the system in every new user's HOME directory automatically. On my Linux system, the /etc/skel directory has the following:

```
# ls -al /etc/skel
total 48
drwxr-xr-x 2 root 4096 2001-11-01 00:23 ..
drwxr-xr-x 107 root 12288 2007-09-20 16:53 ..
-rw-r--r-- 1 root 33 2007-02-12 10:18 .bash_logout
-rw-r--r-- 1 root 176 2007-02-12 10:18 .bash_profile
-rw-r--r-- 1 root 124 2007-02-12 10:18 .bashrc
```

You should recognize this file from Chapter 5. These are the standard startup files for the bash environment. The system automatically copies these default files into every user's HOME directory you create.

You can test this by creating a new user using the default system parameters and then looking at the HOME directory for the new user:

```
# /usr/sbin/useradd test
# ls -al /home/test
total 40
drwx------ 2 test test 4096 2007-09-20 18:23 .
d-rwxr-xr-x 7 root 4096 2007-09-20 18:23 ..
-rw-r--r-- 1 test test 33 2007-09-20 18:23 .bash_logout
-rw-r--r-- 1 test test 176 2007-09-20 18:23 .bash_profile
-rw-r--r-- 1 test test 124 2007-09-20 18:23 .bashrc
```