
2. Make sure that the SpamAssassin `spamd` daemon is running (it should already be on for run levels 2-5), and if it isn't, start it by typing the following as root user:

```
# chkconfig --list spamassassin
spamassassin    0:off  1:off  2:on  3:on  4:on  5:on  6:off
# chkconfig spamassassin on
```

3. Create an `/etc/procmailrc` file (using any text editor, as root user). This `procmailrc` file example pipes all mail messages received by procmail through `spamd` (which is the client side of the `spamd` daemon turned on in the previous step):

```bash
:0fw
| /usr/bin/spamd
```

If you like, you can do a lot more in the `procmailrc` file to deal with spam on a system-wide basis. You could, for example, create procmail recipes that take reported spam e-mail messages and sorts them into a system-wide spam folder or deletes them completely. Likewise, each user can create an individual `$HOME/.procmailrc` file to create personal procmail recipes. (Type **man procmail** for examples of rules in a `procmailrc` file.)

4. Check the `/etc/mail/spamassassin/local.cf` file. This file contains rules that are used system-wide by SpamAssassin, unless they are overriden by a user's individual `$HOME/.spamassassin/user_prefs.cf` file. Here are the contents of the `local.cf` file:

```
required_hits 5
report_safe 0
rewrite_header Subject [SPAM]
```

In SpamAssassin, a scoring system is used to guess at whether a particular message is spam or not. The `required_hits` line shows that a score of **5** is needed to flag the message as spam. You should set that higher for a public mail server (such as 8 or 10). Setting `rewrite_header` to `[SPAM]` has SpamAssassin add the text **[SPAM]** to the Subject line of spam it finds. (Type **man Mail:SpamAssassin:Conf** to see other settings you can use in the `local.cf` file.)

Because false-positives sometimes occur, you risk preventing your users from seeing an e-mail they need if you do system-wide filtering. To avoid this problem, the approach shown here lets the user decide what to do with e-mail tagged as spam. Users can even adjust their own threshold for when a message is believed to be spam.

Next, you should have the users of that mail server set up their own user preferences in their home directories. The preferences set in each user's `$HOME/.spamassassin/user_prefs.cf` file help tell SpamAssassin how to behave for that user's e-mail. Here are examples of lines a user might want to have in that file:

```
required_score                3
whitelist_from                jsmith@example.com  jones@example.net
blacklist_from                *.example.com
```

The `required_score` line (which is set to 5 by default, but set to 3 here) sets the score needed to consider the message to be spam. Scores are based on matching or not matching criteria in the tests SpamAssassin performs. (See http://spamassassin.org/tests.html.)

The `whitelist_from` and `blacklist_from` lines let you set addresses for people, individual hosts, or entire domains that should not be considered as spam (`whitelist_from`) or should always be considered as spam (`blacklist_from`). For other ways to modify SpamAssassin behavior, type the following command:

```bash
man Mail::SpamAssassin::Conf
```

At this point, SpamAssassin should be running and identifying spam based on input from you and the people using your e-mail server. Next, each user needs to decide what to do with the messages that are marked as spam, as described in the following section.

> TIP: Techniques you can use along with SpamAssassin include services such as SpamCop. SpamCop (www.spamcop.net) provides a service that allows you to enter spam messages you receive into a database that helps others block the same spam messages.

# Setting e-mail readers to filter spam

Each user can turn on filtering in his or her e-mail reader to decide what to do with each message tagged as spam by SpamAssassin. A common practice is to direct e-mail marked as spam to a separate folder. Because some real mail can occasionally be mistakenly marked as spam, you can check the spam folder every week or two, just to make sure you don't miss anything.

Here’s an example of how to add a filter rule from Evolution Email:

- 1. Create a folder labeled SPAM under your incoming mailbox.
- 2. Click Tools → Filters.
- 3. From the Filters window, click Add. An Add Rule window appears.
- 4. Identify a rule name (such as Spam) that adds a criterion that looks for a specific header (X-Spam-Flag) containing specific text (YES). Then under Add Action, select an action (Move to Folder) and identify the folder to contain the spam messages (SPAM).

When you ask to receive mail from your mail server, all messages with the X-Spam-Flag set to yes are sorted into your SPAM folder. As an alternative, you can check for the text [SPAM] to appear in the subject line as the criterion for sorting the spam messages.

Other mail readers (Mozilla mail, pine, Netscape mail, and others) also include features for filtering and sorting e-mail based on criteria you enter.

A fairly new feature in Evolution includes some SpamAssassin features within the Evolution framework. Evolution runs a daemonized version of SpamAssassin using the spamd daemon. The spamd daemons automatically filter your mail to find junk mail. When it finds junk mail, it automatically puts it into the Junk folder in the Evolution window. You can ignore those messages or simply scan through them quickly and delete them.

# Getting Mail from the Server (POP3 or IMAP)

After you have set up your mail server, you will want to let users access their e-mail from that server. That means either having each user log in to the mail server to read his or her e-mail or, more likely, configuring POP3 or IMAP to let users access their mail from their workstations. Here are descriptions of POP3 and IMAP:

- **POP3** — With POP3, users download and manage their e-mail messages on their local workstations. POP3 is simpler and requires fewer server resources.
- **IMAP** — With IMAP, messages stay on the server, although you can manipulate those messages from the mail client. Because the messages stay on the server, an IMAP server requires more disk space and uses more CPU. However, you do have the advantage of logging in to different workstations to read your mail and having the mail and folders you have set up appear the same. With all the e-mail on the server, an administrator needs to back up only one machine to keep permanent records of everyone’s e-mail.

Fedora comes with software that is able to provide POP3 and IMAP service. The dovecot package is primarily an IMAP server that also contains a small POP3 server. It supports mail in both maildir (where each mail account can contain multiple folders on the server) and mbox (where all messages are in a single file) formats.

This section describes how to use POP3 to allow the users of your mail server to download their mail messages from your server over the network. POP3 is the simpler of the two protocols for accessing mailboxes over networks.

# Accessing mailboxes in Linux

When e-mail messages are received on your sendmail or postfix mail server, they are sorted to separate files, each of which represents a user’s mailbox. The default location of mailbox files is the /var/spool/mail directory. So the login account jsmith would have a mailbox:

```text
/var/spool/mail/jsmith
```

## Chapter 19: Setting Up a Mail Server

While logged into the mail server, jsmith could simply type `mail` from a Terminal window to read his e-mail (using the simple, text-based `mail` command). However, because most people prefer to get their e-mail from the comfort of their own desktop computer, you can set up either Post Office Protocol (POP3) or Internet Message Access Protocol (IMAP).

POP3 and IMAP servers listen on the network for requests for a user’s e-mail, and then either download the entire contents of the mailbox to the user’s mail reader (as with POP3) or let the user manage the messages while the messages stay on the server (as with IMAP).

Typically, your mail server will be configured to use either POP3 or IMAP to provide e-mail messages to your users (although it is possible to have both running on the same machine).

The next section explains how to set up an IMAP or POP3 service to allow access to e-mail accounts.

> TIP: At times, you may want to check your e-mail on a computer that is not your regular computer, but be able to save messages later. In that case, most mail readers let you choose a setting that copies the e-mail messages without deleting them from your POP3 server. That way, when you get back to your regular computer, you can copy the messages again. IMAP avoids that problem by always keeping the mail messages on the server and letting the user create and work with additional folders on the server.

## Configuring IMAP and POP3 with dovecot

When a user is added to Fedora, a mailbox is configured under that user name in the `/var/spool/mail` directory (such as `/var/spool/mail/chris`). The format of that file, by default, is the traditional mbox format, with all messages and attachments stored in that one file. By configuring the POP3 service on your mail server, users will be able to download their e-mail messages from e-mail clients on other machines. By configuring IMAP, users can work with messages and folders directly on the server.

The following procedure describes how to configure the IMAP or POP3 service in Fedora using dovecot.

- 1. Review the values set in the `/etc/dovecot.conf` file. For this example, I assume the defaults, so you can try dovecot without changing anything in this file. For the purpose of this example, the POP3 protocol is enabled, plain-text passwords are enabled for the standard `/etc/passwd` file, and PAM is used for authentication. Read through the comments in the file to see if there are any settings you want to change.

- 2. Turn on the dovecot service by typing the following (as root user):

```shell
# chkconfig dovecot on
```

(If dovecot is not installed, install it by typing `yum install dovecot`.)

- 3. Start the POP3 service immediately by starting up the dovecot service as follows:

```shell
# /etc/init.d/dovecot start
```
