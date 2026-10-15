
## Configuring Mail Server Options

The second section of the `.fetchmailrc` file contains information on each of the mail servers that should be checked for new mail. Here is an example of what the mail section might look like:

```
poll mail.samplanet.org
proto pop3
no dns
```

The first line tells Fetchmail that it should check the mail server mail.samplanet.org at each poll interval that was set in the global options section (which was 600 seconds in our example). Alternatively, the first line can begin with skip. If a mail server line begins with skip, it will not be polled as the poll interval, but will only be polled when it is specifically specified on the Fetchmail command line.

The second line specifies the protocol that should be used when contacting the mail server. In this case, we are using the POP3 protocol. Other legal options are IMAP, APOP, and KPOP. You can also use

AUTO here—in which case, Fetchmail will attempt to automatically determine the correct protocol to use with the mail server.

The third line tells Fetchmail that it should not attempt to do a Dynamic Name Server (DNS) lookup. You will probably want to include this option if you are running over a dial-up connection.

## Configuring User Accounts

The third and final section of `.fetchmailrc` contains information about the user account on the server specified in the previous section. Here is an example:

```
user foobar
pass secretword
fetchall
flush
```

The first line, of course, simply specifies the username that is used to log in to the email server, and the second line specifies the password for that user. Many security conscious people cringe at the thought of putting clear-text passwords in a configuration file, and they should if it is group or world readable. The only protection for this information is to make certain that the file is readable only by the owner; that is, with file permissions of 600.

The third line tells Fetchmail that it should fetch all messages from the server, even if they have already been read.

The fourth line tells Fetchmail that it should delete the messages from the mail server after it has completed downloading them. This is the default, so we would not really have to specify this option. If you want to leave the messages on the server after downloading them, use the option no flush.

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

- Check the POP3 server mail.sampleplanet.org for new mail every 600 seconds.
- Log in using the username foobar and the password secretword.
- Download all messages off the server.
- Delete the messages from the server after it has finished downloading them.
- Send any mail it receives that cannot be delivered to a local user to the account foobar.

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
2 messages for andrew at andrew.hudson.com (5407 octets).
reading message 1 of 2 (3440 octets) ... flushed
reading message 2 of 2 (1967 octets) . flushed
You have new mail in /var/spool/mail/andrew
```
