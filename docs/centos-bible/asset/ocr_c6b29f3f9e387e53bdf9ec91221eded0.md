being directed back to the sender. Besides creating custom error messages, you can also use any Enhanced Mail System Status codes that are compliant with RFC 1893.

The last two lines (beginning with @example3.net and @example2.com) illustrate how e-mail for all recipients for a given domain can all be directed to the same place. In the first case, all example3.net messages go into the mailbox for the user named example-catchall. The last line shows how the users from a particular domain can all be mapped into their same username ($1) on a selected domain name.

Once you have made changes to this file to suit you, you must rebuild the virtuortable database (virtuortable.db file) for the changes to take effect. See "Starting Sendmail and Generating Database Files" for information on this topic.

# ## Adding User Accounts

Ultimately, the e-mail received by your mail server is placed in a user's mailbox, where the user can pick it up and read it at his or her leisure. Each of those usernames must be added as a real user on your CentOS system. For example, to add the user timothy to your CentOS Sendmail server, you could type (as root user):

```
# useradd -s /sbin/nologin timothy
```

This action creates a user account named timothy in the /etc/passwd file, sets the shell to /sbin/nologin, and creates a mailbox that user in /var/spool/mail/timothy. The /sbin/nologin shell prevents the user from logging in to a shell (which is a good security practice when, e.g., you only want a user to have mail or FTP access). Now, Sendmail can direct e-mail to that user's mailbox.

For that user to be able to access his e-mail later from his POP3 client, he will need a password for his user account. Set the password for that user with the passwd command as follows:

```
# passwd timothy
Changing password for user timothy
New UNIX password: *********
Retype new UNIX password: *********
passwd: all authentication tokens updated successfully
```

Make sure that the user has this user account name and password so it can be configured into the user's e-mail client.

# ## Starting Sendmail and Generating Database Files

None of the configuration that you just did to your sendmail.mc, virtuortable, access, domainstable, and mailertable configuration files take effect until they are regenerated into database (.db) files. There are a few different ways you can go about loading your configuration files into database files:

+   * Restarting Sendmail — Each time you reboot your computer or restart the sendmail daemon (by typing service sendmail restart), all Sendmail configuration files (including