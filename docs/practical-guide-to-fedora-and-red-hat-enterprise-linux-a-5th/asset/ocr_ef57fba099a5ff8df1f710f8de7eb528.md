Also make sure the **procmail** package is installed on the server system. Next, if the `/etc/procmailrc` configuration file does not exist, create it so that this file is owned by **root** and has 644 permissions and the following contents. If it does exist, append the last two lines from the following file to it:

```
```
$ cat /etc/procmailrc
DROPPRIVS=yes
:$0 fw
| /usr/bin/spamc
```
```

The first line of this file ensures that **procmail** runs with the least possible privileges. The next two lines implement a rule that pipes each user's incoming email through `spamc`. The `:$0` tells `procmail` that a rule follows. The `f` flag indicates a filter; the `w` flag causes `procmail` to wait for the filter to complete and check the exit code. The last line specifies that the `/usr/bin/spamc` utility will be used as the filter.

With this file in place, all email that the server system receives for local delivery passes through SpamAssassin, which rates it according to the options in the global configuration file. Users with accounts on the server system can override the global SpamAssassin configuration settings in their `~/.spamassassin/user_prefs` files.

When you run SpamAssassin on a server, you typically want to rate the email conservatively so that fewer pieces of good email are marked as spam. Setting `required_hits` in the range of 6\u201310 is generally appropriate. Also, you do not want to remove any email automatically because you could prevent a user from getting a piece of nonspam email. When the server marks email as possibly being spam, users can manually or automatically filter the spam and decide what to do with it.

# ## WEBMAIL

Traditionally you read email using a dedicated email client such as KMail. Recently it has become more common to use a Web application to read email. If you have an email account with a commercial provider such as Gmail, HotMail, or Yahoo! Mail, you use a Web browser to read email. Email read in this manner is called *Webmail*. Unlike email you read on a dedicated client, you can read Webmail from anywhere you can open a browser on the Internet: You can check your email from an Internet cafe or a friend's computer, for example.

SquirrelMail (`squirrelmail` package) provides Webmail services; the SquirrelMail files reside in `/usr/share/squirrelmail`. If you want to run SquirrelMail, you must run IMAP (page 689) because SquirrelMail uses IMAP to receive and authenticate email. You must also run Apache (Chapter 26) so a user can use a browser to connect to SquirrelMail.

SquirrelMail is modular: You can easily add functionality using plugins. There are plugins that allow you to share a calendar and plugins that give you the ability to change passwords using the Webmail interface. See the plugins section of the SquirrelMail Web site for more information.

Create the following link to make SquirrelMail accessible from the Web: