The configuration options you just inserted configured the entire .fetchmailrc file to look like this:

```
set daemon 600
set postmaster foobar
set logfile ./fetchmail.log

poll mail.sampleplanet.org
proto pop3
no dns

user foobar
pass secretword
fetchall
flush
```

This file tells Fetchmail to do the following:

+   - Check the POP3 server mail.sampleplanet.org for new mail every 600 seconds.
+   - Log in using the username foobar and the password secretword.
+   - Download all messages off the server.
+   - Delete the messages from the server after it has finished downloading them.
+   - Send any mail it receives that cannot be delivered to a local user to the account foobar.

As mentioned before, many more options can be included in the .fetchmailrc file than are listed here. However, these options will get you up and running with a basic configuration.

For additional flexibility, you can define multiple .fetchmailrc files to retrieve mail from different remote mail servers while using the same Linux user account. For example, you can define settings for your most often used account and save them in the default .fetchmailrc file. Mail can then quickly be retrieved like so:

```
$ fetchmail -a
1 message for andrew at mail.ourphotos.me.uk (1108 octets).
reading message 1 of 1 (1108 octets) . flushed
```

By using Fetchmail's -f option, you can specify an alternative resource file and then easily retrieve mail from another server, as follows:

```
$ fetchmail -f .myothermailrc
2 messages for andrew at anrew.hudson.com (5407 octets).
reading message 1 of 2 (3440 octets) ... flushed
reading message 2 of 2 (1967 octets) . flushed
You have new mail in /var/spool/mail/andrew
```