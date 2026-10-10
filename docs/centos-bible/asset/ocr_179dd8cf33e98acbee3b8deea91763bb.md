# Part IV  Networking

**IMAPv4** — With IMAPv4, messages stay on the server, although you can manipulate those messages from the mail client. Because the messages stay on the server, an IMAPv4 server requires more disk space and uses more CPU. However, you do have the advantage of logging in to different workstations to read your mail and having the mail and folders you have set up appear the same. With all the e-mail on the server, an administrator needs to back up only one machine to keep permanent records of everyone’s e-mail.

CentOS comes with software that is able to provide POP3 and IMAPv4 service. The *dovecot* package is primarily an IMAPv4 server that also contains a small POP3 server. It supports mail in both Maildir (where each mail account can contain multiple folders on the server) and mbox (where all messages are in a single file) formats.

This section describes how to use POP3 to allow the users of your mail server to download their mail messages from your server over the network. POP3 is the simpler of the two protocols for accessing mailboxes over networks.

# Accessing Mailboxes in Linux

When e-mail messages are received on your Sendmail or Postfix mail server, they are sorted to separate files, each of which represents a user’s mailbox. The default location of mailbox files is the `/var/spool/mail` directory. So the login account `jsmith` would have a mailbox:

`/var/spool/mail/jsmith`

While logged into the mail server, `jsmith` could simply type **mail** from a Terminal window to read his e-mail (using the simple, text-based `mail` command). However, because most people prefer to get their e-mail from the comfort of their own desktop computers, you can set up either Post Office Protocol (POP3) or Internet Message Access Protocol (IMAPv4).

POP3 and IMAPv4 servers listen on the network for requests for a user’s e-mail and then either download the entire contents of the mailbox to the user’s mail reader (as with POP3) or let the user manage the messages while the messages stay on the server (as with IMAPv4).

Typically, your mail server will be configured to use either POP3 or IMAPv4 to provide e-mail messages to your users (although it is possible to have both running on the same machine).

The next section explains how to set up an IMAPv4 or POP3 service to allow access to e-mail accounts.

> At times, you may want to check your e-mail on a computer that is not your regular computer, but be able to save messages later. In that case, most mail readers let you choose a setting that copies the e-mail messages without deleting them from your POP3 server. That way, when you get back to your regular computer, you can copy the messages again. IMAPv4 avoids that problem by always keeping the mail messages on the server and letting the user create and work with additional folders on the server.