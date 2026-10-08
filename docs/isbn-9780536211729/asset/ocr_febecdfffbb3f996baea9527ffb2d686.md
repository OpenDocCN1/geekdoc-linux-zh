# RECEIVING MAIL AS AN IMAP CLIENT (TCP PORT 143)

Connecting to an IMAP server is another common means of retrieving mail from a remote ISP or when your ISP uses an IMAP server for customer mail retrieval, you need to allow outgoing client-to-server connections.

The server's address will be a specific hostname or address rather than the global, implied WHERE specifier. IMAP accounts are user accounts associated with a specific user and password:

```
IMAP_SERVER=my.isp.imap.server      # external imap server, if any
if [ "CONNECTION_TRACKING" = "1" ]; then
  ipt -A OUTPUT -o $INTERFACE -p tcp \
  -s $IPADDR --sport UNPRIVORTS \
  -d $IMAP_SERVER --dport 143 -m state --state NEW -j ACCEPT

ipt -A OUTPUT -o $INTERFACE -p tcp \
  -s $IPADDR --sport UNPRIVORTS \
  -d $IMAP_SERVER --dport 143 -j ACCEPT
ipt -A INPUT -i $INTERFACE -p tcp ! --syn \
  -s $IMAP_SERVER --dport 143 \
  -d $IPADDR --dport UNPRIVORTS -j ACCEPT
```

# EXAMPLES OF REAL-WORLD CLIENT AND SERVER
EMAIL COMBINATIONS

Four approaches to client and server email combinations are described in this section:

+   - Sending mail as an SMTP client and receiving mail as a POP client
- Sending mail as an SMTP client and receiving mail as an IMAP client
- Sending mail as an SMTP client and receiving mail as an SMTP server
- Sending mail as an SMTP server and receiving mail as an SMTP server

The first two are useful if you rely completely on your ISP's SMTP and POP or IMAP email services. The third example is a mixed approach, relaying outgoing mail through your ISP's SMTP mail server, but receiving mail directly through your local SMTP server. The fourth approach supports running your own complete, independent mail server for both outgoing and incoming mail.

# SENDING MAIL AS AN SMTP CLIENT AND RECEIVING MAIL
AS A POP CLIENT

If you are sending mail as an SMTP client and receiving mail as a POP client, you are relying completely on a remote site for your mail services. The remote site hosts both an SMTP server for relaying your outgoing mail and a POP server for local mail retrieval: