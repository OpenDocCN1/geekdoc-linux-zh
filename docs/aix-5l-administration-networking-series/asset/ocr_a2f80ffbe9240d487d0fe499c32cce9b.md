The second type of mail header is the RFC 822 header. It is used by both the MTA and the MUA. The RFC 822 header identifies the path the mail message has traveled, date, originator, recipients, subject, and so on.

```
```
Received: from gateway.wine.edu
          by hub.wine.edu id AA03037;
          Sun, 10 Nov 02 15:07 PST
Received: from smtp.whiskey.edu
          by mail.wine.edu id AA10255;
          Sun, 10 Nov 02 15:04 PST
Received: from english.whiskey.edu
          by smtp.whiskey.edu id AA12242;
          Sun, 10 Nov 02 15:01 PST
Date: Sun, 10 Nov 02 14:59:10 PST
From: raphael@english.whiskey.edu
To: rachel@wine.edu
Subject: Meeting Wednesday
Raphael:

I enjoyed that seminar last Wednesday. What was
the name of that professor who kept falling asleep?
Raphael
```
```

The ordering of the received lines indicates the MTA path that the mail message has traveled. This path can be used to debug routing problems and loops.

# ## How Mail Is Sent

When a user compose a mail message, the MUA attaches a header envelope to the message separated by a blank line. The MUA then hands the message off to the **sendmail** MTA. A new **sendmail** daemon is forked to process the new message. It passes each of the addresses associated with the mail message through address translation rule sets. The rule sets parse the address line and determine whether the message destination is local or remote. If the message is destined for a remote site, a name service may be queried to determine whether a preferred mail exchange site is requested for the remote site (name service MX record). If the remote site is running a **sendmail** MTA, the message is transferred to the remote site using the SMTP protocol described previously. At the remote site, **sendmail** runs the addresses through the rulesets again to determine whether the recipient is local or remote. If the recipient is local, the headers are rewritten and the message is spooled to the recipient's mail inbox.

# ## A Verbose /usr/bin/mail Session

The simplest way to test **sendmail** is to use the -v verbose flag with /usr/bin/mail. It provides feedback on the interaction between MTAs. The following example also uses the -s option to include a subject heading: