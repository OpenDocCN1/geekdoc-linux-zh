
## CONFIGURING SPAMASSASSIN

SpamAssassin looks in many locations for configuration files; for details, refer to the **spamassassin man** page. The easiest configuration file to work with is `/etc/mail/spamassassin/local.cf`. You can edit this file to configure SpamAssassin globally. Users can override these global options and add their own options in the `~/.spamassassin/user_prefs` file. You can put the options discussed in this section in either of these files.

For example, you can configure SpamAssassin to rewrite the Subject line of email it rates as spam. The **rewrite_header** keyword in the configuration files controls this behavior. The word *Subject* following this keyword tells SpamAssassin to rewrite Subject lines. Remove the # from the following line to turn on this behavior:

```
# rewrite_header Subject ****SPAM****
```

The **required_score** keyword specifies the minimum score a piece of email must receive before SpamAssassin considers it to be spam. The default is **5.00**. Set the value of this keyword to a higher number to cause SpamAssassin to mark fewer pieces of email as spam.

```
required_score 5.00
```

Sometimes mail from addresses that should be marked as spam is not, or mail from addresses that should not be marked as spam is. Use the **whitelist_from** keyword to specify addresses that should never be marked as spam and **blacklist_from** to specify addresses that should always be marked as spam:

```
whitelist_from sams@example.com
blacklist_from *@spammer.net
```

You can specify multiple addresses, separated by *spaces*, on the **whitelist_from** and **blacklist_from** lines. Each address can include wildcards. To whitelist everyone sending email from the example.com domain, use **whitelist_from @example.com**. You can use multiple **whitelist_from** and **blacklist_from** lines.

## RUNNING SPAMASSASSIN ON A MAIL SERVER

This section explains how to set up SpamAssassin on a mail server so it processes all email being delivered to local systems before it is sent to users. It shows how to use **procmail** as the MDA and have **procmail** send email through **spamd**.

First, make sure the MTA (**sendmail**) uses **procmail** as the MDA. The first two of the following lines in **sendmail.cf** specify the **procmail** path, command, and flags. The MAILER line defines **procmail** as the mailer. You should not have to make changes to these lines.

```
define('PROCMAIL_MAILER_PATH', `/usr/bin/procmail')dnl
FEATURE(local_procmail, `' procmail -t -Y -a $h -d $u')dnl
MAILER(procmail)dnl
```

Also make sure the **procmail** package is installed on the server system. Next, if the /etc/procmailrc configuration file does not exist, create it so it is owned by root and has 644 permissions and the following contents. If it does exist, append the last two lines from the following file to it:

```
$ cat /etc/procmailrc
DROPPRIVS=yes
:::fw
| /usr/bin/spamc
```

The first line of this file ensures that **procmail** runs with the least possible privileges. The next two lines implement a rule that uses a pipeline to send each user’s incoming email through **spamc**. The `:::` tells **procmail** that a rule follows. The **f** flag indicates a filter; the **w** flag causes **procmail** to wait for the filter to complete and check the exit code. The last line specifies the /usr/bin/spamc utility as the filter.

With this file in place, all email the server receives for local delivery passes through SpamAssassin, which rates it according to the options in the global configuration file. Users with accounts on the server system can override the global SpamAssassin configuration settings in their `~/.spamassassin/user_prefs` files.

When you run SpamAssassin on a server, you typically want to rate the email conservatively so fewer pieces of good email are marked as spam. Setting **required_hits** in the range of 6–10 is generally appropriate. Also, you do not want to remove any email automatically because you could prevent a user from getting a piece of non-spam email. When the server marks email as possibly being spam, users can manually or automatically filter the spam and decide what to do with it.

## USING SPAMASSASSIN WITH A MAIL CLIENT

Alternatively, individual users can run it from their mail clients.

With the SpamAssassin (**spamd**) daemon running and the configuration files set up, you are ready to have SpamAssassin filter your email. To do so, you need to set up two rules in your mail client: The first passes each piece of email through SpamAssassin using **spamc** (page 753), and the second filters email based on whether the X-Spam-Flag line has a YES or NO on it.

This section explains how to set up Evolution to work with SpamAssassin. You can set up other mail clients similarly. Evolution is set up to work with SpamAssassin only when you use an IMAP server. With this setup, you must specify you want to use SpamAssassin in two places: Mail Preferences and Mail Accounts. If you have multiple accounts, you must specify each account you want to check for spam.

![](img/243613168ac865b539f12460d966088e_814_0.png)

Open the **Evolution Preferences** window by selecting **Evolution menubar**; **Edit** > **Preferences**. Click the Mail Preferences icon and then the Junk tab. See Figure 20-1. Put a tick in the check box labeled **Check custom headers for junk**. Two custom header tests that work with SpamAssassin are installed by default. The first checks if **X-Spam-Flag** is set to **YES**; the second checks if **X-Spam-Level** is set to ***. One of these tests will return a true value if SpamAssassin has rated a piece of email as spam.

Next, display the Account Editor window by clicking the **Mail Accounts** icon in the Evolution Preferences window, highlighting the account you want to work with, and clicking **Edit**. In the Receiving Email tab the Server Type must be **IMAP** for these instructions to work. Click the Receiving Options tab (Figure 20-2). Under Options, put a tick in the check box labeled **Apply filters to new messages in Inbox on this server**. Click **OK** to close the Account Editor window. Click **Close** to close the Evolution Preferences window.

> SELinux When **SELinux** is set to use a targeted policy, the **SpamAssassin** daemon, **spamd**, is protected by **SELinux**. You can disable this protection if necessary. For more information refer to “Setting the Targeted Policy with **system-config-selinux**” on page 475.

## ADDITIONAL EMAIL TOOLS

This section covers Webmail and mailing lists. In addition, it discusses how to set up IMAP and POP3 servers.

### WEBMAIL

Traditionally you read email using a dedicated email client such as **mail** or **Evolution**. Recently it has become more common to use a Web application to read email. If you

![](img/243613168ac865b539f12460d966088e_815_0.png)

have an email account with a commercial provider such as Gmail, HotMail, or Yahoo! Mail, you use a Web browser to read email. Email read in this manner is called Webmail. Unlike email you read on a dedicated client, you can read Webmail from anywhere you can open a browser on the Internet: You can check your email from an Internet cafe or a friend’s computer, for example.

**SquirrelMail**

SquirrelMail provides Webmail services. It is written in PHP and supports the IMAP and SMTP protocols. For maximum compatibility across browsers, SquirrelMail renders pages in HTML 4.0 without the use of JavaScript.

SquirrelMail is modular, meaning you can easily add functionality using plugins. Plugins can allow you to share a calendar, for example, or give you the ability to change passwords using the Webmail interface. See the plugins section of the SquirrelMail Web site (www.squirrelmail.org) for more information.

To use SquirrelMail, you must run IMAP (page 763) because SquirrelMail uses IMAP to receive and authenticate email. You must also run Apache (Chapter 26) so a user can use a browser to connect to SquirrelMail.

Prerequisites: Install the following packages:

- squirrelmail
- httpd (page 935)
- sendmail (page 740)
- dovecot (page 763) or another IMAP server
