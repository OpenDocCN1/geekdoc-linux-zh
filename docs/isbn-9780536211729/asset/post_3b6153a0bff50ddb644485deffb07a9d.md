
```bash
$IPT -A INPUT -i $INTERNET -p udp \
-s $NAMESERVER --sport 53 \
-d $IPADDR --dport 53 -j ACCEPT
```

If the lookup fails because of UDP packet size, the server will fall back to a TCP-mode loop. If the lookup fails because the remote server doesn't have the information, the local server will query the root cache server. Because of these servers, the clients would need to allow DNS traffic to any server, rather than to specific servers listed in the local configuration.

The alternative BIND configuration is to configure it not only as a forwarding server, but also as a slave to the remote servers specified in the BIND configuration file, named.conf. As a slave, the general client UDP rules aren't required.

## 7.4.2 Filtering AUTH User Identification Service (TCP Port 113)

The AUTH, or ident, user identification service is sometimes used when sending mail or posting aenet article. Some FTP sites are also configured to require a resolvable AUTH lookup. For logging purposes, the server initiates an AUTH request back to your machine to get the account name of the user who initiated the mail or news connection. Table 7.2 lists the complete client/server connection protocol for the AUTH service. It's becoming less common for this service to be required though, and therefore I wouldn't recommend running on your servers.

### Table 7.2 ident Protocol

| Description | Protocol | Remote Address | Remote Port | In/Out | Local Address | Local Port | TCP Flag |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| Local client query | TCP | ANYWHERE | 113 | Out | IPADDR | 1024:65535 | Any |
| Remote server response | TCP | ANYWHERE | 113 | In | IPADDR | 1024:65535 | ACK |
| Remote client query | TCP | ANYWHERE | 1024:65535 | In | IPADDR | 113 | Any |
| Local server response | TCP | ANYWHERE | 1024:65535 | Out | IPADDR | 113 | ACK |

### ALLOWING YOUR OUTGOING AUTH REQUESTS AS A CLIENT

Your machine would act as an AUTH client if you ran a mail or FTP server. Here are rules to allow your server to act as an AUTH client, which you choose to do so:

```bash
if [ "$CONNECTION_TRACKING" = "1" ]; then $IPT -A OUTPUT -o $INTERNET -p tcp \
-s $IPADDR --sport $UNPRIVPORTS \
--dport 113 -m state --state NEW -j ACCEPT
fi
$IPT -A OUTPUT -o $INTERNET -p tcp \
-s $IPADDR --sport $UNPRIVPORTS \
--dport 113 -j ACCEPT
```

```bash
$IPT -A INPUT -i $INTERNET -p tcp ! --syn \
--sport 113 \
-d $IPADDR --dport $UNPRIVPORTS -j ACCEPT
```

### FILTERING INCOMING REQUESTS TO YOUR SERVER

Whether or not you decide to offer the service, you will likely receive incoming requests the service when you send mail.

If you run the identd server, the following rules enable incoming identd connection requests:

```bash
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

```bash
$IPT -A OUTPUT -o $INTERNET -p tcp ! --syn \
-s $IPADDR --sport 113 \
--dport $UNPRIVPORTS -j ACCEPT
```

If you decide not to offer the service, it's a good practice to reject the connection request to avoid waiting for the TCP connection timeout. This is the case only when an incoming packet is rejected rather than dropped, in these examples:

```bash
$IPT -A INPUT -i $INTERNET -p tcp \
--sport $UNPRIVPORTS \
-d $IPADDR --dport 113 -j REJECT --reject-with tcp-reset
```

Alternatively, you could use the accept rules but run not the identd server. The result would be the same: The TCP layer would return a TCP RST message to the sender.

## 7.5 Enabling Common TCP Services

It's likely that no one will want to enable all the services listed in this section, but most everyone will want to enable some subset of them. These are the services most used over the Internet today. As such, this section is more of a reference section than anything else. This section provides rules for the following:

- Email
- Usenet
- Telnet
- SSH
- FTP
- Web services
- Whois
- RealAudio, RealVideo, and QuickTime

### 7.5.1 Email (TCP SMTP Port 25, POP Port 110, IMAP Port 143)

Many other services are available that aren't covered here. Some of them are used on specialized servers, some are used by large businesses and organizations, and some are designed for use in local, private networks.

Email is a service that almost everyone wants. How mail is set up depends on your ISP, your connection type, and your own choices. Email is sent across the network using the SMTP protocol assigned to TCP service port 25. Email is commonly received locally through one of three different protocols—SMTP, POP, or IMAP—depending on the services your ISP provides and on your local configuration.

SMTP is the general mail protocol. Mail is delivered to the destination host machine, as defined most commonly by the MX record in the DNS for the given domain. The end-point mail server determines whether the mail is deliverable (addressed to a valid user account on the machine) and delivers it to the user's local mailbox.

POP and IMAP are mail-retrieval services. POP runs on TCP port 110. IMAP runs on TCP port 143. ISPs commonly make incoming mail available to their customers using one or both of these services. Both services are usually authenticated by username and password. As far as mail retrieval is concerned, the difference between SMTP and POP or IMAP is that SMTP receives incoming mail and queues it in the user's local mailbox. POP and IMAP retrieve mail into the user's local mail program from the user's ISP, where the mail had been queued remotely in the user's SMTP mailbox at the ISP. Table 7.3 lists the client/server connection protocols for SMTP, POP, and IMAP. SMTP also uses specialized delivery mechanisms that your local network might use, such as ETRN, that effectively transfers all mail for a given domain for local processing.

### Table 7.3 SMTP, POP, and IMAP Mail Protocols

| Description | Protocol | Remote Address | Remote Port | In/Out | Local Address | Local Port | TCP Flag |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| Send outgoing mail | TCP | ANYWHERE | 25 | Out | IPADDR | 1024:65535 | Any |
| Remote server response | TCP | ANYWHERE | 25 | In | IPADDR | 1024:65535 | ACK |
| Receive incoming mail | TCP | ANYWHERE | 1024:65535 | In | IPADDR | 25 | Any |
| Local server response | TCP | ANYWHERE | 1024:65535 | Out | IPADDR | 25 | ACK |
| Local client query | TCP | POP SERVER | 110 | Out | IPADDR | 1024:65535 | Any |
| Remote server response | TCP | POP SERVER | 110 | In | IPADDR | 1024:65535 | ACK |
| Remote client query | TCP | POP CLIENT | 1024:65535 | In | IPADDR | 110 | Any |
| Local server response | TCP | POP CLIENT | 1024:65535 | Out | IPADDR | 110 | ACK |
| Local client query | TCP | IMAP SERVER | 143 | Out | IPADDR | 1024:65535 | Any |
| Remote server response | TCP | IMAP SERVER | 143 | In | IPADDR | 1024:65535 | ACK |
| Remote client query | TCP | IMAP CLIENT | 1024:65535 | In | IPADDR | 143 | Any |
| Local server response | TCP | IMAP CLIENT | 1024:65535 | Out | IPADDR | 143 | ACK |

### SENDING MAIL OVER SMTP (TCP PORT 25)

Mail is sent over SMTP. But whose SMTP server do you use to collect your mail and send it onward? ISPs offer SMTP mail service to their customers. The ISP's mail server acts as the mail gateway. It knows how to collect your mail, find the recipient host, and relay the mail gateway. With UNIX, you can host your own local mail server, if you want. Your server will be responsible for routing the mail to its destination.

### RELAYING OUTGOING MAIL THROUGH AN EXTERNAL (ISP) GATEWAY SMTP SERVER

When you relay outgoing mail through an external mail gateway server, your client mail program sends all outgoing mail to your ISP's mail server. Your ISP acts as your mail gateway to the rest of the world. Your system doesn't need to know how to locate your mail destinations or the routes to them. The ISP mail gateway serves as your relay.
