```
$IPT -A FORWARD -i $SERVER_LAN_INTERFACE -o $EXTERNAL_INTERFACE -p udp \
-s $DNS_SERVER --sport 53 \
-d $NAME_SERVER_1 --dport 53 \
-m state --state NEW -j ACCEPT
$IPT -A FORWARD -i $SERVER_LAN_INTERFACE -o $EXTERNAL_INTERFACE -p udp \
-s $DNS_SERVER --sport $SNPRIVPORTS \
-d $NAME_SERVER_1 --dport 53 \
-m state --state NEW -j ACCEPT
$IPT -A FORWARD -i $SERVER_LAN_INTERFACE -o $EXTERNAL_INTERFACE -p tcp \
-s $DNS_SERVER --sport $SNPRIVPORTS \
-d $NAME_SERVER_1 --dport 53 \
-m state --state NEW -j ACCEPT
```

The hosts in the CLIENT_LAN point to the MAIL_SERVER as their mail gateway for sending mail:

```
# Sending Mail - SMTP
# -------------------
$IPT -A FORWARD -i $CLIENT_LAN_INTERFACE -o $SERVER_LAN_INTERFACE -p tcp \
-s $CLIENT_ADDRESSES --sport $SNPRIVPORTS \
-d $MAIL_SERVER --dport 25 \
-m state --state NEW -j ACCEPT
```

The SMTP server on the SERVER_LAN needs to send the mail to remote destinations. The server requires access through the firewall to the Internet:

```
$IPT -A FORWARD -i $SERVER_LAN_INTERFACE -o $EXTERNAL_INTERFACE -p tcp \
-s $MAIL_SERVER --sport $SNPRIVPORTS --dport 25 \
-m state --state NEW -j ACCEPT
```

The local mail server also needs to receive incoming mail from remote sites:

```
$IPT -A FORWARD -i $EXTERNAL_INTERFACE --o $SERVER_LAN_INTERFACE -p tcp \
--sport $SNPRIVPORTS -d $MAIL_SERVER --dport 25 \
-m state --state NEW -j ACCEPT
```

Note that, for incoming mail to be addressed to the mail server, the name server must have a publicly accessible MX record advertising the host as the site's mail server. In this particular set of examples, the DNS rules do not allow for incoming DNS queries from the Internet. Thus, the remote name server would need to provide this service. (Alternative solutions using NAT and host forwarding are described in Chapter 7.) Be aware that some *spam conscious* Internet providers prevent incoming and outgoing connections on port 25, the common SMTP port. This of course breaks the end-to-end nature of the Internet.