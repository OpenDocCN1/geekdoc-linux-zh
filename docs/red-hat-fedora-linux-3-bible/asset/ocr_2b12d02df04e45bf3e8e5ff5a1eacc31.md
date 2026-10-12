> NOTE: Although the procedure here describes how to use SpamAssassin from the RPM package that comes with the latest version of Fedora, many people get their version of SpamAssassin directly from the SpamAssassin.org Web site. Because anti-spam software is evolving so quickly (to keep ahead of spammers), some people like to make sure they have the very latest software.

# Setting up SpamAssassin on your mail server

Here’s a quick procedure for enabling SpamAssassin and having your users choose what to do with spam messages that are encountered:

+   1. Configure your mail transport agent (sendmail or postfix) to use the procmail command as its mailer. For sendmail, it is already configured as the default mailer, based on the following line in the /etc/mail/sendmail.mc file:

```
FEATURE(local_procmail,``',procmail -t -Y -a $h -d $u')dn:
```

+   2. Make sure that the SpamAssassin spamd daemon is running (it should already be on for run levels 2-5), and if it isn’t, start it by typing the following (as root user):

```
# chkconfig --list spamassassin
spamassassin 0:off 1:off 2:on 3:on 4:on 5:on 6:off
# chkconfig spamassassin on
```

+   3. Create an /etc/procmail.rc file (using any text editor, as root user). This procmail.rc file example pipes all mail messages received by procmail through spampc (which is the client side of the spamd daemon turned on in the previous step):

```
:0w
| /usr/bin/spampc
```

If you like, you can do a lot more in the procmail.rc file to deal with spam on a system-wide basis. You could, for example, create procmail recipes that take reported spam e-mail messages and sort them into a system-wide spam folder or deletes them completely. Likewise, each user can create an individual $HOME/.procmail.rc file to create personal procmail recipes. (Type man procmailex for examples of rules in a procmail.rc file.)

+   4. Check the /etc/mail/spamassassin/local.cf file. This file contains rules that are used system-wide by SpamAssassin, unless they are overridden by a user’s individual $HOME/.spamassassin/user_prefs file. Here are the contents of the local.cf file:

```
required_hits 5
rewrite_subject 1
subject_tag [SPAM]
report_safe 0
```