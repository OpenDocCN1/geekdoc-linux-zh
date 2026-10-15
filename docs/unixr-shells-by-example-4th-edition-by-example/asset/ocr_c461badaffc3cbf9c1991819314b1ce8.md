Traditionally, when a system administrator wants to run some commands that require root privileges, he or she logs onto an unprivileged account first, and then uses the su command to switch to superuser. A new root-owned shell will be started, and after running privileged commands (presumably to fix a problem that the user can't handle), the superuser will exit from the root shell and return to the account of the unprivileged user.

# EXAMPLE 16.2

```
1 $ id # or use whoami instead
uid=501(ellie) gid=100(users) groups=100(users)
2 $ echo $PATH
/usr/local/bin:/usr/bin:/bin:/usr/X11R6/bin:.
3 $ su
Password:
4 # id
uid=0(root) gid=0(root) groups=0(root)
5 # echo $PATH
/usr/local/bin:/usr/bin:/bin:/usr/X11R6/bin:.
6 # exit
exit
7 $ su -
Password:
8 # id
uid=0(root) gid=0(root) groups=0(root)
9 # echo $PATH
/usr/sbin:/bin:/usr/sbin:/usr/X11R6/bin
```

# EXPLANATION

+   1. The id command shows that ellie is the current user.
+   2. The PATH variable for user ellie is displayed.
+   3. The su command is run to switch user to root. Note that a password must be provided.
+   4. The prompt has changed to a pound sign (#). This almost always signifies a superuser account. The id command is run, showing that the current shell has root permissions.
+   5. When the value of the PATH variable is displayed, it shows the same value as before. This is because the plain su command (without the dash) was used to become root. Plain su does not change the value of the PATH variable.
+   6. Exit is run to terminate the shell created by the su command.
+   7. The prompt changes back to a dollar sign because the previous command terminated the root-owned shell. The su command is run, this time including the dash option.
+   8. The id command verifies that root is the current user.
+   9. Because this shell was run using the dash option to the su command, the PATH value from the root account was used. When the value of the PATH variable is echoed, it shows root's path.