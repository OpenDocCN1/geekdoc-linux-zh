> NOTE See the Postfix FAQ at www.postfix.org for detailed information on how to set up Postfix for a gateway, a local workstation, or a host directly connected to the Internet (null server).

# Security: UCM

Postfix parameters let you configure methods for controlling what it politely refers to as unsolicited commercial mail (UCM).

# Controlling User and Host Access

With an access file, you can control access by certain users, hosts, and domains. The access file works much like the one used for Sendmail. Entries are made in a text file beginning with the user, host, or domain name or address, followed by an action to be take. A user, host, or domain can be accepted, rejected, or rejected with a message. Once entries are made, they can be installed in a Postfix database file with the postmap command:

```
postmap /etc/postfix/access
```

You can then use the access file in various Postfix operations to control clients, recipients, and senders.

# Blocking Access

Access can also be controlled by use of the Mail Abuse Prevention System (MAPS), which provides the RBL+ service, a collection of mail address DNS-based databases (mail-abuse.org). These databases, like the Real-time Blackhole List (RBL), list mail addresses that are known to be used by mail abusers. A domain or host is matched against a list maintained by the service. The service can be accessed on a local server or or directly from an online site. Various Postfix operations let you use MAPS databases to control access by clients, recipients, senders.

# Header and Body Checks

With the header_checks parameter, you can specify a Postfix table where you can list criteria for rejecting messages. The criteria are patterns that can match message headers. You can have matching messages rejected, rejected with a reply, simply deleted, or a warning logged. You have the option of taking several actions including REJECT, DISCARD, WARN, HOLD, and IGNORE.