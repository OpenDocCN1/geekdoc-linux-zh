
# CHAPTER 4: Building and Installing a Standalone Firewall

```bash
$IPT -A INPUT  -i $INTERNET -p tcp \
   --sport $UNRIVPORTS \
   -d $IPADDR --dport 25 -j ACCEPT

$IPT -A OUTPUT -o $INTERNET -p tcp ! --syn \
   -s $IPADDR --sport 25 \
   --dport $UNRIVPORTS -j ACCEPT
```

Alternatively, if you'd rather keep your local mail account relatively private and use your work or ISP mail account as your public address, you can configure your work and ISP mail accounts to forward mail to your local server. In this case, you could replace the previous single rule pair, accepting connections from anywhere, with separate, specific rules for each mail forwarder.

## RETRIEVING MAIL AS A POP CLIENT (TCP PORT 110)

Connecting to a POP server is a very common means of retrieving mail from a remote ISP or work account. If your ISP uses a POP server for customer mail retrieval, you need to allow outgoing client-to-server connections.

The server's address will be a specific hostname or address rather than the global, implied ANYWHERE specifier. POP accounts are user accounts associated with a specific user and password:

```bash
POP_SERVER="my.isp.pop.server"      # external pop server, if any

if [ "$CONNECTION_TRACKING" = "1" ]; then
   $IPT -A OUTPUT -o $INTERNET -p tcp \
        --sport $UNRIVPORTS \
        -d $POP_SERVER --dport 110 -m state --state NEW -j ACCEPT
fi

$IPT -A OUTPUT -o $INTERNET -p tcp \
     -s $IPADDR --sport $UNRIVPORTS \
     -d $POP_SERVER --dport 110 -j ACCEPT

$IPT -A INPUT -i $INTERNET -p tcp ! --syn \
   -s $POP_SERVER --dport 110 \
   -d $IPADDR --dport $UNRIVPORTS -j ACCEPT
```

## RECEIVING MAIL AS AN IMAP CLIENT (TCP PORT 143)

Connecting to an IMAP server is another common means of retrieving mail from a remote ISP or work account. If your ISP uses an IMAP server for customer mail retrieval, you need to allow outgoing client-to-server connections.

The server's address will be a specific hostname or address rather than the global, implied ANYWHERE specifier. IMAP accounts are user accounts associated with a specific user and password:

```bash
IMAP_SERVER="my.isp.imap.server" # external imap server, if any

if [ "$CONNECTION_TRACKING" = "1" ]; then
$IPT -A OUTPUT -o $INTERNET -p tcp \
-s $IPADDR --sport $UNRIVPORTS \
-d $IMAP_SERVER --dport 143 -m state --state NEW -j ACCEPT
fi

$IPT -A OUTPUT -o $INTERNET -p tcp \
-s $IPADDR --sport $UNRIVPORTS \
-d $IMAP_SERVER --dport 143 -j ACCEPT

$IPT -A INPUT -i $INTERNET -p tcp ! --syn \
-s $IMAP_SERVER --dport 143 \
-d $IPADDR --dport $UNRIVPORTS -j ACCEPT
```

## EXAMPLES OF REAL-WORLD CLIENT AND SERVER EMAIL COMBINATIONS

Four common approaches to client and server email combinations are described in this section:

- Sending mail as an SMTP client and receiving mail as a POP client
- Sending mail as an SMTP client and receiving mail as an IMAP client
- Sending mail as an SMTP client and receiving mail as an SMTP server
- Sending mail as an SMTP server and receiving mail as an SMTP server

The first two are useful if you rely completely on your ISP's SMTP and POP or IMAP email services. The third example is a mixed approach, relaying outgoing mail through your ISP's SMTP mail server, but receiving mail directly through your local SMTP server. The fourth approach supports running your own complete, independent mail server for both outgoing and incoming mail.

## SENDING MAIL AS AN SMTP CLIENT AND RECEIVING MAIL AS A POP CLIENT

If you are sending mail as an SMTP client and are receiving mail as a POP client, you are relying completely on a remote site for your mail services. The remote site hosts both an SMTP server for relaying your outgoing mail and a POP server for local mail retrieval:

```bash
SMTP_GATEWAY="my.isp.server" # external mail server or relay

if [ "$CONNECTION_TRACKING" = "1" ]; then
  $IPT -A OUTPUT -o $INTERNET -p tcp \
    -s $IPADDR --sport $UNRIVPORTS \
    -d $SMTP_GATEWAY --dport 25 -m state --state NEW -j ACCEPT
fi

$IPT -A OUTPUT -o $INTERNET -p tcp \
  -s $IPADDR --sport $UNRIVPORTS \
  -d $SMTP_GATEWAY --dport 25 -j ACCEPT

$IPT -A INPUT -i $INTERNET -p tcp ! --syn \
  -s $SMTP_GATEWAY --dport 25 \
  -d $IPADDR --dport $UNRIVPORTS -j ACCEPT

POP_SERVER="my.isp.pop.server" # external pop server, if any

if [ "$CONNECTION_TRACKING" = "1" ]; then
  $IPT -A OUTPUT -o $INTERNET -p tcp \
    -s $IPADDR --sport $UNRIVPORTS \
    -d $POP_SERVER --dport 110 -m state --state NEW -j ACCEPT
fi

$IPT -A OUTPUT -o $INTERNET -p tcp \
  -s $IPADDR --sport $UNRIVPORTS \
  -d $POP_SERVER --dport 110 -j ACCEPT

$IPT -A INPUT -i $INTERNET -p tcp ! --syn \
  -s $POP_SERVER --dport 110 \
  -d $IPADDR --dport $UNRIVPORTS -j ACCEPT
```

## SENDING MAIL AS AN SMTP CLIENT AND RECEIVING MAIL AS AN IMAP CLIENT

If you are sending mail as an SMTP client and are receiving mail as an IMAP client, you are relying completely on a remote site for your mail services. The remote site hosts both an SMTP server for relaying your outgoing mail and an IMAP server for local mail retrieval:

```bash
SMTP_GATEWAY="my.isp.server" # external mail server or relay

if [ "$CONNECTION_TRACKING" = "1" ]; then
  $IPT -A OUTPUT -o $INTERNET -p tcp \
    -s $IPADDR --sport $UNRIVPORTS \
    -d $SMTP_GATEWAY --dport 25 -m state --state NEW -j ACCEPT
fi

$IPT -A OUTPUT -o $INTERNET -p tcp \
  -s $IPADDR --sport $UNRIVPORTS \
  -d $SMTP_GATEWAY --dport 25 -j ACCEPT

$IPT -A INPUT -i $INTERNET -p tcp ! --syn \
  -s $SMTP_GATEWAY --dport 25 \
  -d $IPADDR --dport $UNRIVPORTS -j ACCEPT

IMAP_SERVER="my.isp.imap.server"    # external imap server, if any

if [ "$CONNECTION_TRACKING" = "1" ]; then
$IPT -A OUTPUT -o $INTERNET -p tcp \
-s $IPADDR --sport $UNRIVPORTS \
-d $IMAP_SERVER --dport 143 -m state --state NEW -j ACCEPT
fi

$IPT -A OUTPUT -o $INTERNET -p tcp \
-s $IPADDR --sport $UNRIVPORTS \
-d $IMAP_SERVER --dport 143 -j ACCEPT

$IPT -A INPUT -i $INTERNET -p tcp ! --syn \
-s $IMAP_SERVER --dport 143 \
-d $IPADDR --dport $UNRIVPORTS -j ACCEPT
```

## SENDING MAIL AS AN SMTP CLIENT AND RECEIVING MAIL AS AN SMTP SERVER

If you are sending mail as an SMTP client and are receiving mail as an SMTP server, you are relying on a remote site to offer SMTP service to relay your outgoing mail to remote destinations. You run `sendmail` locally as a local SMTP server, allowing remote hosts to send mail to your machine directly. Outgoing mail is relayed through your ISP, but the local `sendmail` daemon knows how to deliver incoming mail to local user accounts.

```bash
SMTP_GATEWAY="my.isp.server"    # external mail server or relay

if [ "$CONNECTION_TRACKING" = "1" ]; then
$IPT -A OUTPUT -o $INTERNET -p tcp \
-s $IPADDR --sport $UNRIVPORTS \
-d $SMTP_GATEWAY --dport 25 -m state --state NEW -j ACCEPT
fi

$IPT -A OUTPUT -o $INTERNET -p tcp \
-s $IPADDR --sport $UNRIVPORTS \
-d $SMTP_GATEWAY --dport 25 -j ACCEPT

$IPT -A INPUT -i $INTERNET -p tcp ! --syn \
-s $SMTP_GATEWAY --dport 25 \
-d $IPADDR --dport $UNRIVPORTS -j ACCEPT

if [ "$CONNECTION_TRACKING" = "1" ]; then
  $IPT -A INPUT  -i $INTERNET -p tcp \
    --dport $UNRIVPORTS \
    -d $IPADDR --dport 25 \
    -m state --state NEW -j ACCEPT
fi

$IPT -A INPUT  -i $INTERNET -p tcp \
    --dport $UNRIVPORTS \
    -d $IPADDR --dport 25 -j ACCEPT

$IPT -A OUTPUT -o $INTERNET -p tcp ! --syn \
  -s $IPADDR --dport 25 \
  --dport $UNRIVPORTS -j ACCEPT
```

## SENDING MAIL AS AN SMTP SERVER AND RECEIVING MAIL AS AN SMTP SERVER

If you are sending mail as an SMTP server and are receiving mail as an SMTP server, you provide all your own mail services. Your local sendmail daemon is configured to relay outgoing mail to the destination hosts itself, as well as collect and deliver incoming mail:

```bash
if [ "$CONNECTION_TRACKING" = "1" ]; then
  $IPT -A OUTPUT -o $INTERNET -p tcp \
    -s $IPADDR --sport $UNRIVPORTS \
    --dport 25 -m state --state NEW -j ACCEPT
fi

$IPT -A OUTPUT -o $INTERNET -p tcp \
  -s $IPADDR --sport $UNRIVPORTS \
  --dport 25 -j ACCEPT

$IPT -A INPUT -i $INTERNET -p tcp ! --syn \
  --dport $UNRIVPORTS \
  -d $IPADDR --dport 25 -j ACCEPT

if [ "$CONNECTION_TRACKING" = "1" ]; then
  $IPT -A INPUT  -i $INTERNET -p tcp \
    --dport $UNRIVPORTS \
    -d $IPADDR --dport 25 \
    -m state --state NEW -j ACCEPT
fi

$IPT -A INPUT  -i $INTERNET -p tcp \
  --dport $UNRIVPORTS \
  -d $IPADDR --dport 25 -j ACCEPT
```
