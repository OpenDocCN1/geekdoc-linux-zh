# Setting up local delivery destinations:
/etc/mail/sendmail.cw

Use this file to specify the names of hosts and domains for which the sendmail server will receive e-mail. An example of this file is shown here:

niotec.com
ad-engine.com
classedrew.com

Each line specifies a domain name that the sendmail server will service.

# Creating virtual mail servers using /etc/mail/ virtusertable

To provide mail support for multiple domains, set up virtual mail service using sendmail. For example, to provide virtual mail service for a domain called yourclient.com, do the following:

+   1. Add the domain (yourclient.com) in the /etc/mail/sendmail.cw file so that sendmail will accept mail for this host.
+   2. Add the domain (yourclient.com) in the /etc/mail/relay-domains file so that sendmail will relay messages for this domain.

To map the virtual domain users to one or more local accounts, use the /etc/mail/virtusertable file as follows:

```
virtual e-mail address    real e-mail address
```

Here are some examples:

```
webmaster@yourclient.com    mike
mike@yourclient.com        mike
info@yourclient.com        jason
jason@yourclient.com       jason
```

In these examples, e-mail for virtual e-mail addresses such as webmaster@yourclient.com and mike@yourclient.com goes to local user mike; similarly, mail for info@yourclient.com and jason@yourclient.com goes to another local user, jason. This provides yourclient.com with a mail server it didn't have. To the rest of the world, yourclient.com appears to