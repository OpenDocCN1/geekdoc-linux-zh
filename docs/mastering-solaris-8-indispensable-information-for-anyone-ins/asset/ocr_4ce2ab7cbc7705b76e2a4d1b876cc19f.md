# -x option

The -x <number_of_days> option sets the number of days before a password expires from the date that the password was last changed. You can change the parameter from number of days to number of weeks by entering the line MAXWEEKS=<number_of_weeks> into the /etc/default/passwd file.

Solaris ages passwords so that when a certain period of time expires, the password must be changed. You can use the -x option to specify how long a password is active, or you can set the -x option to a null string " " so that a password never expires. Most organizations require that a password be changed every 30, 45, 60, or 90 days.

You can use the passmgt command to create and modify user accounts and their attributes in the passwd and shadow files. The command takes options you can use to set all of the nine fields in the passwd file associated with a user account. Among the options are -a (add a user account), -m (modify a user account), -d (delete a user account), -c (add a comment), -h (specify the home directory), -u (change the UID), -g (change the GID), -o (make a UID nonunique, when used with the -u option), -s (specify the shell), and -l (set the logname). These options are fully described in the man pages and are very similar to those described previously for the useradd command. The passmgt command works only with local accounts and does not alter information stored by the name services.

# The Root Account

The root user, or superuser, has complete access to a system's resources. You can log in as the root user or change to the root user account using the following sequence that both switches your account and changes the environment to the default environment of the root:

```
```
$ su - root
Password:
#
```
```

The display of the number symbol (or hash character symbol) indicates that you are working with root privileges. With root privileges, every action that you take has system-wide implications. A simple error that might delete a subdirectory could with root privileges delete an entire file system. Therefore, you need to exercise caution when using the root account.

You can also enter su - for the same response (because when you use su, Solaris assumes you mean root unless you define a user). Also, the - means it's a login; if you leave the - off, you get the permissions of the user you are switching to (root in this case) but you keep your environment, which is very handy at times.