```
mail naba@comcast.net
Subject: Testing e-mail
This is from my Red Hat Linux system.
^C: Press Ctrl+D
```

The mail command is a simple mail-user agent. In the preceding example, I specify the addressee — naba@comcast.net — in the command line. The mail program prompts for a subject line. Following the subject, I enter my message and end it with a line that contains only a period. When prompted for a Cc:, I press Ctrl+D. After I end the message, the mail-user agent passes the message to sendmail — the mail-transport agent — for delivery to the specified address. Because my system is already connected to the Internet, sendmail delivers the mail message immediately.

To verify the delivery of mail, I check my mail from my ISP and see that the message has arrived. I can also send a reply back, provided my system has an official DNS host name and is in the ISP's DNS database.

Thus, the initial sendmail configuration file that comes with Red Hat Linux should be adequate for sending and receiving e-mail, provided that your Red Hat Linux system has an Internet connection and a registered domain name.

# The mail-delivery mechanism

On an Internet host, the sendmail mail-transport agent delivers mail using the Simple Mail Transfer Protocol (SMTP). SMTP-based mail-transport agents listen to the TCP port 25 and use a small set of text commands to exchange information with other mail-transport agents. In fact, SMTP commands are simple enough that you can use them manually from a terminal to send a mail message. The following example shows how I use SMTP commands to send a mail message to my account on the Red Hat Linux PC from a telnet session running on the same system:

```
telnet localhost 25
Trying 127.0.0.1...
Connected to localhost.
Escape character is '^]'.
220 localhost.localdomain ESMTP Sendmail 8.12.9/8.12.9; Tue, 15 Jul 2003 19:22:24 -0400

help
214-2.0.0 This is sendmail version 8.12.9
214-2.0.0 Topics:
214-2.0.0 HELO EHLO MAIL RCPT DATA
214-2.0.0 RSET NOOP QUIT HELP VRFY
214-2.0.0 EXPN VERB ETRN DSN AUTH
214-2.0.0 STARTTLS
214-2.0.0 For more info use *HELP <topic>*.
214-2.0.0 To report bugs in the Implementation send email to
214-2.0.0 sendmail-bugs@sendmail.org.
214-2.0.0 For local information send email to Postmaster at your site.
214-2.0.0 End of HELP info
```