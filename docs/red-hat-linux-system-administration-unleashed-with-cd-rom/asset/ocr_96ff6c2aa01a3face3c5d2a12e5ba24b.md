# log security <userlist>

This enables the logging of security rule violations for <userlist>. The same real, guest, and anonymous list applies as above.

# log syslog

This will redirect the logging operations listed above to the syslog service instead of xferlog.

These are just a few of the settings possible in the /etc/ftpaccess file. See man ftpaccess for a full explanation of all of the options that can be specified.

# nologin

When this file exists, it contains a message that is printed to any user but root who tries to log into the system. Having this file in the /etc directory will effectively block everyone but root from logging into the system.

# sendmail.cf

This is one of the files used to configure the sendmail package—a package to handle mail services in UNIX. The full explanation of sendmail security is beyond the scope of this chapter, but if you choose to run sendmail, you can do some things right away to make sendmail a little more secure. Disable the EXPN and VRFY commands. These commands return information about valid users on the system, and they can be used through trial and error to determine which accounts exist on your system. Once a hacker knows that, he can proceed to try those usernames with other services in an attempt to gain access to your system.

To disable EXPN and VRFY, edit /etc/sendmail.cf and add the following lines (you may want to add them in the Options section of sendmail.cf just for consistency):

```
O PrivacyOptions=noexpn
O PrivacyOptions=novrfy
```

Then restart the sendmail daemon using

```
/etc/rc.d/init.d/sendmail restart
```