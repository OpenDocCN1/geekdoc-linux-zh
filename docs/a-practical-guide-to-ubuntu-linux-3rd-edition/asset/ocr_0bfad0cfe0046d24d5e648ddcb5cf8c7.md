The first line of this file ensures that procmail runs with the least possible privileges. The next two lines implement a rule that pipes each user’s incoming email through spamc. The :0 tells procmail that a rule follows. The f flag indicates a filter; the w flag causes procmail to wait for the filter to complete and check the exit code. The last line specifies that the /usr/bin/spamc utility will be used as the filter.

With this file in place, all email that the server system receives for local delivery passes through SpamAssassin, which rates it according to the options in the global configuration file. Users with accounts on the server system can override the global SpamAssassin configuration settings in their ~/.spamassassin/user_prefs files.

When you run SpamAssassin on a server, you typically want to set the required_hits in the range of 6–10 is generally appropriate. Also, you do not want to remove any email automatically because you could prevent a user from getting a piece of nons pam email. When the server marks email as possibly being spam, users can manually or automatically filter the spam and decide what to do with it.

# ## ADDITIONAL EMAIL TOOLS

This section covers Webmail and mailing lists. In addition, it discusses how to set up IMAP and POP3 servers.

# ### WEBMAIL

Traditionally you read email using a dedicated email client such as mail or Evolution. Recently it has become more common to use a Web application to read email. If you have an email account with a commercial provider such as Gmail, HotMail, or Yahoo! Mail, you use a Web browser to read email. Email read in this manner is called *Webmail*. Unlike email you read on a dedicated client, you can read Webmail from anywhere you can open a browser on the Internet: You can check your email from an Internet cafe or a friend’s computer, for example.

![](bbox=[0.1, 0.72, 0.18, 0.74])

SquirrelMail provides Webmail services. It is written in PHP and supports the IMAP and SMTP protocols. For maximum compatibility across browsers, SquirrelMail renders pages in HTML 4.0 without the use of JavaScript.

SquirrelMail is modular, meaning that you can easily add functionality using plugins. Plugins can allow you to share a calendar, for example, or give you the ability to change passwords using the Webmail interface. See the plugins section of the SquirrelMail Web site (www.squirrelmail.org) for more information.

To use SquirrelMail, you must run IMAP (page 735) because SquirrelMail uses IMAP to receive and authenticate mail. You must also run Apache (Chapter 26) so a user can use a browser to connect to SquirrelMail. Because the squirrelmail package depends on several Apache packages, APT installs apache2 when it installs squirrelmail. You need to install an IMAP package manually.