"ESMTP" is "extended SMTP," which defines the EHLO command – see:

+   RFC-1869 November 1995 SMTP Service Extensions

RFC-821 defined the TURN command. The ETRN command was introduced in:

+   RFC-1985 August 1996 SMTP Service Extension for Remote Message Queue Starting

In Module 11.6 we explained the `MAIL FROM:` command. When a mail server sends a "bounce message" to say it cannot deliver a message, it uses
`MAIL FROM:<>`
i.e. a null sending domain name. Occasionally you will find mail servers that incorrectly won't accept such a message, because of bugs or mis-configuration.

# ## POP3 and mail clients

The original and current standards for POP3 are, respectively:

+   RFC-1081 November 1988 Post Office Protocol – Version 3

+   RFC-1939 May 1996 Post Office Protocol – Version 3

Linux and most if not all UNIX systems have a command-line e-mail client (or several) that you can use in scripts. These are useful for sending alerts to the system administrator. We use it within a security system that detects whether any files have been changed without authorization (and also in a script which retrieves the lottery results from a Web page and e-mails them to us). These clients can also read mail messages but they don't use POP: they just extract the messages directly from the message store on this machine.

# ## Spam and security

The **sendmail** mail server has historically been a great source of security problems. (Lots of other mail servers have security holes too, probably because they are such large and complex programs.) Module 24.6 and Chapter 25 explain how you can protect your mail server by hiding it behind your firewall, and interposing a small designed-for-security proxy mail server to send/receive messages on the Internet. Chapter 25 also explains how you can counter e-mail virus threats and block spam automatically.

One dial-up ISP (let's call them *some-isp.com*) in the UK does strange things with mail traffic. When you try to connect to any mail server, e.g. with "`telnet mailserver.example.com smtp`," the ISP hijacks the connection and connects you to their own mail server, at *some-isp.com*, instead. We assume this is so they can control people sending spam, but it can be confusing when you are troubleshooting if you haven't seen it before.

For pointers on how to combat spam, see:

+   http://spam.abuse.net

+   http://mail-abuse.org MAPS, the Mail Abuse Prevention System

# ## Appendices

Web Appendix 8: future-proofing your DNS

Web Appendix 37: configuring e-mail settings on different Netscape versions