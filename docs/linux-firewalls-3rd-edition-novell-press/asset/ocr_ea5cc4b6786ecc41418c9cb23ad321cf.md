In this example, incoming mail is delivered to the local mail server. LAN clients retrieve their mail from the local mail host using POP. The mail host also functions as a POP server. This rule is applied to the choke firewall, and you would need to define the constant for the POP3 server as POP_SERVER if you use this code:

```
$IPT -A FORWARD -i $LAN_INTERFACE -O $DMZ_INTERFACE -p tcp \
    -s $LAN_ADDRESSES --sport $UNPRIVPORTS \
    -d $POP_SERVER --dport 110 \
    -m state --state NEW -j ACCEPT
```

# RETRIEVING MAIL AS AN IMAP CLIENT THROUGH THE CHOKE FIREWALL (TCP PORT 143)

Connecting to an IMAP server is another common means of retrieving mail from a mail host. The following example demonstrates the firewall rules necessary to retrieve mail from an IMAP server running in the DMZ.

The next rule forwards client connections from the LAN to the IMAP server running on the mail host in the DMZ and is applied to the choke firewall with the IMAP_SERVER constant predefined:

```
$IPT -A FORWARD -i $LAN_INTERFACE -O $DMZ_INTERFACE -p tcp \
    -s $LAN_ADDRESSES --sport $UNPRIVPORTS \
    -d $IMAP_SERVER --dport 143 \
    -m state --state NEW -j ACCEPT
```

# Accessing Usenet News Services (TCP NNTP Port 119)

Usenet news is accessed over the NNTP protocol running on top of TCP through service port 119. Reading news and posting articles are handled by your local news client.

A non-ISP site isn't likely to host a news server for the outside world. Even hosting a local news server is unlikely for a small site. For the site that represents the rare exception, the server rule should be configured to allow incoming connections from only a select set of external clients or external networks. A local public server would run on a machine in the DMZ, and the gateway would forward incoming NNTP connections to the local NNTP server machine.

# GATEWAY NNTP CONDUIT AND SERVER DMZ CONFIGURATIONS

The server rule allows local client connections to your ISP's news server. Both reading news and posting articles are handled by this rule:

```
$IPT -A FORWARD -i $DMZ_INTERFACE -O $EXTERNAL_INTERFACE -p tcp \
    -s $LAN_ADDRESSES --sport $UNPRIVPORTS \
    -d $NEWS_SERVER --dport 119 \
    -m state --state NEW -j ACCEPT
```