# SuSE System Administration
PART III

With the man procmail* pages, serious study of procmail starts with the page
http://www.faqs.org/faqs/mail/filtering-faq, Nancy McGough's Filtering Mail
FAQ. This gives detailed installation and debugging directions. You'll also find information
about procmail in the Mail-HOWTO, found under the /usr/doc/howto/en directory.
Because your SuSE Linux machine will almost certainly have a correctly configured
procmail, you can immediately begin to program your personal use of it. As a first
experiment, create these files: -/.procmailrc, with these contents:

+   VERBOSE=on
MAILDIR=$HOME/mail
SPAMDIR=$HOME/.procmail
LOGFILE=$SPAMDIR/log
INCLUDER=$SPAMDIR/rc.testing

-/.procmail/rc.testing, holding this code:

+   :0:
* Subject:.*HOT
SPAM.HOT

-./forward, with this:

```
"!IFS=" & & exec /usr/bin/procmail -f !! exec 75 #YOUR_EMAIL_NAME
```

After you create these three, set necessary permissions with the following:

```
# chmod 644 -./forward
# chmod ax -./
```

Now exercise your filter with the following:

```
# echo "This message 1." ! mail -s "Example of HOT SPAM." YOUR_EMAIL_NAME
# echo "This message 2." ! mail -s "Desired message." YOUR_EMAIL_NAME
```

What you now see in your mailbox is only one new item: the one with the subject Desired
message . You also have a new file in your home directory, SPAM.HOT, holding the first
message.

procmail is a robust, flexible utility that you program to achieve even more useful
automations than this. When you gain familiarity with it, it will become natural to construct
rules that, for example, automatically discard obvious spam, sort incoming mailing-list
traffic, and perhaps even implement peter forwarding, remote system monitoring, or FAQ
responding. This can save you considerable time each day.