# ## E-mail for Standalone Workstations

Knowing how to run a full-fledged e-mail server is an excellent system administration skill. But this skill won't help you much if your FreeBSD machine isn't intended to be an Internet server providing mail services for dozens of users. What if you're just running a workstation, in the same way that someone might run a Windows desktop machine, with a GNOME or KDE desktop and graphical productivity applications instead of server tools?

Fortunately, a standalone workstation's e-mail setup is much less complex than that of a full-scale server. Still, it's important that you know how to control the standalone workstation environment, and there are some interesting tricks that make standalone computing with FreeBSD quite convenient.

# ## Using Fetchmail to Retrieve E-mail from POP3 and IMAP Servers

Most consumer operating systems have e-mail client programs (such as Outlook, Eudora, Netscape Messenger, and so on) that have their own internal, built-in mechanisms for checking POP3 or IMAP servers. Each one gets your mail in its own way and then stores it in its own fashion internally. Some MUA programs of this type exist for FreeBSD, and they work just fine.

However, you might choose instead to run an MUA such as Mutt, Elm, or Pine on your workstation, just as you would on a server. These programs operate directly on the system's central `/var/mail` directory and your mail spool file inside it, rather than keeping their own internal cache of downloaded messages. This allows you to share the mailbox between programs, search through it using command-line tools, and participate in any number of other testaments to the versatility of Unix.

But to get the messages from the POP3 or IMAP server where your e-mail address stores them (for instance, all mail to a `frank@earthlink.net` address would collect on the `earthlink.net` servers) to your local FreeBSD workstation, something needs to make the POP3 or IMAP connection and deliver the new messages from the remote mailbox to your local one. That something is Fetchmail, a small but versatile utility written by Eric Raymond.

Fetchmail can be installed out of the `ports` (`/usr/ports/mail/fetchmail`) or `packages`. It operates on the basis of a `.fetchmailrc` file in your home directory. This file specifies remote POP3 or IMAP servers to poll for new mail, the intervals at which to check, and numerous other options. Fetchmail then retrieves new mail as specified and relays it to port 25 on your workstation, where Sendmail is listening (in the default configuration). It then will deliver the mail to your local mailbox according to all the rules that would normally apply, such as `.forward` files and mail aliases.

Once Fetchmail has been installed (it is available in the FreeBSD ports collection in the `mail` directory), you will need to configure the `.fetchmailrc` file in your home directory before you can use it. This can be done in one of two ways.