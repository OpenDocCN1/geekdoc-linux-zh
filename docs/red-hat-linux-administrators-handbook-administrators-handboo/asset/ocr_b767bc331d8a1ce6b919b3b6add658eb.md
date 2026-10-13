# Rerouting mail for domains using /etc/mail/mailertable

This configuration file can be used to create a database to override default mail routing for certain domains. The format of this file is as follows:

```
source-domain mailer:replacement-domain or user@host
```

For example:

```
visitor-01.mydomain.com local:visitor1
```

When mail for visitor-01.mydomain.com arrives, it is rerouted to local user visitor1. One can use only the mailers that are specified in the /etc/sendmail.cf file using an M line. A quick look in the /etc/sendmail.cf file shows qmtp, procmail, smtp, esmtp, smtp8, relay, usenet, uucp, uucp-ol, suucp, uucp-new, uucp-om, uucp-u uom, local, and prog to be defined as mailers.

You can also specify partial domain names as the source domain name. In the following example, mail for *.mydomain.com hosts will be relayed to mail-hub.mydomain.com via the SMTP mailer:

```
.mydomain.com smtp:mail-hub.mydomain.com
```

![](bbox=[0.1, 0.84, 0.17, 0.93])

# Caution

You must have the appropriate MX record for the source domain or else mail will never be delivered.

Consider another example, wherein all mail for ad-engine.com will be delivered to user kabir@integrationlogic.com via the SMTP mailer as long as ad-engine.com is listed in the /etc/sendmail.cw file:

```
ad-engine.com smtp:kabir@integrationlogic.com
```

Sendmail does not directly use the /etc/mail/mailertable configuration file. It uses a DBM database version of the file. To create the necessary DBM file for your /etc/mail/mailertable file, run the following command:

```
makemap hash /etc/mail/mailertable < /etc/mail/mailertable
```