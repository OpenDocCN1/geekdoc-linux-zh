# Chapter 9 Special m4 Configurations

explanation. When Sendmail is asked to deliver a mail to an address that contains a user but no host post, it assumes the name of a local user. It verifies this through the aliasing process by checking whether or not the name is a local login or a valid alias. If it is not one of these, the name is not considered local and is rejected. The name appared to be local but wasn't—it was an apparently local name. It is possible to configure Sendmail to send mail to apparently local users to a relay server. Use the USER_RELAY macro to define the server if you want to do this. The following command would forward all apparently local users to the server wren.forebirds.org for processing:

+   LUSER_RELAY(wren.forebirds.org).

LUSER_RELAY is most useful in an organization where every user has a unique-name. When that is the case, the mail can be addressed to the unique username of any user in the entire organization without adding the host part of the address. The Sendmail client detects that the address is apparently local, and sends the mail to the LUSER_RELAY. The relay server must now know how to deliver the mail to the correct user.

One other that you will occasionally see discussed for local mail relay is the LOCAL_RELAY macro. You should ignore it: it is a deprecated method that has been superseded by the MAIL_HUB macro. LOCAL_RELAY should not be used in your configuration.

Finally, there are special relay servers for non-SMTP. These are:

```
define(UUCP_RELAY, mailer:server) The server is the name of the system that handles UUCP mail for all UUCP sites that are not directly connected to the local host. The mailer defaults to relay. It is very common to send UUCP mail from the client to the server via SMTP, which is the protocol used by the relay mail. The server then forwards the mail through UUCP. The argument provided to the UUCP_RELAY option is stored in the sendmail.cf variable Y.
```

```
define(FAX_RELAY, mailer:server) The FAX_RELAY option identifies the server used to deliver mail addressed to the pseudo-domain .FAX , which is obviously an external fax server. With this option, users can address mail to a fax machine by using the syntax provided the external fax server and .FAX domain is the name of the external fax server and mailer is the mailer used to reach that server. mailer defaults to relay. The argument of the FAX_RELAY option is stored in the sendmail.cf variable F.
```

```
define(DECNET_RELAY, mailer:server) The DECNET_RELAY option identifies the mail gateway to a DECNET network. DECNET is an outdated network that was used by Digital Equipment corporation mini-computers. The argument of the DECNET_RELAY option is stored in the sendmail.cf variable C.
```