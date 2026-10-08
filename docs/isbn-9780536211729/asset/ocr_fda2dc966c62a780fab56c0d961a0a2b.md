# Enabling Common TCP Services

fi

```
$IPT-A INPUT -i $INTERNET -p tcp \\n--sport $UNPRIVORTS \\n-d $IPADDR --dport 25 -j ACCEPT
```

```
$IPT-A OUTPUT -o $INTERNET -p tcp ! --syn \\n-s $IPADDR --sport 25 \\n--dport $UNPRIVORTS -j ACCEPT
```

# SENDING MAIL AS AN SMTP SERVER AND RECEIVING MAIL\nAS AN SMTP SERVER

If you are sending mail as an SMTP server and are receiving mail as an SMTP server, you provide all your own mail services. Your local sendmail daemon is configured to relay outgoing mail to the destination hosts, as well as collect and delivering mail:

```
if [ "$CONNECTION_TRACKING" = "1" ]; then\n$IPT-A OUTPUT -o $INTERNET -p tcp \\n-s $IPADDR --sport $UNPRIVORTS \\n--dport 25 -m state state NEW -j ACCEPT
```

fi

```
$IPT-A OUTPUT -o $INTERNET -p tcp \\n-s $IPADDR --sport $UNPRIVORTS \\n--dport 25 -j ACCEPT
```

```
$IPT-A INPUT -i $INTERNET -p tcp ! --syn \\n--sport 25 \\n-d $IPADDR --dport $UNPRIVORTS -j ACCEPT
```

```
if [ "$CONNECTION_TRACKING" = "1" ]; then\n$IPT-A INPUT -i $INTERNET -p tcp \\n--sport $UNPRIVORTS \\n-d $IPADDR --dport 25 \\n-m state state NEW -j ACCEPT
```

fi

```
$IPT-A INPUT -i $INTERNET -p tcp \\n--sport $UNPRIVORTS \\n-d $IPADDR --dport 25 -j ACCEPT
```

```
$IPT-A OUTPUT -o $INTERNET -p tcp ! --syn \\n-s $IPADDR --sport 25 \\n--dport $UNPRIVORTS -j ACCEPT
```

# HOSTING A MAIL SERVER FOR REMOTE CLIENTS

Hosting public POP or IMAP services is unusual for a small system. You might do this if you offer remote mail services to a few friends, or if their ISP mail service is