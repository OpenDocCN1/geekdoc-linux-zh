# CHAPTER 19 Simple Mail Transfer Protocol (SMTP) 509

> > If you do not set the $mynworks variable correctly and spammers using your mail server as a relay, you will quickly find a surge of angry mail administrators e-mailing you about it. Furthermore, it is a fast way to get your mail server blacklisted by one of the spam techniques, such as a DNS Blacklist (DNSBL) or Realtime Blackhole List (RBL). Once your server is blacklisted, very few people will be able to receive mail from you, and you will need to jump through a lot of hoops to get it. Worse, no one will tell you that you have been blacklisted.

# smtpd_banner

This variable allows you to return a custom response when a client connects to your mail server. It is a good idea to change the banner to something that doesn't give away what mail server you are using. This just adds one more slight hurdle for hackers trying to find faults in your specific software version.

```
smtpd_banner = $hostname ESMTP
```

# inet_protocols

This parameter is used to invoke the Internet Protocol Version 6 (IPv6) capabilities of the Postfix mail server. It is used to specify the Internet protocol version that Postfix will use when making or accepting connections. Its default value is ipv4. Setting this value to ipv6 will make Postfix support IPv6. Here are some example values that the parameter_accepts:

```
inet_protocols = ipv4 (DEFAULT)
inet_protocols = ipv4, ipv6
inet_protocols = all
inet_protocols = ipv6
```

Tons of other parameters in the Postfix configuration file are not discussed here. You might see them commented out in the configuration file when you set the preceding options. These other options will allow you to set security levels and debugging levels, among other things, as required.

Now let's move to running the Postfix mail system and maintaining your mail server.

# Checking Your Configuration

Postfix includes a nice tool for checking a current configuration and helping you troubleshoot it. Simply run the following:

```
[root@server ~]# postfix check
```