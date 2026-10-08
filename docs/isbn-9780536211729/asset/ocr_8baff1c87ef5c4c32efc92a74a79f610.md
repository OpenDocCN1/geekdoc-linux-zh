# ACCESSING REMOTEBSITES AS A CLIENT

It's almost inconceivable in today's world that a home-based site would not want to access
World Wide Web from a web browser. The next two rules allow access to remote web
servers:

```
if [ "$CONNECTION_TRACKING" = "1" ]; then
$IPT -A OUTPUT -o $INTERNET -p tcp \
  -s $IPADDR --port $UNPRIVVORTS \
  --dport 80 -m state --NEW -j ACCEPT
```

fi

```
$IPT -A OUTPUT -o $INTERNET -p tcp \
  -s $IPADDR --port $UNPRIVVORTS \
  --dport 80 -j ACCEPT
$IPT -A INPUT -i $INTERNET -p tcp | --syn \
  --sport 80 \
  -d $IPADDR --dport $UNPRIVVORTS -j ACCEPT
```

# ALLOWING REMOTE ACCESS TO A LOCAL WEB SERVER

If you decide to run a web server of your own and host a public website, the following gen-\eral server rules allow all typical incoming access to your site. This is all that most people
need in order to host a website:

if [ "$CONNECTION_TRACKING" = "1" ]; then

```
$IPT -A INPUT -i $INTERNET -p tcp \
  --sport $UNPRIVVORTS \
  -d $IPADDR --dport 80 \
  -m state --NEW -j ACCEPT
```

fi

```
$IPT -A INPUT -i $INTERNET -p tcp \
  --sport $UNPRIVVORTS \
  -d $IPADDR --dport 80 -j ACCEPT
$IPT -A OUTPUT -o $INTERNET -p tcp | --syn \
  -s $IPADDR --port 80 \
  --dport $UNPRIVVORTS -j ACCEPT
```

# SECURE WEB ACCESS (SSL AND TLS) (TCP PORT 443)

Secure Sockets Layer (SSL) and Transport Layer Security (TLS) are used for secure,
encrypted web access. The protocols use TCP port 443. You will most often encounter
if you go to a commercial website to purchase something, use online banking services, or
Enter a protected web area where you will be prompted for personal information. The Apache
web server shipped with Red Hat Linux 7.1 implements OpenSSL support. Table 7.9 lists the
complete client/server connection protocol for the service.