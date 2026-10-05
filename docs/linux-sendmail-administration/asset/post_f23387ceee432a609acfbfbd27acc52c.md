
## Listing 9.8 A Sample nullclient Configuration

```
[root]$ cat client-only.mc
OSTYPE(linux)
FEATURE('nullclient', 'wren.foobirds.org')
[root]# m4 -../m4.cf client-only.mc > client-only.cf
[root]# grep 'wren' client-only.cf
DSw.foobirds.org
DHren.foobirds.org
DWren.foobirds.org
```

In this case, we use a DOMAIN macro file. Instead, we replace the entire configuration with the client-only file that contains only two lines. Unlike all of the other macro control files we have created in this book, client-only.mc does not contain a MAILER command. The two lines in the file are a OSTYPE type to specify that we are running Linux and the nullclient configuration. The nullclient feature requires an argument to identify the external server. In Listing 9.8, the remote server is identified as wren.foobirds.org.

When the small client-only.mc file is processed through m4 to produce the client-only.cf, you might be surprised to find that this configuration file is no smaller than any other sendmail.cf. The nullclient feature does not produce a radically different configuration. How it stores the value from the argument field in the S, H, and M variables. S, H, and M direct how mail is processed in the nullclient configuration.

You're familiar with the M variable from the discussion of masquerading. The argument associated with the nullclient feature is used as the masquerade value so that all mail sent from the client is masqueraded as if it came from the external server.

The S variable holds the name of the SMART_HOST relay. The SMART_HOST is the server used for outbound mail. The H variable holds the name of the MAIL_HUB server that collects inbound mail, even mail addressed from one local user to another local user. The role of the MAIL_HUB is particularly surprising because local mail is not actually handled locally: the mail is sent to the MAIL_HUB. If H is set to a value, localaddr (rule 5) sends the mail to the host identified by variable H if mail is addressed to a local user.

> WARNING The nullclient configuration creates the possibility of mail routing loops. If an alias or .forward file on the MAIL_HUB forwards mail back to the client, the client might send the mail right back to the MAIL_HUB, kicking off a mail loop. Don't forward mail from a MAIL_HUB to its clients. It is safest for the clients to download mail using a separate tool, such as IMAP.

## Configuring a Relay Client

The nullclient feature is a simple way to create a client-only Sendmail configuration.

Like many simple solutions, it lacks flexibility. With nullclient, SMART_HOST and MAIL_HUB are set to the same value. That might not be what you want. You may not even want to use a SMART_HOST and the MAIL_HUB. Two define commands can be used to build the client configuration the way you want it.

define(SMART_HOST, mailer:server) The SMART_HOST option allows you to identify the external server that should be used for outbound mail from the client. The optional mailer value can be used to specify the mailer used for relay mail to the external server. Easily, the relay mailer is used to relay mail to the external server if no SMART_HOST value is provided with the SMART_HOST option. The value provided to the SMART_HOST option is stored in variable S exactly as it is entered-i.e.,

mailer:server or just server.

define(MAIL_HUB, mailer:server) The MAIL_HUB option identifies the external server that the client uses for inbound mail. Again, an optional mailer can be specified, and if it is not, the relay mailer is used to relay mail to the server. The value specified for MAIL_HUB is written to variable H exactly as entered.

> **NOTE** In addition to add flexibility, an advantage of SMART_HOST and MAIL_HUB as opposed to nullclient is that you can select the mailer you want to. If you use the mailer:server format with nullclient, the mailer:server value is written to S, H, and M, creating an invalid masquerade value.

When MAIL_HUB is used, for all local users are sent to the MAIL_HUB. This might not be what you want. For example, you might not want to send mail addressed to root of the MAIL_HUB for delivery. Use the LOCAL_USER macro to identify local users whose mail should be delivered locally even when a MAIL_HUB is defined. As an example, the following command prevents mail addressed to root from being sent to the MAIL_HUB for delivery:

LOCAL_USER(root)

The LOCAL_USER macro adds values to class L. There is no macro that loads class L from a file. If you want to load a class from you, use a sendmail.cf F command to do so. Assume that you have a file named /etc/mail/10local-user that contains a list of users whose mail should not be sent to the MAIL_HUB. You could add the following to your macro configuration to load the file into class L:

LOCAL_CONFIG

FL/etc/mail/1local-users

Conversely, there may be users whose mail should be sent to the MAIL_HUB even though those are not really local users. The idea of "apparently local" is.

## Special Configurations

When Sendmail is asked to deliver, it checks if the address is local. If it is, the mail is delivered locally. If it is not, the mail is sent to a relay server. The relay server must decide if it wants to handle the mail and how to deliver it once it accepts it. Configuring a system as a relay server has become an issue of security and span control. How will you cover the server side of relaying in Chapter 11.

## In Sum

This chapter concludes Part 3, "Advanced Configuration," with a look at some of the special configurations that can be used to customize Sendmail for your environment. Most of the configurations we looked at in this chapter fit as well as the DOMAIN file because they relate to something that is special about your domain or network.
