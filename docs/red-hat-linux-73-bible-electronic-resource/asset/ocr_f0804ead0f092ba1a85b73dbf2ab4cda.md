passwords by default, so you can’t use any administrative login separately until you assign it a password. To make an administrative login useful, you may need to change permissions of some executables, spool files, and log files so that they are owned by the administrative login:

+   * **lp** — This user can control some printing features. Having a separate lp administrator allows someone other than the super user to do such things as move or remove lp logs and print spool files. The home directory for lp is /var/spool/lpd.
+   * **mail** — This user can work with administrative e-mail features. The mail group has group permissions to use mail files in /var/spool/mail (which is also the mail user’s home directory).
+   * **uucp** — This user owns various uucp commands (once used as the primary method for dial-up serial communications). It is the owner of log files in /var/log/uucp, spool files in /var/spool, administrative commands (such as uuchk, uucico, uuconv, and uuxqt) in /usr/sbin, and user commands (uucp, cu, uuname, uustat, and uux) in /usr/bin. The home directory for uucp is /var/spool/uucp.
+   * **bin** — This user owns many commands in /bin in traditional UNIX systems. This is not the case in Red Hat Linux, because root tends to own most executable files. The home directory of bin is /bin.
+   * **news** — This user could be used to do administration of Internet news services, depending on how you set permission for /var/spool/news and other news-related resources. The home directory for news is /var/spool/news.

# Using sudo for assigning administrative privilege

One way to give full or limited root privileges to any non-root user is to set up the *sudo* facility. That simply entails adding the user to /etc/sudoers and defining what privilege you want them to have. Then the user can run any command he or she is privileged to use by preceding that command with the *sudo* command.

The following is an example of how to use the *sudo* facility to cause any users that are added to the wheel group to have full root privileges:

+   1. As the root user, edit the /etc/sudoers file by running the visudo command as follows:

```
# visudo
```

By default, the file is opened in vi, unless your EDITOR variable happens to be set to some other editor acceptable to visudo. The reason for using visudo is that the command will lock the /etc/sudoers file and do some basic sanity checking of the file to make sure it was edited correctly.

> **NOTE:** If you are stuck here, refer to the vi tutorial in Chapter 3 for information on using the vi editor.