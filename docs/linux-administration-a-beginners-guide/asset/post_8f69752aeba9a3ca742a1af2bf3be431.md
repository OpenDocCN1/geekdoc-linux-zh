
**RELAY_ENTIRE_DOMAIN** Sendmail's default behavior is to relay mail only from hosts listed in the access database (discussed later). By using this feature, you allow any host within your domain to relay through you.

**RELAY_BASED_ON_MX** This feature tells Sendmail to look up the DNS MX record of a host that is asking to relay through you. If Sendmail finds that the host's MX record is the same host that Sendmail is running on, the message will be accepted for relaying.

**ACCEPT_UNQUALIFIED_SENDERS** Normally, Sendmail refuses mail from unqualified e-mail addresses that are unqualified. For example, mail from ssh@localhost.com is acceptable, but mail from ssh@localhost.com is not. Using this feature tells Sendmail to not require that sender e-mail addresses be qualified.

**ACCEPT_UNRESOLVABLE_DOMAINS** Sendmail defaults to requiring that the sender's domain name be resolvable via DNS. This keeps people from forging e-mail from non-existent domains. If your site has a limited view of the Internet DNS name space for some reason (such as if you're behind a firewall), you will want to tell Sendmail to accept messages from unresolvable domains using this feature.

**ACCESS_DB** This feature enables the access database, which allows you to specify whether you want to accept, reject, drop, or reject with a special code, all of your incoming e-mail, based on source domain or e-mail address. We explore the configuration file for this feature in greater detail later on in this chapter when we discuss spam control.

**BLACKLIST_RECIPIENTS** There are some users who should never receive e-mail, such as nobody, bin, or lp. You can blacklist these users so that they cannot receive e-mail by using this feature in combination with the access_db feature.

The way that blacklist configuration works with the access_db is discussed in the spam control section.

## Configurable Parameters

Sendmail offers a number of configurable parameters for its features. In this section we step through these parameters and explain what they are used for and their default values. You'll find that for the most part, the defaults are perfectly good, and you won't need to change anything.

You can see the very long list of configurable options in the cf/README file; however many of those options are so incredibly rarely used, you'll probably never forget they are there when you're done with this chapter. Because of that, Table 15-1 starts off the most common options.

> NOTE: Some of the parameters in the configuration file represent time values. The format of these values is a number followed by a letter, where the letter is either s for seconds, m for minutes, h for hours, or d for days. For example, 10m is 10 minutes, 3d is 3 days, and so on.

**Table 15-1. Sendmail's Most Common Configurable Parameters**

| Option Name | Description | Default |
| --- | --- | --- |
| confMAILER_NAME | The name used for internally generated mail (typically for error messages for returned mail). | MAILER-DAEMON |
| confDOMAIN_NAME | Your domain name. You should set this option only if Sendmail cannot determine your domain name by itself. | No default |
| confCW_FILE | The full path to the file containing host names that the server may be known as (see the use_cw_file feature). | /etc/sendmail.cw |
| confCT_FILE | The full path to the file containing trusted users (see the use_ct_file feature). | /etc/sendmail.ct |
| confCR_FILE | The full path to the relay-domains file. This is the list of domains Sendmail will relay for. (You should use the access_db feature instead.) | /etc/mail/relay-domains |
| confALIAS_WAIT | When the mail aliases file is updated, it must be converted to the internal database format with the newaliases command. This parameter tells Sendmail how long to wait for newaliases to run before rebuilding the database itself. | 10 minutes (10m) |
| confMIN_FREE_BLOCKS | The number of free blocks the mail storage partition must have for Sendmail to accept new messages. This option allows Sendmail to protect the system from sudden bursts of e-mail. | 100 blocks, where 1 block under Linux is equal to 1K |
| confMAX_MESSAGE_SIZE | The maximum message size (in bytes) that Sendmail will accept. | Infinite |
| ConfAUTO_REBUILD | Specifies if Sendmail should automatically rebuild the aliases database if needed. | False |
| ConfLOG_LEVEL | Specifies Sendmail's level of logging. The higher the level number, the more logging performed. The level codes are as follows: <br>0: Minimal logging <br>1: Serious system failures and potential security problems <br>2: Lost communication (network problems) <br>3: Transient errors, malformed addresses, forward/include errors <br>4: Minor failures, out-of-date alias databases, connection rejections via check_rule sets <br>5: Message collection statistics <br>6: Creation of error messages, VERB and EXPN commands <br>7: Delivery failures (host or user unknown, and so on) <br>8: Successful deliveries and alias database rebuilds <br>9: Messages being deferred <br>10: Database expansion (aliases, forward, and user database lookups) <br>11: NFS errors and end-of-job processing <br>12: All SMTP connections <br>13: Bad user shells and files with improper permissions | Log level 9 |
| confME_TOO | Determines whether, when a message is sent to an alias that has the sender as a member of the list (such as the user hcd sends a message to management, which expands to the users hcd,julia,eco), the message should be sent to the sender, too. | False (does not send message back to sender) |
| confTO_INITIAL | Timeout period Sendmail should wait when connecting to remote sites to send mail. | 5 minutes (5m) |
| confTO_IDENT | Timeout period Sendmail should wait when trying to identify the user name of someone trying to send mail to it via the IDENT protocol. | 30 seconds (30s) |
| confTO_QUEUEWARN | Timeout period before a user is told that her message being relayed through Sendmail is being deferred because the remote site cannot be contacted. | 4 hours (4h) |
| ConfSMTP_LOGIN_MSG | The greeting message sent to someone trying to connect to Sendmail. Some sites have taken to customizing this string so that remote sites don't know what kind of mail server is really being run. In essence, this is security through obscurity, where the underlying philosophy is, “Why tell them what you don't have to.” Just understand that obscuring the type of mail server does not mean a cracker will not get through if they are determined enough. | Host name of the server, the version of Sendmail, and the version of the Sendmail configuration file |
| confDOUBLE_BOUNCE_ADDRESS | If an error occurs, Sendmail delivers an e-mail notice to the site administrator. The site administrator is defined by this option. Most sites leave the default alone and use an alias to route messages to the system administrator. | Postmaster |

**Example:** To set the path for the procmail program to /usr/bin/procmail, we would use

```
define(`PROCMAIL_MAILER_PATH', `/usr/bin/procmail')
```

## A Complete Sample Configuration

Here is a complete .mc file:

```
OSTYPE(`linux')
define(`confAUTO_REBUILD')
define(`confFO_CONNECT', 'lm')
define(`confTRY_NULL_MX_LIST', true)
define(`PROCMAIL_MAILER_PATH', '/usr/bin/procmail')
FEATURE(`smrsh', '/usr/sbin/smrsh')
FEATURE(`virtusertable', /hash -o /etc/mail/virtusertable')
FEATURE(`redirect')
FEATURE(always_add_domain)
FEATURE(use_cw_file)
FEATURE(local_procmail)
MAILER(procmail)
MAILER(smtp)
FEATURE(`access_db')
FEATURE(`blacklist_recipients')
FEATURE(`accept_unresolvable_domains')
```

## Compiling Macros into a Configuration File

Once you have all of your macros put into an _mc file, you are ready to convert it into a complete configuration file that Sendmail can understand. The process is wonderfully straightforward.
