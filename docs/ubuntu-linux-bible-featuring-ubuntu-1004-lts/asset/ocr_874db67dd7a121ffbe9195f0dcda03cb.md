# Chapter 30: Setting Up a Mail Server

```
myhostname = ubuntu.vonhagen.org
alias_maps = hash:/etc/aliases
ialias_database = hash:/etc/aliases
myorigin = /etc/mailname
mydestination = mail.vonhagen.org, ubuntu.vonhagen.org,
localhost.vonhagen.org, localhost
relayhost = \mynetworks = 127.0.0.0/8 ::ffff:127:0:0.1/104
mailbox_size_limit = 0
recipient_delimiter = +
inet_interfaces = all
html_directory = /usr/share/doc/postfix/html
```

In order, these configuration variables do the following:

+   - myorigin: An option for Debian and derivative distributions (such as Ubuntu) enables you to use the first line of the text file /etc/mailname as the name of the mailer. This is actually later in the default file.
- smtpd_banner: Sets the value of the banner that is displayed when an SMTP connection is established. In this case, the banner is constructed by the value of other variables set in the configuration file.
- biff: Determines whether the local e-mail notification service (biff) should be used for each user with new mail that Postfix processes the incoming mail queue. In this case, it is disabled because biff notifications can cause a performance drain, and are relevant only on the machine that houses the mail files. Users who use local mail files can enable this for themselves.
- append_dot_mydomain: Determines whether Postfix should append a domain name to mail sent to user@host. Nowadays, this is usually handled by the MUA, so it is disabled.
- delay_warning_time: Uncommenting this parameter would specify the period of time after which users would be notified if mail they sent had not yet been delivered. After all, the remote site could be using Microsoft Exchange, and might be down.
- smtpd_tls_cert_file: Identifies the full pathname of the file on this system that holds the certificate used by this machine when sending messages using TLS (Transport Layer Security).
- smtpd_tls_key_file: Identifies the full pathname of the file on this system that holds the RSA private key for the Postfix SMTP client when sending messages using TLS (Transport Layer Security).
- smtpd_use_tls: Determines whether this Postfix server should use TLS when a remote SMTP server announces STARTTLS support. If the remote server does not announce STARTTLS support, the message is sent in the clear.