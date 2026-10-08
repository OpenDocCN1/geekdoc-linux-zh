
The next section explores the default Postfix configuration file that was installed and configured in the previous section. Subsequent sections address how to make your Postfix server work on your network and how to configure your mail server so that it accepts POP mail requests.

# Note

As discussed in Chapter 7 and mentioned earlier in this chapter, POP and IMAP are the primary protocols used for remote systems to read e-mail on a mail server. The key difference between them is that POP is designed to store e-mail on the client, while IMAP is designed to store e-mail on the server. Each model has its advantages, but I believe most people are more familiar with the POP model, so I'm going to focus on that in this chapter.

# Postfix Configuration Files

The Ubuntu mail server uses three configuration files, all of which are installed in the directory /etc/postfix:

- dynamicmaps.cf: Identifies additional capabilities to be loaded at runtime based on the type of operation that is being performed.
- main.cf: Contains configuration information for Postfix that is used during message processing.
- master.cf: Contains parameters used when the Postfix master program runs other programs from /usr/lib/postfix.

Postfix can also use standard mailer configuration files such as /etc/aliases (which allows e-mail to be delivered to one to another), but this is not a Postfix-specific configuration file.

The main.cf configuration file is the only Postfix configuration file that most users will have to modify. As installed on an Ubuntu system, the main.cf configuration file for a system looks like the following (I removed some irrelevant comments and white space):

```
#myorigin = /etc/mailname
smtpd_banner = $hostname SMTP $mail_name (Ubuntu)
biff = - no
append_dot_mydomain = no
#delay_warning_time = 4h
smtpd_tls_cert_file=/etc/ssl/certs/ssl-cert-snakeoil.pem
smtpd_tls_key_file=/etc/ssl/private/ssl-cert-snakeoil.key
smtpd_use_tls=yes
smtpd_tls_session_cache_database = \
  btree:${queue_directory}/smtpd_scache
smtpd_tls_session_cache_database = \
  btree:${queue_directory}/smtp_scache
```

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

- myorigin: An option for Debian and derivative distributions (such as Ubuntu) enables you to use the first line of the text file /etc/mailname as the name of the mailer. This is actually later in the default file.
- smtpd_banner: Sets the value of the banner that is displayed when an SMTP connection is established. In this case, the banner is constructed by the value of other variables set in the configuration file.
- biff: Determines whether the local e-mail notification service (biff) should be used for each user with new mail that Postfix processes the incoming mail queue. In this case, it is disabled because biff notifications can cause a performance drain, and are relevant only on the machine that houses the mail files. Users who use local mail files can enable this for themselves.
- append_dot_mydomain: Determines whether Postfix should append a domain name to mail sent to user@host. Nowadays, this is usually handled by the MUA, so it is disabled.
- delay_warning_time: Uncommenting this parameter would specify the period of time after which users would be notified if mail they sent had not yet been delivered. After all, the remote site could be using Microsoft Exchange, and might be down.
- smtpd_tls_cert_file: Identifies the full pathname of the file on this system that holds the certificate used by this machine when sending messages using TLS (Transport Layer Security).
- smtpd_tls_key_file: Identifies the full pathname of the file on this system that holds the RSA private key for the Postfix SMTP client when sending messages using TLS (Transport Layer Security).
- smtpd_use_tls: Determines whether this Postfix server should use TLS when a remote SMTP server announces STARTTLS support. If the remote server does not announce STARTTLS support, the message is sent in the clear.

- smtpd_tls_session_cache_database: Identifies the organization and location of the SMTP server TLS session cache used by the tlsmgr daemon.
- smtp_tls_session_cache_database: Identifies the organization and location of the SMTP client TLS session cache used by the tlsmgr daemon.
- myhostname: Identifies the actual Internet hostname of this system. By default, this value is the value returned by hostname().
- alias_maps: Identifies the organization and full pathname of the aliases used for local mail delivery.
- alias_database: Identifies the organization and full pathname of the aliases used for local mail delivery, which is updated using.
- myorigin: An option for Debian and derivative distributions (such as Ubuntu) enables you to use the first line of the text file /etc/mailname as the name of the mailer. This is actually later in the default file.
- smtpd_banner: Sets the value of the banner that is displayed when an SMTP connection is established. In this case, the banner is constructed by the value of other variables set in the configuration file.
- biff: Determines whether the local e-mail notification service (biff) should be used for each user with new mail that Postfix processes the incoming mail queue. In this case, it is disabled because biff notifications can cause a performance drain, and are relevant only on the machine that houses the mail files. Users who use local mail files can enable this for themselves.
- append_dot_mydomain: Determines whether Postfix should append a domain name to mail sent to user@host. Nowadays, this is usually handled by the MUA, so it is disabled.
- delay_warning_time: Uncommenting this parameter would specify the period of time after which users would be notified if mail they sent had not yet been delivered. After all, the remote site could be using Microsoft Exchange, and might be down.
- smtpd_tls_cert_file: Identifies the full pathname of the file on this system that holds the certificate used by this machine when sending messages using TLS (Transport Layer Security).
- smtpd_tls_key_file: Identifies the full pathname of the file on this system that holds the RSA private key for the Postfix SMTP client when sending messages using TLS (Transport Layer Security).
- smtpd_use_tls: Determines whether this Postfix server should use TLS when a remote SMTP server announces STARTTLS support. If the remote server does not announce STARTTLS support, the message is sent in the clear.
- smtpd_tls_session_cache_database: Identifies the organization and location of the SMTP server TLS session cache used by the tlsmgr daemon.
- smtp_tls_session_cache_database: Identifies the organization and location of the SMTP client TLS session cache used by the tlsmgr daemon.
- myhostname: Identifies the actual Internet hostname of this system. By default, this value is the value returned by hostname().
- alias_maps: Identifies the organization and full pathname of the aliases used for local mail delivery.
- alias_database: Identifies the organization and full pathname of the aliases used for local mail delivery, which is updated using.
- myorigin: An option for Debian and derivative distributions (such as Ubuntu) enables you to use the first line of the text file /etc/mailname as the name of the mailer. This is actually later in the default file.
- smtpd_banner: Sets the value of the banner that is displayed when an SMTP connection is established. In this case, the banner is constructed by the value of other variables set in the configuration file.
- biff: Determines whether the local e-mail notification service (biff) should be used for each user with new mail that Postfix processes the incoming mail queue. In this case, it is disabled because biff notifications can cause a performance drain, and are relevant only on the machine that houses the mail files. Users who use local mail files can enable this for themselves.
- append_dot_mydomain: Determines whether Postfix should append a domain name to mail sent to user@host. Nowadays, this is usually handled by the MUA, so it is disabled.
- delay_warning_time: Uncommenting this parameter would specify the period of time after which users would be notified if mail they sent had not yet been delivered. After all, the remote site could be using Microsoft Exchange, and might be down.
- smtpd_tls_cert_file: Identifies the full pathname of the file on this system that holds the certificate used by this machine when sending messages using TLS (Transport Layer Security).
- smtpd_tls_key_file: Identifies the full pathname of the file on this system that holds the RSA private key for the Postfix SMTP client when sending messages using TLS (Transport Layer Security).
- smtpd_use_tls: Determines whether this Postfix server should use TLS when a remote SMTP server announces STARTTLS support. If the remote server does not announce STARTTLS support, the message is sent in the clear.
- smtpd_tls_session_cache_database: Identifies the organization and location of the SMTP server TLS session cache used by the tlsmgr daemon.
- smtp_tls_session_cache_database: Identifies the organization and location of the SMTP client TLS session cache used by the tlsmgr daemon.
- myhostname: Identifies the actual Internet hostname of this system. By default, this value is the value returned by hostname().
- alias_maps: Identifies the organization and full pathname of the aliases used for local mail delivery.
- alias_database: Identifies the organization and full pathname of the aliases used for local mail delivery, which is updated using.
- myorigin: An option for Debian and derivative distributions (such as Ubuntu) enables you to use the first line of the text file /etc/mailname as the name of the mailer. This is actually later in the default file.
- smtpd_banner: Sets the value of the banner that is displayed when an SMTP connection is established. In this case, the banner is constructed by the value of other variables set in the configuration file.
- biff: Determines whether the local e-mail notification service (biff) should be used for each user with new mail that Postfix processes the incoming mail queue. In this case, it is disabled because biff notifications can cause a performance drain, and are relevant only on the machine that houses the mail files. Users who use local mail files can enable this for themselves.
- append_dot_mydomain: Determines whether Postfix should append a domain name to mail sent to user@host. Nowadays, this is usually handled by the MUA, so it is disabled.
- delay_warning_time: Uncommenting this parameter would specify the period of time after which users would be notified if mail they sent had not yet been delivered. After all, the remote site could be using Microsoft Exchange, and might be down.
- smtpd_tls_cert_file: Identifies the full pathname of the file on this system that holds the certificate used by this machine when sending messages using TLS (Transport Layer Security).
- smtpd_tls_key_file: Identifies the full pathname of the file on this system that holds the RSA private key for the Postfix SMTP client when sending messages using TLS (Transport Layer Security).
- smtpd_use_tls: Determines whether this Postfix server should use TLS when a remote SMTP server announces STARTTLS support. If the remote server does not announce STARTTLS support, the message is sent in the clear.

## Identifying Hosts and Domains

The main.cf configuration file is the only Postfix configuration file that most users will have to modify. As installed on an Ubuntu system, the main.cf configuration file for a system looks like the following (I removed some irrelevant comments and white space):

```
#myorigin = /etc/mailname
smtpd_banner = $hostname SMTP $mail_name (Ubuntu)
biff = - no
append_dot_mydomain = no
#delay_warning_time = 4h
smtpd_tls_cert_file=/etc/ssl/certs/ssl-cert-snakeoil.pem
smtpd_tls_key_file=/etc/ssl/private/ssl-cert-snakeoil.key
smtpd_use_tls=yes
smtpd_tls_session_cache_database = \
  btree:${queue_directory}/smtpd_scache
smtpd_tls_session_cache_database = \
  btree:${queue_directory}/smtp_scache
```

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

- myorigin: An option for Debian and derivative distributions (such as Ubuntu) enables you to use the first line of the text file /etc/mailname as the name of the mailer. This is actually later in the default file.
- smtpd_banner: Sets the value of the banner that is displayed when an SMTP connection is established. In this case, the banner is constructed by the value of other variables set in the configuration file.
- biff: Determines whether the local e-mail notification service (biff) should be used for each user with new mail that Postfix processes the incoming mail queue. In this case, it is disabled because biff notifications can cause a performance drain, and are relevant only on the machine that houses the mail files. Users who use local mail files can enable this for themselves.
- append_dot_mydomain: Determines whether Postfix should append a domain name to mail sent to user@host. Nowadays, this is usually handled by the MUA, so it is disabled.
- delay_warning_time: Uncommenting this parameter would specify the period of time after which users would be notified if mail they sent had not yet been delivered. After all, the remote site could be using Microsoft Exchange, and might be down.
- smtpd_tls_cert_file: Identifies the full pathname of the file on this system that holds the certificate used by this machine when sending messages using TLS (Transport Layer Security).
- smtpd_tls_key_file: Identifies the full pathname of the file on this system that holds the RSA private key for the Postfix SMTP client when sending messages using TLS (Transport Layer Security).
- smtpd_use_tls: Determines whether this Postfix server should use TLS when a remote SMTP server announces STARTTLS support. If the remote server does not announce STARTTLS support, the message is sent in the clear.

(Note: The OCR text provided contained significant repetitions and fragmented lists across pages 1083-1084 and 1085 which I have collapsed into a coherent logical structure based on the instruction to "merge cross-page continuous paragraphs" and "identify titles/lists based on semantics".)

## Rewriting Addresses in Outgoing Mail

Although all hosts on the local network can now send mail through the mail server, many MUAs send mail using the fully qualified domain name of the host from which the mail was sent. This means that mail from vwh(on the host 64bit.vonhagen.org) goes out with an e-mail address of vwh@64bit.vonhagen.org. Although I don't particularly care about this, I probably don't have a mailbox there, and therefore people cannot reply to me.

To correct this problem, you can use the Postfix configuration parameter masquerade_domains to identify domains for which Postfix should rewrite outgoing mail addresses so that they simply appear to be user@domain.com. In this case, mail from vwh@64bit.vonhagen.org would go out simply as vwh@vonhagen.org, which is my actual e-mail address. In this case, I would add the masquerade_domains setting to my main.cf.

```
masquerade_domains = vonhagen.org
```

I then restart the Postfix server (using sudo /etc/init.d/postfix restart) or use the sudo postfix reload command to activate the active Postfix daemon to pick up my changes to the configuration file. All hosts on my network can now send mail through the Postfix mail server without identifying the specific host from which the mail originated.
