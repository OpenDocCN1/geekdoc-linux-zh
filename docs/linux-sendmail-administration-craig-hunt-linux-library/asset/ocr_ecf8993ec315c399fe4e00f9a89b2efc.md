# Configuring a Relay Client 263

The nullclient feature is a simple way to create a client-only Sendmail configuration.
Like many simple solutions, it lacks flexibility. With nullclient, SMART_HOST and MAIL_HUB are set to the same value. That might not be what you want. You may not want to use both SMART_HOST and a MAIL_HUB. Two define commands can be used to build the client configuration the way you want.

define(SMART_HOST, mailer:server) The SMART_HOST option allows you to identify the external server that should be used for outbound mail from the client. The optional mailer value can be used to specify the mailer to relay mail to the external server. Simply enough, the relay mailer is used to relay mail to the external server if no mailer value is used with the SMART_HOST option. The value provided to the SMART_HOST option is stored in variable S as it is entered—i.e., mailer:server or just server.

define(MAIL_HUB, mailer:server) The MAIL_HUB option identifies the external server that the client uses for inbound mail. Again, an optional mailer can be specified, and if it isn't, the relay mailer is used to relay mail to the server. The value specified for MAIL_HUB is written to variable H exactly as entered.

> **NOTE** In addition to flexibility, an advantage of using SMART_HOST and MAIL_HUB as opposed to nullclient is that you can select the mailer to use. If you use the mailer:server format with nullclient, the mailer:server value is written to S, H, and M, creating an invalid masquerade value.

When MAIL_HUB is used, for all local users is set to the MAIL_HUB. This might not be what you want. For example, you might not want to send mail addressed to root to the MAIL_HUB for delivery. Use the LOCAL_USER macro to identify local users whose mail should be delivered locally even when a MAIL_HUB is defined. As an example, the following command prevents mail addressed to root from being sent to the MAIL_HUB for delivery:

```
LOCAL_USER(root)
```

The LOCAL_USER macro adds values to class L. There is no macro that loads class L from a file. To load class L from a file, use a sendmail -cf command to do so. Assume that you have a file named /etc/mail/local-user that contains a list of users whose mail should not be sent to the MAIL_HUB. You could add the following to your macro configuration to load the file into class L:

```
LOCAL_CONFIG
```

```
FL/etc/mail/local-users
```

Conversely, there may be users whose mail should be sent to the MAIL_HUB even though those users are not really local users. The idea of “apparently local” users requires some

![](bbox=[0.913, 0.258, 0.984, 0.542])