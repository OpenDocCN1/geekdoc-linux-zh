
## Table 9-2 Configuration Options for the /etc/mail/access Database

| Option | Description |
|---|---|
| OK | Accept mail even if other configuration rules want to reject mail from the specified host or the user. |
| RELAY | Act as an SMTP mail relay for the specified host. In other words, accept mail intended for users on the specified domain and also allow users on the specified domain to send mail via the server. Don't reject mail from the specified domain even if other rules want to do so. |
| REJECT | Reject all (incoming/outgoing) mail for the specified domain. |
| DISCARD | Discard the message completely by using the $#discard mailer. Discarded messages are accepted but silently undelivered so that the sender thinks they have been delivered. |
| 501 <message> | Do not accept mail if the sender address partially or fully matches the specified user@host. |
| 553 <message> | Do not accept mail if the sender address does not contain host name. |
| 550 <message> | Do not accept mail for specified domain name. |

Here is an example /etc/mail/access configuration:

```
any-spam-maker.com    REJECT
client-domain.com     RELAY
annoying-company.com  DISCARD
dumbguy@dumb-net.com  501 You can't use this mail server.
```

All mail from any-spam-maker.com will be rejected; all incoming and outgoing mail to and from client-domain.com will be relayed; all mail from annoying-company.com will be accepted but silently discarded; and all mail from dumbguy@dumb-net.com will be rejected with the "You can't use this mail server." message.

Note that sendmail does not directly use the /etc/mail/access configuration file. It uses a DBM database version of the file. To create the necessary DBM file for your /etc/mail/access file, run the following command:

```
makemap hash /etc/mail/access < /etc/mail/access
```

This creates the necessary DBM database file (such as /etc/mail/access.db) in the same directory. You don't need to restart the sendmail daemon after you modify this file.

## Creating aliases for users using /etc/mail/aliases

This configuration file enables you to create an alias database for users. For example, suppose that you want to create an alias called carol.godsave for a user called carol. You can do so by using this configuration file, which has the following format:

```
alias name: comma-separated list of users
```

To create the carol.godsave alias, add a line in this configuration file as follows:

```
carol.godsave: carol
```

When sendmail receives mail for carol.godsave@yourdomain.com, it will be delivered to the carol account on your mail server.

One of the really useful uses of aliases is to create local groups. For example,

```
web-developers: keith, cynthia, jason
```

defines an alias web-developers, which can be used to send e-mail messages to the specified users.

The default /etc/mail/aliases file already contains a set of default aliases that you can change as you see fit. Also note that if you have a user with the same name as an alias, the e-mail will be sent to the user(s) specified in the alias. Here is an example of such an alias:

```
root: kabir
```

When mail is sent to root@nitec.com, even though a user account called root exists on the mail server, the mail will still be sent to user kabir. You can also chain aliases. In the following example, alias root resolves to alias kabir, which resolves to mohammed:

```
root: kabir
kabir: mohammed
```

So, mail sent to root@localhost on my system can go to the mailbox of a user called mohammed.

Sendmail does not directly use the /etc/mail/aliases configuration file. It uses a DBM database version of the file. To create the necessary DBM file for your /etc/mail/aliases file, run the following command:

```
newaliases
```

This creates the necessary DBM database file (such as /etc/mail/aliases.db) in the same directory. You don't need to restart the sendmail daemon when you modify this file.

![](img/c2419364ebb911c809b6a79991707c27_223_0.png)

### TIP
Running newaliases is equivalent to running the sendmail -bi command.

## Mapping domains using /etc/mail/domaintable

This configuration file can be used to create a domain name mapping database, such as the following, which maps yet-another-domain.com to yourdomain.com:

```
Yet-another-domain.com yourdomain.com
```

So, when mail is received for user@yet-another-domain.com, it is translated to user@yourdomain.com. The destination domain (yourdomain.com) must be a fully qualified domain name. Also, the domain mapping in the domain table is reflected into headers; that is, this is done in ruleset 3.

Sendmail does not directly use the /etc/mail/domaintable configuration file. It uses a DBM database version of the file. To create the necessary DBM file for your /etc/mail/domaintable file, run the following command:

```
makemap hash /etc/mail/domaintable < /etc/mail/domaintable
```

This creates the necessary DBM database file (such as /etc/mail/domaintable.db) in the same directory. You do not need to restart the sendmail daemon when you modify this file.

## Rerouting mail for domains using /etc/mail/mailertable

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

![](img/c2419364ebb911c809b6a79991707c27_224_0.png)

### Caution
You must have the appropriate MX record for the source domain or else mail will never be delivered.

Consider another example, wherein all mail for ad-engine.com will be delivered to user kabir@integrationlogic.com via the SMTP mailer as long as ad-engine.com is listed in the /etc/sendmail.cw file:

```
ad-engine.com smtp:kabir@integrationlogic.com
```

Sendmail does not directly use the /etc/mail/mailertable configuration file. It uses a DBM database version of the file. To create the necessary DBM file for your /etc/mail/mailertable file, run the following command:

```
makemap hash /etc/mail/mailertable < /etc/mail/mailertable
```

This creates the necessary DBM database file (for instance, /etc/mail/mailertable.db) in the same directory. You do not need to restart the sendmail daemon when you modify this file.

## Setting up mail relays using /etc/mail/relay-domains

The latest version of sendmail (v 8.9.x), by default, denies unauthorized relaying of mail. In other words, if sendmail is not explicitly told to accept mail destined for another domain, it refuses to do so. For example, suppose that you run the latest version of sendmail on a host called mail.mydomain.com. If an unauthorized user tries to use mail.mydomain.com to deliver mail to another SMTP server, your sendmail server will refuse such requests, by default. This is done to eliminate mail relay abuse by people who send unsolicited e-mail messages.

To allow legitimate domains to use your sendmail server as a relay, you must specify them in this file. Add your own domain and any other friendly domains for which you want to allow relay operation. For example:

```
nitec.com
integrationlogic.com
ad-engine.com
```

You can also use IP addresses in the form of a network address or a full IP.

To test the relay configuration, run the following command:

```
echo '$=R' | sendmail -bt
```

This should display all the allowed domains.

## Setting up local delivery destinations: /etc/mail/sendmail.cw

Use this file to specify the names of hosts and domains for which the sendmail server will receive e-mail. An example of this file is shown here:

```
nitec.com
ad-engine.com
classifiedworks.com
```

Each line specifies a domain name that the sendmail server will service.
