**CAUTION:** In general, it is safer to use the `sudo` command to run a single Linux command as the super user instead of running the `su` command. See the description of the `sudo` command later in this chapter.

From any Terminal window or shell, you can simply type the following:

```
$ su
Password: ******
#
```

When you are prompted, type in the root user's password. The prompt for the regular user ($) will be changed to the super user prompt (#). At this point, you have full permission to run any command and use any file on the system. However, one thing that the `su` command doesn't do when used this way is read in the root user's environment. As a result, you may type a command that you know is available and get the message “command not found.” To fix this problem, you can use the `su` command with the dash (-) option instead, as follows:

```
$ su -
Password: ******
#
```

You still need to type the password, but after you do that, everything that normally happens at login for the root user will happen after the `su` command is completed. Your current directory will be root's home directory (probably `/root/`), and things like the root user's `PATH` variable will be used. If you became the root user by just typing `su`, rather than `su -`, you would not have changed directories or the environment of the current login session.

**TIP:** When you become the root user during someone else's session, a common mistake is to leave files or directories in the user's directories that are owned by root. If you do this, be sure to use the `chown` or `chmod` command to make the files and directories you modify open to the user that you want to own them. Otherwise, you will probably get a phone call in a short time, asking you to come back and fix it.

You can also use the `su` command to become another user other than root. For example, to have the permissions of a user named chum, you could type the following:

```
$ su - chum
```

Even if you were the root user before you typed this command, you would only have the permission to open files and run programs that are available to chum. As the root user, however, after you type the `su` command to become another user, you don't need a password to continue. If you type that command as a regular user, you must type the new user's password.

When you are finished using super user permissions, return to the previous shell by exiting the current shell. Do this by pressing Ctrl+D or by typing `exit`.