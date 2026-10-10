Because open relays are such a threat, you should explicitly check for them. Review your access file and look for any option with the word relay in the m4 configuration file. You can also use services that will connect to your mail server and attempt to relay mail as a way of testing your system, then give you a report of the results. One of these is hosted at http://www.abuse.net/relay.html. Be careful, though—it’s conceivable that a spammer somewhere has set up such a service as a way of locating open relays to abuse, so you should only use a trusted service.

# ### Outgoing Relay Configuration

Many Linux mail servers, particularly on workstations and small networks, should be configured to use an outgoing mail relay, aka a smart relay. This is the case for the workstations described in this task’s scenario. To configure these systems to use Pangaea University’s main mail server for outgoing mail, enable outgoing relaying in the workstations’ m4 files:

```
FEATURE(`nullclient`, `mail.pangaea.edu`)
```

In reality, you would change mail.pangaea.edu to the hostname of the computer that should relay the mail. You should also remove or comment out two other lines, if they’re present:

```
MAILER(local)dn1
MAILER(smtp)dn1
```

Another way to make similar changes is to use the SMART_HOST feature:

```
define(`SMART_HOST', `mail.pangaea.edu`)
```

The difference between the two is that the nullclient method is intended for very simple configurations that contain few other options. A workstation that should send all its email via the outgoing relay might use this option. SMART_HOST, by contrast, can be used in more complex configurations in which some mail remains local and some is relayed.

When you’ve made these changes, rebuild sendmail.cf, and restarted or reloaded sendmail, the server should send all non-local mail to the specified mail server. This is handy if your ISP blocks direct outgoing SMTP connections (as many home-oriented ISPs do as an anti-spam measure) or if you want your organization’s mail to be filtered through a single powerful mail server system.

# ### Criteria for Completion

To complete this task, you should have configured one mail server to accept mail for two entire domains (pangaea.edu and mesozoic.edu). You should also have adjusted the server to redirect mail for postmaster (and, perhaps, some other addresses) to specific local users of your choice. Finally, you should have configured at least one other system’s sendmail configuration to direct its mail through the first one. These options can be tricky to implement, so be sure to test them by sending and reading mail using local mail clients such as mutt or KMail.