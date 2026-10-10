
## Table 4.2 Ident Protocol

| DESCRIPTION | PROTOCOL | REMOTE ADDRESS | REMOTE PORT | LOCAL IN/OUT | LOCAL ADDRESS | LOCAL PORT | TCP FLAG |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| Local client query | TCP | ANYWHERE | 113 | Out | IPADDR | 1024:65535 | Any |
| Remote server response | TCP | ANYWHERE | 113 | In | IPADDR | 1024:65535 | ACK |
| Remote client query | TCP | ANYWHERE | 1024:65535 | In | IPADDR | 113 | Any |
| Local server response | TCP | ANYWHERE | 1024:65535 | Out | IPADDR | 113 | ACK |

## Allowing Your Outgoing AUTH Requests as a Client

Your machine would act as an AUTH client if you ran a mail or FTP server. Here are rules to allow your server to act as an AUTH client, should you choose to do so:

```
if [ "$CONNECTION_TRACKING" = "1" ]; then
  $IPT -A OUTPUT -o $INTERNET -p tcp \
       -s $IPADDR --sport $UNPRIVPORTS \
       --dport 113 -m state --state NEW -j ACCEPT
fi
$IPT -A OUTPUT -o $INTERNET -p tcp \
     -s $IPADDR --sport $UNPRIVPORTS \
     --dport 113 -j ACCEPT
$IPT -A INPUT -i $INTERNET -p tcp ! --syn \
     --sport 113 \
     -d $IPADDR --dport $UNPRIVPORTS -j ACCEPT
```

## Filtering Incoming AUTH Requests to Your Server

Whether or not you decide to offer the service, you will likely receive incoming requests for the service when you send mail.

If you run the `identd` server, the following rules enable incoming `identd` connection requests:

```
if [ "$CONNECTION_TRACKING" = "1" ]; then
  $IPT -A INPUT -i $INTERNET -p tcp \
       --sport $UNPRIVPORTS \
       -d $IPADDR --dport 113 \
       -m state --state NEW -j ACCEPT
fi
$IPT -A INPUT -i $INTERNET -p tcp \
--sport $UNPRIVPORTS \
-d $IPADDR --dport 113 -j ACCEPT
```

```
$IPT -A OUTPUT -o $INTERNET -p tcp ! --syn \
-s $IPADDR --sport 113 \
--dport $UNPRIVPORTS -j ACCEPT
```

If you decide not to offer the service, it’s a good practice to reject the connection request to avoid waiting for the TCP connection timeout. This is the case only when an incoming packet is rejected rather than dropped, in these examples:

```
$IPT -A INPUT -i $INTERNET -p tcp \
--sport $UNPRIVPORTS \
-d $IPADDR --dport 113 -j REJECT --reject-with tcp-reset
```

Alternatively, you could use the accept rules but not run the `identd` server. The result would be the same: The TCP layer would return a TCP RST message to the sender.

## Enabling Common TCP Services

It’s likely that no one will want to enable all the services listed in this section, but most everyone will want to enable some subset of them. These are the services most often used over the Internet today. As such, this section is more of a reference section than anything else. This section provides rules for the following:

- Email
- Usenet
- Telnet
- SSH
- FTP
- Web services
- Whois
- RealAudio, RealVideo, and QuickTime

Many other services are available that aren’t covered here. Some of them are used on specialized servers, some are used by large businesses and organizations, and some are designed for use in local, private networks. Additional LAN and DMZ services are covered in Chapter 6.

### Email (TCP SMTP Port 25, POP Port 110, IMAP Port 143)

Email is a service that almost everyone wants. How mail is set up depends on your ISP, your connection type, and your own choices. Email is sent across the network using the SMTP protocol assigned to TCP service port 25. Email is commonly received locally through one of three different protocols—SMTP, POP, or IMAP—depending on the services your ISP provides and on your local configuration.

SMTP is the general mail protocol. Mail is delivered to the destination host machine, as defined most commonly by the MX record in the DNS for the given domain. The endpoint mail server determines whether the mail is deliverable (addressed to a valid user account on the machine) and then delivers it to the user's local mailbox.

POP and IMAP are mail-retrieval services. POP runs on TCP port 110. IMAP runs on TCP port 143. ISPs commonly make incoming mail available to their customers using one or both of these two services. Both services are usually authenticated by username and password. As far as mail retrieval is concerned, the difference between SMTP and POP or IMAP is that SMTP receives incoming mail and queues it in the user's local mailbox. POP and IMAP retrieve mail into the user's local mail program from the user's ISP, where the mail had been queued remotely in the user's SMTP mailbox at the ISP. Table 4.3 lists the complete client/server connection protocols for SMTP, POP, and IMAP. SMTP also uses specialized delivery mechanisms that your local network might use, such as ETRN, that effectively transfer all mail for a given domain for local processing.

#### Table 4.3 SMTP, POP, and IMAP Mail Protocols

| DESCRIPTION | PROTOCOL | REMOTE ADDRESS | REMOTE PORT | LOCAL IN/OUT | LOCAL ADDRESS | LOCAL PORT | TCP FLAG |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| Send outgoing mail | TCP | ANYWHERE | 25 | Out | IPADDR | 1024: 65535 | Any |
| Remote server response | TCP | ANYWHERE | 25 | In | IPADDR | 1024: 65535 | ACK |
| Receive incoming mail | TCP | ANYWHERE | 1024: 65535 | In | IPADDR | 25 | Any |
| Local server response | TCP | ANYWHERE | 1024: 65536 | Out | IPADDR | 25 | ACK |
| Local client query | TCP | POP SERVER | 110 | Out | IPADDR | 1024: 65535 | Any |
| Remote server response | TCP | POP SERVER | 110 | In | IPADDR | 1024: 65535 | ACK |
| Remote client query | TCP | POP CLIENT | 1024:65535 | In | IPADDR | 110 | Any |
| Local server response | TCP | POP CLIENT | 1024:65535 | Out | IPADDR | 110 | ACK |
| Local client query | TCP | IMAP SERVER | 143 | Out | IPADDR | 1024:65535 | Any |
| Remote server response | TCP | IMAP SERVER | 143 | In | IPADDR | 1024:65535 | ACK |
| Remote client query | TCP | IMAP CLIENT | 1024:65535 | In | IPADDR | 143 | Any |
| Local server response | TCP | IMAP CLIENT | 1024:65535 | Out | IPADDR | 143 | ACK |

### Sending Mail over SMTP (TCP Port 25)

Mail is sent over SMTP. But whose SMTP server do you use to collect your mail and send it onward? ISPs offer SMTP mail service to their customers. The ISPs mail server acts as the mail gateway. It knows how to collect your mail, find the recipient host, and relay the mail. With UNIX, you can host your own local mail server, if you want. Your server will be responsible for routing the mail to its destination.

### Relaying Outgoing Mail Through an External (ISP) Gateway SMTP Server

When you relay outgoing mail through an external mail gateway server, your client mail program sends all outgoing mail to your ISP’s mail server. Your ISP acts as your mail gateway to the rest of the world. Your system doesn’t need to know how to locate your mail destinations or the routes to them. The ISP mail gateway serves as your relay.

The following two rules enable you to relay mail through your ISP’s SMTP gateway:

```
SMTP_GATEWAY="my.isp.server"      # external mail server or relay

if [ "$CONNECTION_TRACKING" = "1" ]; then
    $IPT -A OUTPUT -o $INTERNET -p tcp \
    -s $IPADDR --sport $UNPRIVPORTS \
    -d $SMTP_GATEWAY --dport 25 -m state --state NEW -j ACCEPT
fi

$IPT -A OUTPUT -o $INTERNET -p tcp \
-s $IPADDR --sport $UNPRIVPORTS \
-d $SMTP_GATEWAY --dport 25 -j ACCEPT
$IPT -A INPUT -i $INTERNET -p tcp ! --syn \
-s $SMTP_GATEWAY --sport 25 \
-d $IPADDR --dport $UNPRIVPORTS -j ACCEPT
```

### Sending Mail to Any External Mail Server

Alternatively, you can bypass your ISP’s mail server and host your own. Your local server is responsible for collecting your outgoing mail, doing the DNS lookup on the destination host-name, and sending the mail to its destination. Your client mail program points to your local SMTP server rather than to the ISP’s server.

The following two rules enable you to send mail directly to the remote destinations:

```
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
```

### Receiving Mail

How you receive mail depends on your situation. If you run your own local mail server, you can collect incoming mail directly on your Linux machine. If you retrieve your mail from your ISP account, you may or may not retrieve mail as a POP or IMAP client, depending on how you’ve configured your ISP email account, and depending on the mail delivery services the ISP offers.

### Receiving Mail as a Local SMTP Server (TCP Port 25)

If you want to receive mail sent directly to your local machines from anywhere in the world, you need to run sendmail, qmail, or some other mail server program. These are the local server rules:

```
if [ "$CONNECTION_TRACKING" = "1" ]; then
$IPT -A INPUT -i $INTERNET -p tcp \
--sport $UNPRIVPORTS \
-d $IPADDR --dport 25 \
-m state --state NEW -j ACCEPT
```
