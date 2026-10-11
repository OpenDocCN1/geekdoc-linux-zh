The following entries merely ensure that Postfix only accepts mail from the clients in the local network:

```
# 10.0.0.51 is the IP in the LAN
inet_interfaces = 10.0.0.51, 127.0.0.1
mynetworks = 10.0.0.0/24, 127.0.0.0/8
smtpd_recipient_restrictions = permit_mynetworks, reject

```

It is necessary to rewrite addresses to make sure that the sender does not appear in the form

**geeko@da51.digitalairlines.com**

but in the common form

**geeko@digitalairlines.com**

On the other hand, the host is important for messages sent to root.
Therefore, mail addressed to root should not be rewritten.

Two entries in the file /etc/postfix/main.cf are sufficient for this simple scenario:

```
masquerade_exceptions = root
masquerade_domains = digitalairlines.com

```

Moreover, Postfix must be informed of the mail server to which it is supposed to deliver the mail.

The relayhost entry also ensures that Postfix does not attempt to establish a direct contact to respective mail servers of the recipients.

```
relayhost = dal.digitalairlines.com

```