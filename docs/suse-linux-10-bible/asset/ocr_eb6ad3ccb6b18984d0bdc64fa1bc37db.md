# Enabling SMTP-AUTH

To enable SMTP authentication, change the drop-down box for authentication through SMTP-AUTH to On and click the Confirm button.

Your users will be able to configure their mail clients to send authentication information to the SMTP server before they attempt to send any mail.

> The mail server will not ask the client for authentication details for the user. It is up to the client to tell the mail server wants to authenticate before sending mail. With this in mind, a mail client must support the SMTP-AUTH standard to be able to authenticate to an SMTP server.

# Enabling Spam Prevention

With most things in the world, there are people who want to spam email the rest of us. Spammers are out there, sending useless mail by the thousands, and most people's mailboxes are full of this spam.

SLOX includes the excellent SpamAssassin prevention mechanism to check each email that is received by the mail server based on things such as keywords, the for- mat of the mail (HTML as opposed to plain text), inclusion of images, and so on.

![](bbox=[0.176, 0.118, 0.823, 0.506])