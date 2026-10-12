Evolution, a Ximian/Novell product, is the standard email client that comes with Fedora (see Figure 8.5). If you have used Microsoft Outlook, Evolution’s interface will come as no great shock. It really is a drop-in replacement for Outlook and encompasses many of Outlook’s features and benefits, including email, calendaring, contact management, and task management. Here we examine how to get Evolution configured for email access.

![](bbox=[0.2, 0.25, 0.75, 0.55])

**FIGURE 8.5** Ximian Evolution, the default and extremely powerful email client for Fedora.

You need to have the following information to successfully configure Evolution:

+   - Your email address
+   - Your incoming email server name and type (that is, pop.email.com, POP, and IMAP)
+   - Your username and password for the incoming server
+   - Your outgoing email server name (that is, smtp.email.com)

After you have all the information, you can start Evolution. The first screen you are presented with is the Account Setup Assistance (see Figure 8.6).

The next screen permits you to configure Evolution to use your MTA. You can choose POP, IMAP, The local spools found in /var/mail in either mbox or maildir format, a local MTA, or None if you simply want to use the other features of Evolution. As shown in Figure 8.7, you can also set your password.