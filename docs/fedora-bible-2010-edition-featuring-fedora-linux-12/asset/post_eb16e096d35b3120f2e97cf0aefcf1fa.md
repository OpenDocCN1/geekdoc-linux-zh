
qualified domain name to this file, Postfix will use your local hostname as the name of the mail service it represents.

- **Mailboxes** (`/var/spool/mail`)—Directory containing incoming mail files, with each user’s mailbox represented by a file of the user’s name. (This is the same default spool directory used by sendmail.)
- **Mail queue** (`/var/spool/postfix`)—Location of directories where mail messages are queued for delivery.
- **Mail log** (`/var/log/mail` and `/var/log/maillog`)—Location of mail log files.

Although most options you need for Postfix are described in the `/etc/postfix/main.cf` file, you can see many more available options in the `main.cf.default` file in `/usr/share/doc/postfix-*/`. Based on the default configuration in the `main.cf` file, here is how Postfix will handle outbound and incoming mail:

- **Outbound mail** — The local hostname is added as the sending host for the mail posted from this computer. You might want to change it to the local domain name (set `myorigin = $mydomain`).
- **Incoming mail** — Only mail destined for the local hostname is kept on the local server by default. Other mail is forwarded. To have all mail for your domain kept on the local server, add `$mydomain` to the `mydestination` line. You must also change the `inet_interfaces` line to not merely listen for incoming mail sent from the local host. For example, the line could appear as follows to listen on all interfaces:

```
inet_interfaces = all
```

For complete information on configuring Postfix, refer to `http://www.postfix.org/docs.html`.

# Stopping Spam with SpamAssassin

Despite the fact that it is rude and antisocial, there are people who send out thousands of unsolicited e-mail messages (referred to as spam), hoping to get a few responses. Due to the economics of the Internet, spammers can send out literally millions of messages. Just a very small number of respondents is enough to make a profit for the spammers. Furthermore, modern spam can be dangerous, including messages designed to fool users into entering user names and passwords (called *phishing*) or messages that try to exploit vulnerable systems (particularly Windows systems).

Because Linux systems are often used as mail servers, tools for scanning mail messages for spam and viruses have become quite sophisticated over the years. In this chapter, I describe how to use a tool called SpamAssassin to deal with spam and viruses on your mail server. If this doesn’t meet your needs, you might add the ClamAV virus scanner to test mail messages for actual malware attachments. You can learn about ClamAV and how to use it with different mail software by using the following links:

- **ClamAV** (www.clamav.net) — Command-line virus scanner with database update features. The clamav package is in the Fedora repository (yum install clamav).
- **Klamav** (http://klamav.sourceforge.net/klamavwiki/index.php) — The KDE version of ClamAV (yum install klamav).
- **Third-party ClamAV Apps** (www.clamav.net/3rdparty.html) — Find links to third-party software that works with ClamAV.

## Using SpamAssassin

With SpamAssassin, you can configure your incoming mail service to tag messages it believes to be spam so you and your users can deal with those messages as you choose.

There are several methods that SpamAssassin uses to identify spam:

- **Checking mail headers** — Examines the headers of your incoming mail to look for well-known tricks used to make the e-mail look valid.
- **Checking mail text** — Looks for text style, content, and disclaimers in message bodies that are commonly used in spam.
- **Checking blacklists** — Checks blacklists to find e-mail sent from sites previously known to relay spam. (The mail-abuse.com site provides a search tool for checking if a server at a particular IP address has been blacklisted. To use that tool, go to www.mail-abuse.com/cgi-bin/lookup.)
- **Checking spam signatures** — Compares e-mail signatures. Because spam often consists of the exact same message sent thousands of times, taking signatures of spam messages lets SpamAssassin compare your message to a database of known spam messages. SpamAssassin uses Vipul’s Razor (see http://razor.sourceforge.net).

Although there are many different ways to deal with spam (or rather, e-mail that might be spam), most of the experts I have consulted like to configure SpamAssassin to simply tag incoming e-mail messages that appear to be spam. Then they encourage each user of the e-mail server to create his or her own rules for filtering the spam.

> **NOTE:** Although the procedure here describes how to use SpamAssassin from the RPM package that comes with the latest version of Fedora, many people get their version of SpamAssassin directly from the SpamAssassin Web site. Because anti-spam software is evolving so quickly (to keep ahead of spammers), some people like to make sure they have the very latest software. Instructions for installing the spamassassin package from source code are available from the SpamAssassin download page: http://spamassassin.apache.org/download.cgi. Typically you can simply run the rpm-build -tb command on the Mail-Spamassassin tar file to create a new RPM.

## Setting up SpamAssassin on your mail server

Here’s a quick procedure for enabling SpamAssassin and having your users choose what to do with spam messages that are encountered:

1. Configure your Mail Transport Agent (sendmail or Postfix) to use the `procmail` command as its mailer. For sendmail, it is already configured as the default mailer, based on the following line in the `/etc/mail/sendmail.mc` file:
   `FEATURE(local_procmail,`'`,procmail -t -Y -a $h -d $u`)dnl`
2. Make sure that the SpamAssassin `spamd` daemon is running, and if it isn’t, start it by typing the following (as root user):
   ```
   # chkconfig spamassassin on
   # chkconfig --list spamassassin
   spamassassin  0:off  1: off  2:on  3:on  4:on  5:on  6:off
   # service spamassassin start
   ```
3. Create an `/etc/procmailrc` file (using any text editor, as root user). This `procmailrc` file example pipes all mail messages received by procmail through `spamd` (which is the client side of the `spamd` daemon turned on in the previous step):
   ```
   :0fw
   | /usr/bin/spamc
   ```

If you like, you can do a lot more in the `procmailrc` file to deal with spam on a system-wide basis. You could, for example, create procmail recipes that take reported spam e-mail messages and sort them into a system-wide spam folder or deletes them completely. Likewise, each user can create an individual `$HOME/.procmailrc` file to create personal procmail recipes. (Type `man procmailrc` for examples of rules in a `procmailrc` file.)

4. Check the `/etc/mail/spamassassin/local.cf` file. This file contains rules that are used system-wide by SpamAssassin, unless they are overridden by a user’s individual `$HOME/.spamassassin/user_prefs.cf` file. Here are the contents of the `local.cf` file:
   ```
   required_hits 5
   report_safe 0
   rewrite_header Subject [SPAM]
   ```

In SpamAssassin, a scoring system is used to guess at whether a particular message is spam or not. The `required_hits` line shows that a score of 5 is needed to flag the message as spam. You should set that higher for a public mail server (such as 8 or 10). Setting `rewrite_header` to `[SPAM]` has SpamAssassin add the text `[SPAM]` to the Subject line of spam it finds. (Type `man Mail::SpamAssassin::Conf` to see other settings you can use in the `local.cf` file.)

Because false-positives sometimes occur, you risk preventing your users from seeing an e-mail they need if you do system-wide filtering. To avoid this problem, the approach shown here lets the user decide what to do with e-mail tagged as spam. Users can even adjust their own threshold for when a message is believed to be spam.

Next, you should have the users of that mail server set up their own user preferences in their home directories. The preferences set in each user's `$HOME/.spamassassin/user_prefs.cf` file help tell SpamAssassin how to behave for that user's e-mail. Here are examples of lines a user might want to have in that file:

```
required_score 3
whitelist_from jsmith@example.com bjones@example.net
blacklist_from *.example.org
```

The `required_score` line (which is set to 5 by default, but set to 3 here) sets the score needed to consider the message to be spam. Scores are based on matching or not matching criteria in the tests SpamAssassin performs. (See http://spamassassin.apache.org/tests.html.)

The `whitelist_from` and `blacklist_from` lines let you set addresses for people, individual hosts, or entire domains that should not be considered as spam (`whitelist_from`) or should always be considered as spam (`blacklist_from`). For other ways to modify SpamAssassin behavior, type the following command:

```
man Mail::SpamAssassin::Conf
```

At this point, SpamAssassin should be running and identifying spam based on input from you and the people using your e-mail server. Next, each user needs to decide what to do with the messages that are marked as spam, as described in the following section.

> TIP: Techniques you can use along with SpamAssassin include services such as SpamCop. SpamCop (http://www.spamcop.net) provides a service that allows you to enter spam messages you receive into a database that helps others block the same spam messages.

## Setting e-mail readers to filter spam

Each user can turn on filtering in his or her e-mail reader to decide what to do with each message tagged as spam by SpamAssassin. A common practice is to direct e-mail marked as spam to a separate folder. Because some real mail can occasionally be mistakenly marked as spam, you can check the spam folder every week or two, just to make sure you don't miss anything.

Here’s an example of how to add a filter rule from Evolution Email:

1. Create a folder labeled SPAM under your incoming mailbox.
2. Click Edit → Message Filters.
