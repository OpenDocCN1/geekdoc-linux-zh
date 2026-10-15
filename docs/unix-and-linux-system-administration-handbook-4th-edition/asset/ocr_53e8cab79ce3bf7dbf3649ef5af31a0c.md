# Content filtering

Postfix can use regular expressions to check the headers and bodies of email messages for contraband. It can also pass messages to other programs such as dedicated spam fighting tools or antivirus applications.

Header and body checks are performed in real time as messages are accepted through SMTP. Each regular expression that is checked invokes an action as specified in Table 20.25 on page 838 if the regex matches. For example, the line

```
header_checks = regexp/etc/postfix/header_checks
```

in main.cf along with the following line in /etc/postfix/header_checks

```
/^Subject: reject-me/ REJECT You asked for it
```

would reject any message whose subject started with "reject-me". Though regular expression support is always nice, it comes with caveats in the context of email processing. In particular, this is not an effective method of spam or virus filtering.

# Content filtering with amavisd

Industrial-strength virus filtering is usually implemented through amavisd (see page 769), a Perl program that interfaces mail server software with one or more antivirus applications. Such filters are configured with Postfix's content_filter parameter, which instructs Postfix to pass every incoming message once through the specified service. In addition to setting the content_filter parameter, you must modify some existing entries in the master.cf file and add some new ones.

Postfix and amavisd interact with each other by means of the standard SMTP and LMTP protocols. Postfix sends the mail to be analyzed by amavisd through LMTP. amavisd scans it and sends it back to Postfix through SMTP at an alternative port that's accessible only on the local machine and that has content-scanning disabled (thus avoiding a loop).

For mail coming in from the Internet, amavisd typically listens on port 10,024, and Postfix's back-door port is often 10,025. If we also process outgoing mail and want to differentiate it from incoming mail, we need a separate amavisd port for that—say, 10,026. The incoming mail can return to Postfix on the same return port as outgoing mail.

The configuration outlined below is a "post queue" setup that scans mail after it has been accepted into Postfix's queue. If you want to implement an in-line scanning setup, whereby the mail is scanned during the client's initial SMTP dialog, try the amavisd-milter helper tool, which lets you connect Postfix to amavisd as a milter.

On the amavisd side, make sure that amavisd's configuration contains lines such as the following. (This configuration uses separate ports for inbound and outbound messages.)