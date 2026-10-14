# Configurable Options for Mail Forwarding

Webmin and Usermin support a number of different mail transfer agents (MTAs), namely Sendmail, Postfix, and Qmail. This option should be set to the mail transfer agent that your server uses. Postfix is not listed as an option, however, because Postfix is entirely Sendmail-compatible from a user perspective. Simply select Sendmail if Postfix is the MTA, and everything will work as expected.

# Configurable Options for Read Mail

The Usermin Read Mail module offers users a complete, if basic, web-based mail client. It allows the user to send and receive mail, as well as keep a simple address book and digitally sign or encrypt messages. For this module there are a number of configurable options, as shown in Figure 4-2 and Figure 4-3.

![](bbox=[0.25, 0.44, 0.7, 0.7])

Figure 4-2: Configurable options for Read Mail

# Default hostname for From: addresses

This is the host name that will be included in the mail headers in the From field. If you wish all mail from your domain to be addressed from just the domain name (rather than, for example, mail.domain.com) you may enter it here. Entering domain.com will cause all mail sent from this machine using the Usermin mail client to appear to be from domain.com.

# Allow editing of From: address

If Yes the user can enter any address they choose in the From field. If No, all mail will be marked as originating from the domain you chose in the previous option. It may be appropriate to permit this change, if clients have their own domain names or would like to be able to primarily use another address and do not want to keep up with replies to another mailbox.