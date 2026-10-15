
You can then telnet to port 26 and type SMTP commands in an attempt to reproduce the problem you are debugging.

Alternatively, you can have swaks do your SMTP talking for you. It's a Perl script that makes SMTP debugging faster and easier. swaks --help gets you some documentation, and jetmore.org/john/code/#swaks supplies complete details.

If your log files show timeouts of around 30 seconds, that's suggestive of a DNS issue. Timeouts of 5 seconds are more likely to be identd query timeouts. (identd was a daemon intended to identify the actual sender of a mail message, but since it's so easily fooled, no one uses it anymore.)

## 20.15 POSTFIX

Postfix is another popular alternative to sendmail. Wietse Venema started the Postfix project when he spent a sabbatical year at IBM's T. J. Watson Research Center in 1996, and he is still actively developing it. Postfix's design goals included not only security (first and foremost!), but also an open source distribution policy, speedy performance, robustness, and flexibility. All major Linux distributions include Postfix, and since version 10.3, Mac OS X has shipped Postfix instead of sendmail as the default mail system.

> See page 48 for more information about regular expressions.

The most important things to know about Postfix are, first, that it works almost out of the box (the simplest config files are only a line or two long), and second, that it leverages regular expression maps to filter email effectively, especially in conjunction with the PCRE (Perl Compatible Regular Expression) library. Postfix is compatible with sendmail in the sense that Postfix's aliases and .forward files have the same format and semantics as those of sendmail.

Postfix speaks ESMTP. Virtual domains and spam filtering are both supported. For address rewriting, Postfix relies on table lookups from flat files, Berkeley DB, DBM, LDAP, NIS, NetInfo, or SQL databases. Postfix also supports sendmail's milter protocol, so you can easily customize its behavior with a multitude of publicly available milters (external programs that take over specific tasks during an SMTP session; see page 767).

### Postfix architecture

Postfix is composed of several small, cooperating programs that send network messages, receive messages, deliver email locally, etc. Communication among them is performed through local domain sockets or FIFOs. This architecture is quite different from that of sendmail and Exim, wherein a single large program does most of the work.

The master program starts and monitors all Postfix processes. Its configuration file, master.cf, lists the subsidiary programs along with information about how they should be started. The default values set in that file cover most needs; in general, no tweaking is necessary. One common change is to comment out a program, for example, smtpd, when a client should not listen on the SMTP port.

The most important server programs involved in the delivery of email are shown in Exhibit D.

### Exhibit D Postfix server programs

![](img/14d78e3cecac4581d37024baf1e94cca_877_0.png)

### Receiving mail

smtpd receives mail entering the system through SMTP. It also verifies that the connecting clients are authorized to send the mail they are trying to deliver. When email is sent locally through the /usr/lib/sendmail compatibility program, a file is written to the /var/spool/postfix/maildrop directory. That directory is periodically scanned by the pickup program, which processes any new files it finds.

All incoming email passes through cleanup, which adds missing headers and rewrites addresses according to the canonical and virtual maps. Before inserting it in the incoming queue, cleanup gives the email to trivial-rewrite, which does minor fixing of the addresses, such as appending a mail domain to addresses that are not fully qualified.

### Managing mail-waiting queues

qmgr manages five queues that contain mail waiting to be delivered:

- incoming – mail that is arriving
- active – mail that is being delivered
- deferred – mail for which delivery has failed in the past
- hold – mail blocked in the queue by the administrator
- corrupt – mail that can't be read or parsed

The queue manager generally selects the next message to process with a simple FIFO strategy, but it also supports a complex preemption algorithm that prefers messages with few recipients over bulk mail.
