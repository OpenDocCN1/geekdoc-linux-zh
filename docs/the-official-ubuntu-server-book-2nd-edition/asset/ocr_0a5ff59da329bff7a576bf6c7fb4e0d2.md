+   Logging of all sudo access
+   Every time users run sudo they generate a new log entry in /var/log/auth.log that lists the time, the users who ran sudo, and what commands they ran. This gives an administrator a nice forensics trail. Also, sudo can send the administrator an e-mail whenever a user fails the password check.

+   Can configure passwordless access to rules
+   While you wouldn’t necessarily want to enable this for every sudo rule, there is sometimes a need for a script (particularly cron scripts) to gain root access to run a particular command. Since it’s a cron script, it’s much easier if it can run without your having to code support for the interactive password prompt. It might be tempting to give complete passwordless sudo access to a user, but I recommend you limit rules like this to individual commands.

# Configure sudo

sudo’s configuration file can be found at /etc/sudoers. Ubuntu provides a basic file by default that allows the root user to do anything as any other user and allows members of the admin group to become root (the user you create at install time is automatically added to this group). Your natural inclination might be to open the file with your favorite text editor; however, this is not recommended. The sudo package provides a tool called visudo that you should use whenever you want to make changes to the file, so to view and edit the /etc/sudoers file, type

```
$ sudo visudo
```

The reason you want to use visudo is that it automatically checks your sudoers file for mistakes. Since a mistake in the sudoers file could potentially lock you out of root access, this syntax check is pretty important. If you do make a mistake, visudo will tell you about it after you save and exit. You will have the option to go back and fix your mistake, exit without saving, or ignore its warnings and save anyway (which is not recommended).

While the basics of sudoers syntax are pretty straightforward, the full set of features and syntax for things like user or command groups can get