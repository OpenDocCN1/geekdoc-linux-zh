
```
FEATURE(`nullclient')
define(`MAIL_HUB', `mail.example.com')
```

where **mail.example.com** is the mail hub.

**local_procmail** This feature tells Sendmail to use Procmail as the local mailer. It can take up to three arguments: the path to Procmail (defaults to */usr/local/bin/procmail*), parameters to Procmail (defaults to *-X -a hostname -d username*), and flags for the mailer. Realistically speaking, all you need to do is specify the location of Procmail. Don’t worry about the parameters to Procmail unless you have a special need and have read the corresponding Procmail parameters. For example:

```
FEATURE(`local_procmail', `/usr/bin/procmail')
```

**smrsh** One of Sendmail’s security problems is that we, the people who configure it, make mistakes. One of the most common mistakes is setting up programs that can be run through an alias expansion in an insecure manner that can be exploited by remote users. We are effectively hitting ourselves in the foot with a hammer.
Sendmail tries to take away the hammer with the SendMail Restricted Shell (**smrsh**). It is a very simplified shell that has limited functionality, and therefore fewer things can be exploited because of a misconfiguration.
This feature accepts a parameter specifying where **smrsh** is located. If **smrsh** is in the */usr/sbin* directory, we would specify

```
FEATURE(`smrsh', `/usr/sbin/smrsh')
```

**promiscuous_relay** By default, Sendmail does not allow any site to relay mail through your site. This is done to protect you from spammers using your systems as a hopping point. If, for some really strange reason, you have to allow random people to relay through your mail server, you can use this feature.

![](img/ec2066d370d3af1a767664d36aa7ddfe_420_0.png)

*Allowing random people to relay through your server is a very bad idea. It opens up your site to denial of service (DoS) attacks, theft of bandwidth, and the nightmare of getting floods of e-mail coming from angry recipients of unsolicited e-mail. Before opening up your system like this, understand the implications!*

**relay_entire_domain** Sendmail’s default behavior is to relay mail only from hosts listed in the **access** database (discussed in “Spam Control: The access Database,” later in this module). By using this feature, you allow any host from within your domain to relay through you.

**relay_based_on_MX** This feature tells Sendmail to look up the DNS MX record of a host that is asking to relay through you. If Sendmail finds that the host’s MX record is the same host that Sendmail is running on, the message will be accepted for relaying.

**accept_unqualified_senders** Normally, Sendmail refuses mail from e-mail addresses that are unqualified. For example, mail from alicee@example.com is acceptable, but mail from alicee alone is not. Using this feature tells Sendmail *not* to require that sender e-mail addresses be qualified.

**accept_unresolvable_domains** Sendmail defaults to verifying that the sender’s domain name is resolvable via DNS. This keeps people from forging e-mail from nonexistent domains. If your site has a limited view of the Internet DNS namespace for some reason (such as if you’re behind a firewall), you will want to use this feature to tell Sendmail to accept messages from unresolvable domains.

**access_db** This feature enables the **access** database, which allows you to specify whether you want to accept, reject, drop, or reject with a special code all of your incoming e-mail, based on source domain or e-mail address. We explore the configuration file for this feature in greater detail in “Spam Control: The access Database” later in this module, when we discuss spam control.

**blacklist_recipients** There are some users who should never receive e-mail, such as **nobody**, **bin**, or **lp**. You can blacklist these users so that they cannot receive e-mail by using this feature in combination with the **access_db** feature.

The way blacklist configuration works with the **access_db** is discussed later in “Spam Control: The access Database.”

## Configurable Parameters

Sendmail offers a number of configurable parameters for its features. In this section, we review these parameters and explain what they are used for and their default values. You’ll find that, for the most part, the defaults are perfectly good, and you won’t need to change anything.

You can see the very long list of configurable options in the **README.cf** file. However, many of those options are so incredibly rarely used that you’ll probably even forget they are there when you’re done with this module. Because of that, Table 13-2 sticks to the most common options.

| Option Name | Description | Default |
|---|---|---|
| confMAILER_NAME | The name used for internally-generated mail (typically for error messages for returned mail). | MAILER-DAEMON |
| confDOMAIN_NAME | Your domain name. You should set this option only if Sendmail cannot determine your domain name by itself. | No default |
| confCW_FILE | The full path to the file containing host names that the server may be known as (see the use_cw file feature). | /etc/sendmail.cw |
| confCT_FILE | The full path to the file containing trusted users (see the use_ct file feature). | /etc/sendmail.ct |
| confCR_FILE | The full path to the relay-domains file. This is the list of domains for which Sendmail will relay. (You should use the access_db feature instead.) | /etc/mail/relay-domains |
| confALIAS_WAIT | When the mail aliases file is updated, it must be converted to the internal database format with the newaliases command. This parameter tells Sendmail how long to wait for newaliases to run before rebuilding the database itself. | 10 minutes (10m) |
| confMIN_FREE_BLOCKS | The number of free blocks the mail storage partition must have for Sendmail to accept new messages. This option allows Sendmail to protect the system from sudden bursts of e-mail. | 100 blocks, where 1 block (under Linux) is equal to 1K |
| confMAX_MESSAGE_SIZE | The maximum message size (in bytes) that Sendmail will accept. | Infinite |
| confAUTO_REBUILD | Specifies if Sendmail should automatically rebuild the aliases database if needed. | False |
| confLOG_LEVEL | Specifies Sendmail’s level of logging. The higher the level number, the more logging performed. The level codes are as follows: 0 Minimal logging 1 Serious system failures and potential security problems 2 Lost communication (network problems) 3 Transient errors, malformed addresses, forward/inclusion errors 4 Minor failures, out-of-date alias databases, connection rejections via check_rule sets 5 Message collection statistics 6 Creation of error messages, VRFY and EXPN commands 7 Delivery failures (host or user unknown, and so on) 8 Successful deliveries and alias database rebuilds 9 Messages being deferred 10 Database expansion (alias, forward, and user database lookups) 11 NIS errors and end-of-job processing 12 All SMTP connections 13 Bad user shells and files with improper permissions | Log level 9 |

Table 13-2 Sendmail’s Most Common Configurable Parameters

| Option Name | Description | Default |
| --- | --- | --- |
| **confME_TOO** | When a message is sent to an alias that has the sender as a member of the list (such as the user *hdrs* sends a message to *management*, which expands to the users *hd*, *julia*, and *cael*), this option determines whether the message should be sent to the sender, too. | False (does not send message back to sender) |
| **confTO_INITIAL** | Timeout period Sendmail should wait when connecting to remote sites to send mail. | 5 minutes (5*m) |
| **confTO_IDENT** | Timeout period Sendmail should wait when trying to identify the username of someone trying to send mail to it via the IDENT protocol. | 30 seconds (30*s) |
| **confTO_QUEUEWARN** | Timeout period before a user is told that her message being relayed through Sendmail is being deferred because the remote site cannot be contacted. | 4 hours (4*h) |
| **confSMTP_LOGIN_MSG** | The greeting message sent to someone trying to connect to Sendmail. Some sites have taken to customizing this string so that remote sites don't know what kind of mail server is really being run; in essence, this is security through obscurity, where the underlying philosophy is, "Why tell them what you don't have to?" Just understand that obscuring the type of mail server does not mean a cracker will not get through if they are determined enough. | Host name of the server, the version of Sendmail, and the version of the Sendmail configuration file |
| **confDOUBLE_BOUNCE_ADDRESS** | If an error occurs, Sendmail delivers an e-mail notice to the site administrator. The site administrator is defined by this option. Most sites leave the default alone and use an alias to route messages to the system administrator. | Postmaster |

Table 13-2 Sendmail's Most Common Configurable Parameters (continued)

![](img/ec2066d370d3af1a767664d36aa7ddfe_423_0.png)

Some of the parameters in the configuration file represent time values. The format of these values is a number followed by a letter, where the letter is either s for seconds, m for minutes, h for hours, or d for days. For example, **10m** is 10 minutes, **3d** is 3 days, and so on.

For example, to set the path for the Procmail program to `/usr/bin/procmail`, we would use

```
define(`PROCMAIL_MAILER_PATH', `/usr/bin/procmail')
```

## A Complete Sample Configuration

Here is the complete **.mc** file used to build the Red Hat & configuration:

```
VERSIONID(`linux_setup_for_Red_Hat_Linux')dnl
OSTYPE('linux')
define(`confDEF_USER_ID', `8:12')dnl
undefine(`UUCP_RELAY')dnl
undefine(`BITNET_RELAY')dnl
define(`confAUTO_REBUILD')dnl
define(`confTO_CONNECT', `1m')dnl
define(`confTRY_NULL_MX_LIST',true)dnl
```
