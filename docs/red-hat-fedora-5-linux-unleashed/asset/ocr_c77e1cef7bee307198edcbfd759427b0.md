+   4.  The system prompts for a password; it is checked against the encrypted password kept in `/etc/shadow`. Unsuccessful attempts are logged via the syslog facility and can be reviewed with the lastd command.
+   
+   5.  The UID and the GID of the tty (terminal) being used are set.
+   
+   6.  The TERM environment, if it has been set, is preserved.
+   
+   7.  The HOME, PATH, SHELL, TERM, MAIL, and LOGNAME environment variables are set. (If the `-p` option is used, all preexisting environmental variables are preserved.)
+   
+   8.  The PATH defaults to `/usr/local/bin:/bin:/usr/bin`: for normal users and to `/sbin:/bin:/usr/sbin:/usr/bin` for root.
+   
+   9.  Normal greeting messages and mail checking are disabled if the file `.hushlogin` exists in the user's `home directory`; otherwise, those messages are displayed at the end of the login process.
+   
+   10. The user's command shell is started at this point, presenting the user with a command prompt. If no shell is specified for the user in `/etc/passwd`, `/bin/sh` is used by default. (Some UNIX operating systems will just log you back out.) If no home directory is specified in `/etc/passwd`, `/` is used.

When you log in as a regular user, the files that control your environment are found in your `/home/username` directory. These configuration files are normally hidden from view because their filename is preceded by a period (as in `.bashrc`—these are known as `dot files`).

The name of the file indicates which program it is associated with. The files `.bash_logout`, `.bash_profile`, and `.bashrc` all determine how the `bash` shell is used by the user. (These files can, of course, be preset by the system administrator with the user given only read access, so the files cannot be changed. Other shells have their own associated files.)

The `.screenrc` file determines the console screen environment, and the `.xdefaults` file determines much the same thing for `X11`. For Fedora, the `.dmrc` file sources the file `/etc/X11/dm/Sessions/Default.desktop`, which sets the default desktop for the entire system. The `.Xclients-default` file is created by running the `switchdesk` command (the `Desktop Switching Tool` is the name of the GUI interface) to change the default desktop for that user. You would use this command if you occasionally launched `X11` from the command line and desired to change your default desktop. Fedora sets the default as `GNOME`.

Other files might be present depending on the system and the system administrator. The point is that the environment of each user can be set globally through the use of files in `/etc/skel` and individually by allowing user modification of the files in their `/home` directory (or not, depending on the system administration policies).

The system logs all user logins, as well as all users of `su` and `sudo` commands for the sysadmin's review. (The `init`, `syslogd`, and `klogd` applications create the logs.) Modern security-monitoring programs (or simple scripts you create) can scan these files (such as `/var/log/messages`) for anomalies and signal possible security violations.