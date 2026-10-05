# SMTP and Protocols
CHAPTER 9

The first copy backs up your current sendmail configuration in case you need to get it back for any reason. You can then stop and start sendmail or find the process ID and send it a HUP signal. This causes sendmail to reread its configuration file:

```
[root@gonzo]# /etc/rc.d/init.d/sendmail stop
[root@gonzo]# /etc/rc.d/init.d/sendmail start
```

# Common sendmail Configuration Mistakes

There are three main common configuration errors when you are setting up a sendmail based mail server.

The first is not having an alias for the postmaster user. All bounced messages sent to this alias, which should point to a user who regularly reads his mail. When you bounced messages for your site, you should read *them*! Most of the time it helps you diagnose a problem before the users notice it and start complaining. It is also a widely known alias that Internet users commonly mail to if they need to contact an email administrator for a particular domain name.

The second is having an incorrectly configured sendmail.cw file. This file should list all the domain names for which the server is responsible for receiving mail.

The third is due to incorrectly configured DNS entries. Most of the time have incorrect secondary MX records, which is of no use if your main mail server goes down for a period of time. Usually your ISP will be happy to act as a secondary MX for your site.

# POP

As much as you love Linux, the reality is that you must contend with other operating systems out there. Even worse, many of them aren't even UNIX-based. Although the Linux community has forgiven the users of other operating systems, there is still a long way to go before complete assimilation happens. In the meantime, the best thing that can happen is to use tools to tie the worlds together.

The following sections cover the integration of the most-used application of any network: electronic mail (or email for short). Because UNIX and other operating systems have very different views of how email should be handled, the Post Office Protocol (POP) was created. This protocol abstracts the details of mail to a system-independent level so anyone who writes a POP client can communicate with a POP server.