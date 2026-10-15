# Objective 2 Manage Spam

This objective explains the following:

+   - Use SpamAssassin
+   - Test SpamAssassin

# Use SpamAssassin

spamassassin (and spamc) expect their input from STDIN.

The simplest way to use SpamAssassin is to pipe the mailbox into the command spamassassin:

```
da51:~# cat /var/spool/mail/root | spamassassin
```

If you want to use SpamAssassin with your Postfix configuration, the easiest way is to use Procmail. You need to edit only three files:

+   - Create the file /etc/procmailrc with this content:

```
#LOGFILE=/tmp/procmail.log
#VERBOSE=yes

# Until now, mail is untagged, you may add rules for
# mail that must not be tagged

:0 hbfw
| /usr/bin/spamc
```

The mail is piped in the first filter rule to the spamc. The flags of the filter rule are explained below:

+   - h. Feed the header to the pipe, file, or mail destination (default).
+   - b. Feed the body to the pipe, file, or mail destination (default).