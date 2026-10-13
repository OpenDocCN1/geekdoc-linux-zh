The resulting file looks similar to a typical ASCII armored encrypted file, but when the file is decrypted, the extra steps that were taken to sign it pay off. Signing encrypted files or binary files is a good way to ensure they have not been tampered with since you encrypted them. Many software packages, especially security-related software packages, are signed. This process has prevented the sabotage of at least one security program offered using anonymous FTP on the Internet.

# TROUBLESHOOTING

*I’ve set up my email client, but I seem to be having trouble sending mail. It keeps bouncing with a message about sender domain must resolve.*

You’ve probably configured your email client to use your localhost’s sendmail instead of your ISP. This will no longer work, thanks to spammers’ abuse of the email systems. Most MTAs don’t accept mail from systems if they don’t have a valid MX record. Change your email client to point to your ISP’s outgoing mail host.

*I set up my email at home to run through the sendmail server at my work rather than at my ISP, but I keep getting an error message 550 relaying denied and the messages won’t go out.*

By default, sendmail will not permit any messages to come from an external system with another external system as its destination. This is called relaying, and is prohibited. You’ll need to ask your administrator to open up your ISP’s network, your IP, or your range of IPs (if you have a dialup with dynamic IP allocation). Alternately, you’ll need to dial in to your place of work to send mail through your work mail server.

*But I am the administrator of my work system. How do I accomplish the above?*

Unfortunately, in the past, Caldera has elected not to build in the access_db into their sendmail configuration. If this is still the case, you’ll need to add access_db in a line like this in your sendmail.mc file:

```
FEATURE(access_db, hash /etc/mail/access.db')
```

After you’ve rebuilt your sendmail config file, you can start this and do the following:

As root, cd to /etc/mail. Create a file called access. In this file put the appropriate entry to allow yourself access, for example:

```
192.168.0        RELAY
```

The first column can be a full or partial IP address (partial assumes the entire range of IPs in that block) or a domain name. You can also specify an email address in some cases. Legitimate values that can replace RELAY include OK, REJECT, DISCARD, or certain error codes and text.

You then need to issue the following command to create the access.db file:

```
makemap hash access.db <access
```

If you feel uncertain about how to do this, you might want to consider using Webmin, which uses drop down boxes in many places and performs sanity checking.