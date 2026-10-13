```
# chmod go-w /etc/mail/usr /var /var/spool /var/spool/mqueue
```

To check whether you have file or directory permission problems, run sendmail as follows:

```
# sendmail -v -bi
```

sendmail will attempt to initialize the aliases database. If you see errors similar to the following then you have incorrect directory and file permissions set and you need to fix the problem to ensure maximum security of your sendmail system:

```
WARNING: writable directory /etc
WARNING: writable directory /usr/spool/mqueue
```

# USING WILDCARD MAIL EXCHANGERS FOR YOUR DOMAIN

While it is technically possible to define wildcard mail exchangers for your domain in your DNS records, this should be avoided if at all possible. By using wildcards to define the hostnames or IP addresses of mail exchangers, several problems arise. In particular, it is possible for mail to invalid hosts within your domain to be delivered to your mail servers. You may see errors such as MX list for hostname somehost points back to somehost or config error: mail loops back to myself in bounced messages sent back to senders of incoming emails.

# OTHER MAIL RELAYING PROBLEMS

You may see bounce errors such as the following:

```
553 MX list for do.main points back to relay.do.main
554 <user@do.main>... Local configuration error
```

This means you have set up an MX record for mail to do.main, which points to the host relay.do.main. However, the relaying machine does not have do.main specified as a legal domain for which it relays mail. Add do.main in /etc/mail/relay-domains and restart sendmail to fix this problem.