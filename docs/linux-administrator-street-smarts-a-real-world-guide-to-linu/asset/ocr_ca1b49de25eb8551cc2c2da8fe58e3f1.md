# Criteria for Completion

To complete this task, you should have configured your super server to enable an FTP server. This task requires first identifying which super server your computer runs and then making appropriate changes to the `/etc/inetd.conf` file or to a file in the `/etc/xinetd.d` directory. You must then verify that the FTP server is running by accessing it with an FTP client program.

# Task 6.6: Operate a Mail Server

Email is a very important Internet feature; it enables users to send messages to one another to be read at the recipient’s leisure. This function requires computers that run Simple Mail Transfer Protocol (SMTP) server software such as the popular sendmail (http://www.sendmail.org). This software accepts messages that are created in email client programs such as mutt or KMail and delivers the messages across the Internet to another mail server. The recipient server then stores the messages in a form that enables their retrieval by local programs or via another server that runs a protocol such as the Post Office Protocol (POP) or the Internet Message Access Protocol (IMAP).

This task focuses upon sendmail configuration, which is the most central and critical part of the email delivery equation. A full email server is likely to support POP or IMAP in addition to SMTP or might support user logins and access via mail client programs. Be aware that SMTP is a complex protocol and SMTP server configuration is correspondingly complex. This task barely scratches the surface. If you have a need to configure a real email server, you should consult a book that’s dedicated to the software you choose to run.

![](bbox=[0.14, 0.61, 0.26, 0.74])

Although sendmail is the most popular SMTP server software on the Internet at large, it’s not the only option. Postfix (http://www.postfix.org), Exim (http://www.exim.org), and qmail (http://www.qmail.org) are all popular in Linux, and some Linux distributions use one of these as the default mail server rather than sendmail. If your system is configured in this way, you must either replace your current mail server with sendmail (which could render it inoperative until you fix it) or simply read through this task without actually changing your configuration.

# Scenario

You are in charge of setting up the mail server for Pangaean University (pangaean.edu), which also manages mail for the Institute for Mesozoic Studies (mesozoi.c.edu). You must configure the server to accept mail addressed to users at either domain name. You must set up several email aliases, redirecting mail for certain users (such as postmaster) to specific users on the system. You must also configure some Linux workstations' mail server programs to relay mail through the main Pangaean University mail server system (mail.pangaean.edu).