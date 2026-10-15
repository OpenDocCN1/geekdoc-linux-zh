You can then telnet to port 26 and type SMTP commands in an attempt to reproduce the problem you are debugging.

Alternatively, you can have swaks do your SMTP talking for you. It's a Perl script that makes SMTP debugging faster and easier. swaks --help gets you some documentation, and jetmore.org/john/code/#swaks supplies complete details.

If your log files show timeouts of around 30 seconds, that's suggestive of a DNS issue. Timeouts of 5 seconds are more likely to be identd query timeouts. (identd was a daemon intended to identify the actual sender of a mail message, but since it's so easily fooled, no one uses it anymore.)

# 20.15 POSTFIX

Postfix is another popular alternative to sendmail. Wietse Venema started the Postfix project when he spent a sabbatical year at IBM's T. J. Watson Research Center in 1996, and he is still actively developing it. Postfix's design goals included not only security (first and foremost!), but also an open source distribution policy, speedy performance, robustness, and flexibility. All major Linux distributions include Postfix, and since version 10.3, Mac OS X has shipped Postfix instead of sendmail as the default mail system.

> See page 48 for more information about regular expressions.

The most important things to know about Postfix are, first, that it works almost out of the box (the simplest config files are only a line or two long), and second, that it leverages regular expression maps to filter email effectively, especially in conjunction with the PCRE (Perl Compatible Regular Expression) library. Postfix is compatible with sendmail in the sense that Postfix's aliases and .forward files have the same format and semantics as those of sendmail.

Postfix speaks ESMTP. Virtual domains and spam filtering are both supported. For address rewriting, Postfix relies on table lookups from flat files, Berkeley DB, DBM, LDAP, NIS, NetInfo, or SQL databases. Postfix also supports sendmail's milter protocol, so you can easily customize its behavior with a multitude of publicly available milters (external programs that take over specific tasks during an SMTP session; see page 767).

# Postfix architecture

Postfix is composed of several small, cooperating programs that send network messages, receive messages, deliver email locally, etc. Communication among them is performed through local domain sockets or FIFOs. This architecture is quite different from that of sendmail and Exim, wherein a single large program does most of the work.

The master program starts and monitors all Postfix processes. Its configuration file, master.cf, lists the subsidiary programs along with information about how they should be started. The default values set in that file cover most needs; in