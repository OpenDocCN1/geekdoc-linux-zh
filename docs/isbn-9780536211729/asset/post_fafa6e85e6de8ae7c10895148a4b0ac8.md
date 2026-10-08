
# Enabling Common TCP Services

```bash
$IPT -A INPUT -i $INTERNET -p tcp \
  --sport $UNPRIVPORTS \
  -d $IPADDR --dport 25 -j ACCEPT
```

```bash
$IPT -A OUTPUT -o $INTERNET -p tcp ! --syn \
  -s $IPADDR --sport 25 \
  --dport $UNPRIVPORTS -j ACCEPT
```

# Sending Mail as an SMTP Server and Receiving Mail as an SMTP Server

If you are sending mail as an SMTP server and are receiving mail as an SMTP server, you provide all your own mail services. Your local sendmail daemon is configured to relay outgoing mail to the destination hosts, as well as collect and deliver mail:

```bash
if [ "$CONNECTION_TRACKING" = "1" ]; then
  $IPT -A OUTPUT -o $INTERNET -p tcp \
    -s $IPADDR --sport $UNPRIVPORTS \
    --dport 25 -m state --state NEW -j ACCEPT
fi

$IPT -A OUTPUT -o $INTERNET -p tcp \
  -s $IPADDR --sport $UNPRIVPORTS \
  --dport 25 -j ACCEPT

$IPT -A INPUT -i $INTERNET -p tcp ! --syn \
  --sport 25 \
  -d $IPADDR --dport $UNPRIVPORTS -j ACCEPT

if [ "$CONNECTION_TRACKING" = "1" ]; then
  $IPT -A INPUT -i $INTERNET -p tcp \
    --sport $UNPRIVPORTS \
    -d $IPADDR --dport 25 \
    -m state --state NEW -j ACCEPT
fi

$IPT -A INPUT -i $INTERNET -p tcp \
  --sport $UNPRIVPORTS \
  -d $IPADDR --dport 25 -j ACCEPT

$IPT -A OUTPUT -o $INTERNET -p tcp ! --syn \
  -s $IPADDR --sport 25 \
  --dport $UNPRIVPORTS -j ACCEPT
```

# Hosting a Mail Server for Remote Clients

Hosting public POP or IMAP services is unusual for a small system. You might do this if you offer remote mail services to a few friends, or if their ISP mail service is temporarily unavailable. In any case, it's important to limit the checks your system will accept connections from, both the packet-filtering level and on the server configuration level.

## Hosting a POP Server for Remote Clients

POP servers are one of the most common and successful points of entry for hacking exploits. Firewall rules can offer some amount of protection, in many cases. Of course, you would limit access at the server configuration level as well. As always, and perhaps particularly so with mail server software, it is crucial to keep up-to-date with security updates for the software.

If you use a local system as a central mail server and run a local POP3 server to provide access to local machines on a LAN, you don't need the server rules in this example. Incoming connections from the Internet should be dropped. If you need to have POP service for a limited number of remote individuals, the next two rules allow incoming connections to your POP server. Connections are limited to your specific clients' IP addresses:

```bash
if [ $CONNECTION_TRACKING = "1" ]; then
  $IPT -A INPUT -i $INTERNET -p tcp \
    -s <my.pop.clients> --sport $UNPRIVPORTS \
    -d $IPADDR --port 110 \
    -m state --state NEW -j ACCEPT
fi

$IPT -A INPUT -i $INTERNET -p tcp \
  -s <my.pop.clients> --sport $UNPRIVPORTS \
  -d $IPADDR --port 110 -j ACCEPT

$IPT -A OUTPUT -o $INTERNET -p tcp ! --syn \
  -s $IPADDR --port 110 \
  -d <my.pop.clients> --dport $UNPRIVPORTS -j ACCEPT
```

If your site is an ISP, you could use network address masking to limit which source addresses would accept POP connection requests:

```bash
POP_CLIENTS="192.168.24.0/24"
```

If yours is a residential site with a handful of remote POP clients, the client addresses would need to be explicitly stated, with a separate rule pair for each client address.

## Hosting an IMAP Server for Remote Clients

IMAP servers are one of the most common and successful points of entry for hacking exploits. Firewall rules can offer some amount of protection, in many cases. Of course, you would limit access at the server configuration level as well. As always, and perhaps particularly so with mail server software, it is crucial to keep up-to-date with security updates for the software.

If you use a local system as a central mail server and run a local imap server to provide access to local machines on a LAN, you don't need a server rule. Incoming connections from the Internet should be dropped. If you do need host IMAP service for a limited number of remote individuals, the next two rules allow incoming connections to your IMAP server. Connections are limited to your specific clients' IP addresses:

```bash
if [ "$CONNECTION_TRACKING" = "1" ]; then
  $IPT -A INPUT -i $INTERNET -p tcp \
    -s <my.imap.clients> --sport $UNPRIVPORTS \
    -d $IPADDR --dport 143 \
    -m state --state NEW -j ACCEPT
fi

$IPT -A INPUT -i $INTERNET -p tcp \
  -s <my.imap.clients> --sport $UNPRIVPORTS \
  -d $IPADDR --dport 143 -j ACCEPT

$IPT -A OUTPUT -o $INTERNET -p tcp ! --syn \
  -s $IPADDR --dport 143 \
  -d <my.imap.clients> --dport $UNPRIVPORTS -j ACCEPT
```

If your site were an ISP, you could use network address masking to limit which addresses you would accept IMAP connection requests from:

```bash
IMAP_CLIENTS="192.168.24.0/24"
```

If yours is a residential site with a handful of remote IMAP clients, the client addresses would need to be stated explicitly, with a separate rule pair for each client address.

## 7.5.2 Accessing Usenet News Services
(TCP NNTP Port 119)

Usenet is accessed over NNTP running on top of TCP through service port 119. Reading news and posting articles are handled by your local news client. Few systems require the server rules. Table 7.4 lists the complete client/server connection protocol for the NNTP Usenet news service.

### Table 7.4 NNTP Protocol

| Description | Protocol | Remote Address | Remote Port | In/Out | Local Address | Local Port | TCP Flag |
|---|---|---|---|---|---|---|---|
| Local client query | TCP | NEWS SERVER | 119 | Out | IPADDR | 1024:65535 | Any |
| Remote server response | TCP | NEWS SERVER | 119 | In | IPADDR | 1024:65535 | ACK |
| Remote client query | TCP | NNTP clients | 1024:65535 | In | IPADDR | 119 | Any |
| Local server response | TCP | NNTP clients | 1024:65535 | Out | IPADDR | 119 | ACK |
| Local server query | TCP | News feed | 119 | Out | IPADDR | 1024:65535 | Any |
| Remote server response | TCP | News feed | 119 | In | IPADDR | 1024:65535 | ACK |

### Reading and Posting News as a Usenet Client

The client rules allow connections to your ISP's news server. Both reading and posting articles are allowed by these rules:

```bash
NEWS_SERVER="my.news.server" # external news server, if any
if [ "$CONNECTION_TRACKING" = "1" ]; then
  $IPT -A OUTPUT -o $INTERNET -p tcp \
    -s $IPADDR --sport $UNPRIVPORTS \
    -d $NEWS_SERVER --dport 119 -m state --state NEW -j ACCEPT
fi

$IPT -A OUTPUT -o $INTERNET -p tcp \
  -s $IPADDR --sport $UNPRIVPORTS \
  -d $NEWS_SERVER --dport 119 -j ACCEPT

$IPT -A INPUT -i $INTERNET -p tcp ! --syn \
  -s $NEWS_SERVER --sport 119 \
  -d $IPADDR --dport $UNPRIVPORTS -j ACCEPT
```

### Hosting a Usenet News Server for Remote Clients

A small site is very unlikely to host a news server for the outside world. Even hosting a local news server is unlikely. For the rare exception, server rules should be configured to allow incoming connections from only a set of clients:

```bash
if [ "$CONNECTION_TRACKING" = "1" ]; then
  $IPT -A INPUT -i $INTERNET -p tcp \
    -s <my.news.clients> --sport $UNPRIVPORTS \
    -d $IPADDR --dport 119 \
    -m state --state NEW -j ACCEPT
fi

$IPT -A INPUT -i $INTERNET -p tcp \
  -s <my.news.clients> --sport $UNPRIVPORTS \
  -d $IPADDR --dport 119 -j ACCEPT

$IPT -A OUTPUT -o $INTERNET -p tcp ! \
  -s $IPADDR --sport 119 \
  -d <my.news.clients> --dport $UNPRIVPORTS -j ACCEPT
```

### Allowing Peer News Feeds for a Local Usenet Server

A small, home-based site is unlikely to have a peer-to-peer news-feed relationship with an ISP. Although news servers used to be fairly accessible to the general Internet, few open servers are available nowadays because of SPAM and server load issues.

If your site is large enough or rich enough to host a general Usenet server, you have to get your news feed from somewhere. The next rules allow your local news server to receive its news feed from a remote server. The local server connects to the remote server as a client using the name or address of the host. The only difference between the peer-to-peer news-feed rules and the regular client

```bash
if [ "$CONNECTION_TRACKING" = "1" ]; then
  $IPT -A OUTPUT -o $INTERNET -p tcp \
    -s $IPADDR --sport $UNPRIVPORTS \
    -d $MY_NEWS_FEED --dport 119 -m state --state NEW -j ACCEPT
fi

$IPT -A OUTPUT -o $INTERNET -p tcp \
  -s $IPADDR --sport $UNPRIVPORTS \
  -d $MY_NEWS_FEED --dport 119 -j ACCEPT

$IPT -A INPUT -i $INTERNET -p tcp ! \
  -s <my.news.feed> --sport 119 \
  -d $IPADDR --dport $UNPRIVPORTS -j ACCEPT
```

### 7.5.3 Telnet (TCP Port 23)

Telnet had been the de facto standard means of remote login over the Internet for many years. As the nature of the Internet community has changed, telnet has come to be viewed more as an insecure service because it communicates in ASCII clear text. If you have the option, you should always use an encrypted service, such as SSH, rather than telnet. However, Microsoft Windows does not offer an SSH service and only offers telnet—so much for security commitment!
