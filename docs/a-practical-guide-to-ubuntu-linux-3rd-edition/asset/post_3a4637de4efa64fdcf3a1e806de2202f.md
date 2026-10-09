
## CONFIGURING SPAMASSASSIN

SpamAssassin looks in many locations for configuration files; for details, refer to the spamassassin man page. The easiest configuration file to work with is `/etc/mail/spamassassin/local.cf`. You can edit this file to configure SpamAssassin globally. Users can override these global options and add their own options in the `~/spamassassin/user_prefs` file. You can put the options discussed in this section in either of these files.

For example, you can configure SpamAssassin to rewrite the Subject line of email that it rates as spam. The `rewrite_header` keyword in the configuration files controls this behavior. The word Subject following this keyword tells SpamAssassin to rewrite Subject lines. Remove the # from the following line to turn on this behavior:

```
# rewrite_header Subject *****SPAM*****
```

The `required_score` keyword specifies the minimum score a piece of email must receive before SpamAssassin considers it to be spam. The default is `5.00`. Set the value of this keyword to a higher number to cause SpamAssassin to mark fewer pieces of email as spam.

```
required_score 5.00
```

Sometimes mail from addresses that should be marked as spam is not, or mail from addresses that should not be marked as spam is. Use the `whitelist_from` keyword to specify addresses that should never be marked as spam and `blacklist_from` to specify addresses that should always be marked as spam:

```
whitelist_from sams@example.com
blacklist_from @spammer.net
```

You can specify multiple addresses, separated by spaces, on the `whitelist_from` and `blacklist_from` lines. Each address can include wildcards. To whitelist everyone sending email from the example.com domain, use `whitelist_from @example.com`. You can use multiple `whitelist_from` and `blacklist_from` lines.

## RUNNING SPAMASSASSIN ON A MAIL SERVER

This section explains how to set up SpamAssassin on a mail server so that it will process all email being delivered to local systems before it is sent to users. It shows how to use `procmail` as the MDA and have `procmail` send email through `spamc`. Also make sure the `procmail` package is installed on the server system. Next, if the `/etc/procmailrc` configuration file does not exist, create it so that this file is owned by `root` and has `644` permissions and the following contents. If it does exist, append the last two lines from the following file to it:

```
$ cat /etc/procmailrc
DROPPRIVS=yes
:$0 fw
| /usr/bin/spamc
```

The first line of this file ensures that procmail runs with the least possible privileges. The next two lines implement a rule that pipes each user’s incoming email through spamc. The :0 tells procmail that a rule follows. The f flag indicates a filter; the w flag causes procmail to wait for the filter to complete and check the exit code. The last line specifies that the /usr/bin/spamc utility will be used as the filter.

With this file in place, all email that the server system receives for local delivery passes through SpamAssassin, which rates it according to the options in the global configuration file. Users with accounts on the server system can override the global SpamAssassin configuration settings in their ~/.spamassassin/user_prefs files.

When you run SpamAssassin on a server, you typically want to set the required_hits in the range of 6–10 is generally appropriate. Also, you do not want to remove any email automatically because you could prevent a user from getting a piece of nons pam email. When the server marks email as possibly being spam, users can manually or automatically filter the spam and decide what to do with it.

### ADDITIONAL EMAIL TOOLS

This section covers Webmail and mailing lists. In addition, it discusses how to set up IMAP and POP3 servers.

#### WEBMAIL

Traditionally you read email using a dedicated email client such as mail or Evolution. Recently it has become more common to use a Web application to read email. If you have an email account with a commercial provider such as Gmail, HotMail, or Yahoo! Mail, you use a Web browser to read email. Email read in this manner is called *Webmail*. Unlike email you read on a dedicated client, you can read Webmail from anywhere you can open a browser on the Internet: You can check your email from an Internet cafe or a friend’s computer, for example.

![](img/2344fc4a798f29dca9e8b5ed7288171a_781_0.png)

SquirrelMail provides Webmail services. It is written in PHP and supports the IMAP and SMTP protocols. For maximum compatibility across browsers, SquirrelMail renders pages in HTML 4.0 without the use of JavaScript.

SquirrelMail is modular, meaning that you can easily add functionality using plugins. Plugins can allow you to share a calendar, for example, or give you the ability to change passwords using the Webmail interface. See the plugins section of the SquirrelMail Web site (www.squirrelmail.org) for more information.

To use SquirrelMail, you must run IMAP (page 735) because SquirrelMail uses IMAP to receive and authenticate mail. You must also run Apache (Chapter 26) so a user can use a browser to connect to SquirrelMail. Because the squirrelmail package depends on several Apache packages, APT installs apache2 when it installs squirrelmail. You need to install an IMAP package manually.

Install the following packages:

- squirrelmail
- apache2 (page 902; installed as a dependency when you install squirrelmail)
- exim4 (page 714) or sendmail
- php5-cgi
- dovecot-imapd (page 735) or another IMAP server

You do not need to start SquirrelMail, nor do you have to open any ports for it. However, you need to configure, start, and open ports (if the server is running on a system with a firewall) for exim4 (page 718), IMAP (page 735), and Apache (page 903).

The SquirrelMail files reside in /usr/share/squirrelmail. Create the following link to make SquirrelMail accessible from the Web:

```
$ sudo ln -s /usr/share/squirrelmail /var/www/mail
```

Give the following command to configure SquirrelMail:

```
$ sudo squirrelmail-configure

SquirrelMail Configuration : Read: config.php (1.4.0)
------------------------------------------------------------

Main Menu --
1. Organization Preferences
2. Server Settings
3. Folder Defaults
4. General Options
5. Themes
6. Address Books
7. Message of the Day (MOTD)
8. Plugins
9. Database
10. Languages

D. Set pre-defined settings for specific IMAP servers

C Turn color on
S Save data
Q Quit

Command >>
```

This menu has multiple levels. When you select a setting (and not a submenu), squirrelmail-configure displays information that can help you decide how to answer the question it poses. Set the server's domain name (number 1 on the Server Settings page) and the name of the IMAP server you are using (D on the main menu). SquirrelMail provides several themes; if you do not like the way SquirrelMail looks, choose another theme from Themes (number 5). When you are finished making changes, exit from squirrelmail-configure. Run squirrelmail-configure whenever you want to change the configuration of SquirrelMail.

SquirrelMail provides a Web page that tests its configuration. Point a browser on the server to localhost/mail/src/configtest.php. Replace localhost with the IP address or FQDN of the server to view the page from another system. SquirrelMail checks its configuration and displays the results on this page.

![](img/2344fc4a798f29dca9e8b5ed7288171a_783_0.png)

**Figure 20-2** SquirrelMail running a configuration test

Figure 20-2 shows that SquirrelMail cannot connect to the IMAP server on the local system, probably because IMAP has not been installed.

Point a Web browser at **localhost/mail** or **localhost/mail/src/login.php** to display the SquirrelMail login page (Figure 20-3). Replace **localhost** with the IP address or FQDN of the server to view the page from another system. Enter the username and password of a user who has an account on the server system.

![](img/2344fc4a798f29dca9e8b5ed7288171a_783_1.png)

**Figure 20-3** SquirrelMail login page

## MAILING LISTS

A mailing list can be an asset if you regularly send email to the same large group of people. It offers several advantages over listing numerous recipients in the To or Cc field of an email or sending the same email individually to many people:

- **Anonymity**—None of the recipients of the email can see the addresses of the other recipients.
