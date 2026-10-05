```
[user01@host ~]$ su user02
Password:
[user02@host ~$]
```

If you use the user name, the su or su command attempts to switch to root by default.

```
[user01@host ~]$ su -
Password:
[root@host ~]#
```

The command su starts a non-login shell, while the command su starts a login shell. The main distinction between the two commands is that su - sets up the environment as if it were a new login as user, while su just starts a shell as user, but uses the original user's environment settings.

In most cases, administrators should run su - to get a shell with the target user's normal environment settings. For more information, see the bash(1) man page.

> NOTE The su is most frequently used to get a command-line interface (shell prompt) when running as another user, typically root. However, with the -c option, it can be used like the Windows runas to run an arbitrary program as another user. Run info su to view more details.

# RUNNING COMMANDS WITH SUDO

In some cases, the root user's account may not have a valid password at all for security reasons. In this case, users cannot log in to the system as root directly without a password, and cannot su to get an interactive shell. One tool that can be used to get root access in this case is sudo.

Unlike su, sudo normally requires users to enter their own password for authentication, not the password of the user account they are trying to access. That is, users who sudo to run commands as root do not need to know the root password. Instead, they use their own passwords to authenticate access.

Additionally, sudo can be configured to allow specific users to run any command as some other user, or only some commands as that.

For example, when sudo is configured to allow the user01 to run the command usermod as root, user01 could run the following command to lock or unlock a user account:

```
[user01@host ~]$ sudo usermod -l user02
[sudo] password for user01:
[user01@host ~]$ su - user02
su: Authentication failure
[user01@host ~]$
```

If a user tries to run a command as another user, the sudo configuration does not permit it, the command will be blocked, the attempt will be logged, and by default an email will be sent to the root user.