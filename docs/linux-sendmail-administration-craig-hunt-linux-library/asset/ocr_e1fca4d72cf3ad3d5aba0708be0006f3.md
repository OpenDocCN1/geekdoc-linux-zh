# The Cr, Cw, and Ct Files 145

Unlike the "ct" file, which is never used, the "cr" file is used. The "cr" file is really named the relay-domains file. Sendmail always uses the data it finds in the relay-domains file. The purpose and structure of that file is the next topic.

# The relay-domains File

When mail arrives at a Sendmail server, it is either accepted, rejected, or relayed. If it is addressed to the server itself, by any name that the server accepts as its own, the mail is accepted for local delivery, meaning that the mail is placed in the mailbox of a local user or routed as one of the Sendmail databases. If the mail is not addressed to the server itself, the mail is either rejected or relayed. Mail is relayed by re-sending it to the delivery address. Prior to Sendmail 8.9, all addressed to another host that received by a Sendmail server was relayed. Now, no mail is relayed unless you explicitly tell Sendmail to relay it. This was a big headache for many system administrators who were using a Sendmail server to relay outbound mail for their PCs. But the change was necessary. Spammers were exploiting the relay feature of Sendmail to hide the source of spam. Now all administrators must pay the price of spam, and that is the extra work necessary to create an explicit relay configuration.

![](bbox=[0.936, 0.283, 0.981, 0.365])

One way to explicitly enable decaying is to list the names of hosts allowed to relay mail in the /etc/mail/relay-domains file. Sendmail copies anything written in that file to the class variable R. Any host listed in class R is allowed to relay mail. Listing 6.2 shows the contents of a simple relay-domains file.

# Listing 6.2 Using the relay-domains File

```
[root]# cat /etc/mail/relay-domains
ibis.foobirds.org
[root]# ps -ax | grep sendmail
542 ?  S  0:00 sendmail: accepting connections
[root]# kill -HUP 542
[root]# sendmail -bt
ADDRESS TEST MODE (ruleset 3 NOT automatically invoked)
ter <ruleset> <address>
=$R
ibis.foobirds.org
> ^D
```

AIGHUP signal is passed to the Sendmail process to ensure that it reaches the hostnames from relay-domains into class R. The test in Listing 6.2 shows that class R was fully modified.