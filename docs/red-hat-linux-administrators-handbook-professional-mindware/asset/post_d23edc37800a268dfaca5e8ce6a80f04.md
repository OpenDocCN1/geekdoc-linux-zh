
rewrite: ruleset 198 returns: $@ local $@ kabilr @ nitec . com
rewrite: ruleset 0 returns: $@ local $@ kabilr @ nitec . com

The kabilr@nitec.com address is delivered using the local mailer.

Consider another example, in which you have the following `/etc/mail/domaintable` map:

```
ad-engine.com nitec.com
```

The preceding map routes all mail destined for ad-engine.com to nitec.com. The following example tests this map:

```
ADDRESS TEST MODE [ruleset 3 NOT automatically invoked]
Enter <ruleset> <address>
> 3,0 kabilr@nitec.com

rewrite: ruleset 3 input: kabilr @ nitec . com
rewrite: ruleset 96 input: kabilr @ nitec . com >
rewrite: ruleset 96 returns: kabilr < @ ad-engine . com >
rewrite: ruleset 3 returns: kabilr < @ ad-engine . com >
rewrite: ruleset 0 input: kabilr < @ ad-engine . com >
rewrite: ruleset 199 input: kabilr < @ ad-engine . com >
rewrite: ruleset 199 returns: kabilr < @ ad-engine . com >
rewrite: ruleset 98 input: kabilr < @ ad-engine . com >
rewrite: ruleset 98 returns: kabilr < @ ad-engine . com >
rewrite: ruleset 198 input: kabilr < @ ad-engine . com >
rewrite: ruleset 90 input: < ad-engine . com > kabilr < @ ad-engine . com >
rewrite: ruleset 90 input: ad-engine . com > kabilr < @ ad-engine . com >
rewrite: ruleset 90 returns: kabilr < @ ad-engine . com >
rewrite: ruleset 95 input: < kabilr < @ ad-engine . com >
rewrite: ruleset 95 returns: kabilr < @ ad-engine . com >
rewrite: ruleset 198 returns: $@ smtp $@ ad-engine . com . $: kabilr < @
ad-engine . com >
rewrite: ruleset 0 returns: $@ smtp $@ ad-engine . com . $: kabilr < @
ad-engine . com >
```

The address kabilr@nitec.com is rewritten as kabilr@ad-engine.com, and sendmail shows that it will deliver it via ESMTP (enhanced SMTP mailer, because ad-engine.com is not listed in `/etc/mail/sendmail.cw`. If it were, the preceding test would show the following output:

```
ADDRESS TEST MODE (ruleset 3 NOT automatically invoked)
Enter <ruleset> <address>
> 3,0 kabir@ad-engine.com

rewrite: ruleset     3  input: kabir @ ad-engine . com
rewrite: ruleset    96  input: kabir<@ ad-engine . com >
rewrite: ruleset    96 returns: kabir<@ ad-engine . com >
rewrite: ruleset     3  returns: kabir<@ ad-engine . com >
rewrite: ruleset     0  input: kabir<@ ad-engine . com >
rewrite: ruleset   199  input: kabir<@ ad-engine . com >
rewrite: ruleset   199  returns: kabir<@ ad-engine . com >
rewrite: ruleset    98  input: kabir<@ ad-engine . com >
rewrite: ruleset    98  returns: kabir<@ ad-engine . com >
rewrite: ruleset   198  input: kabir<@ ad-engine . com >
rewrite: ruleset   198  returns: $! local $: kabir
rewrite: ruleset     0  returns: $! local $: kabir
```

Notice that 3,0 is used as the *ruleset*, because ruleset 3 is involved in the domain table translation, and ruleset 0 is involved in parsing the address.

## Testing `/etc/mail/*` database files

Any time you modify `/etc/mail/access`, `/etc/mail/aliases`, `/etc/mail/domaintable`, `/etc/mail/mailertable`, `/etc/mail/virtuortable`, and similar files, make sure sendmail can perform lookups properly. For example, suppose you just created the following alias in the `/etc/mail/aliases` file:

```
root: kabir
```

After you run the *newaliases* command, find out whether sendmail can do appropriate alias lookups by running `sendmail -bt`. At the address test mode prompt, enter the following:

```
/map database name key
```

For example, to test the `/etc/mail/aliases` database for the alias `root`, I can run

```
/map aliases root
```

which shows the following output:

```
map_lookup: aliases (root) returns kabir
```

## Using sendmail to see the SMTP transaction verbosely

You can also use sendmail to see how it delivers a message to the destination. For example, the `-vt` option in the following command tells sendmail to be verbose and scan for To:, From:, Cc:, and Bcc: headers in the input:

```
sendmail -vt
```

After you run the preceding command, it waits for user input. At this point, you can enter something like this:

```
To: kabir@intevo.com
From: someone@somewhere.com
Subject: Testing sendmail

This is a test.
.
```

After you enter a short message, as shown here, press Ctrl+D to exit message entry mode. Sendmail then displays an SMTP transaction similar to the following:

```
kabir@intevo.com... Connecting to mail.intevo.com via esmtp...
220 wormhole.intevo.com ESMTP Sendmail 8.11.0/8.11.0;
Sun, 24 Nov 2001 19:57:00 -0500
>>> EHLO piasco.nitesc.com

250-wormhole.intevo.com Hello picao.nitec.com [206.171.50.50], pleased to meet you

250-EXPN

250-VERB

250-8BITMIME

250-SIZE

250-DSN

250-ONEX

250-ETRN

250-XUSR

250 HELP

>>> MAIL From:<kabilir@picao.nitec.com> SIZE=77

250 <kabilir@picao.nitec.com>... Sender ok

>>> RCPT To:<kabir@intevco.com>

250 <kabir@intevco.com>... Recipient ok

>>> DATA

354 Enter mail, end with "." on a line by itself

>>> .

250 TAAA16439 Message accepted for delivery

kabir@intevco.com... Sent

(TAAA16439 Message accepted for delivery)

Closing connection to mail.intevco.com.

>>> QUIT

221 wormhole.intevco.com closing connection
```

The lines that start with `>>>` are sent by the local sendmail server (picao.nitec.com) to the remote sendmail server (mail.intevco.com). This is very close to what I demonstrated earlier via a Telnet connection.

## Using the sendmail debug flag

Use the `-dX` option (where X is a debug level) along with `-bv` to see what action sendmail will take for a particular address. For example,

```
sendmail -bv -d0 kabir@nitec.com
```

produces the following output on my sendmail server:

```
Version 8.9.3
  Compiled with: MAP REGEX LOG MATCHGECOS MIME/8TO8
MIME8TO7 NAMED BIND NETINET NETUNIX NENDB NIS QUEUE SCANF
SMTP USERDB XDEBUG


========== SYSTEM IDENTITY (after readcf) ===========
(short domain name) $w = picao
(canonical domain name) $j = picao.nitac.com
(subdomain name) $m = nitac.com
(node name) $k = picao.nitac.com
========== SYSTEM IDENTITY (after readcf) ==========

kabir@nitac.com... deliverable: mailer local, user kabir
```

The `-d0` option causes sendmail to display various items of information about itself. The last line shows how sendmail will handle the given address. Specifying `-d` without any debug level number shows all the debugging information you'll ever want.

## Using a test configuration file

When you are modifying `sendmail.cf`, it is a good idea to create a test version of the `/etc/sendmail.cf` file and modify only the test copy, so that you don't lose any working configuration. Here is how you can test a new configuration:

1. Create a copy of `/etc/sendmail.cf` with a new name. For this example, call the test configuration `/etc/sendmail-test.cf`.
2. To run sendmail with your new test configuration file, use the `-C` option. For example, `/usr/sbin/sendmail -Csendmail-test.cf` uses `/etc/sendmail-test.cf`.
3. If you want to use a different queue (that is, other than `/var/spool/mqueue`) for the test configuration, use the `-OQ` option. For example, `/usr/sbin/sendmail -Csendmail-test.cf -OQ/var/spool/test-mqueue` uses the `/var/spool/test-mqueue` directory for the test configuration.

At this point, you should have sendmail configured as expected.

# Securing sendmail

Being one of the oldest mail servers, sendmail has had its share of security holes and blame. The current version of sendmail has been released with strict security in mind.

## Securing your configuration files

Beginning with version 8.11.x, sendmail has tightened the restrictions on configuration file permissions. For example, if I run `chmod -R 664 /etc/mail/*` to change the file permissions for the configuration files and then try to restart sendmail, I get the following error messages:

```
Starting sendmail: /etc/sendmail.c: line 93: fileclass:
cannot open /etc/mail/sendmail.cw: Group writable directory
```

```
WARNING: Group writable directory /etc/mail
/etc/mail/virtualuserstable.db: could not create: Permission
denied
```

```
WARNING: Group writable directory /etc/mail
/etc/mail/access.db: could not create: Permission denied
```

```
WARNING: Group writable directory /etc/mail
/etc/mail/domaintable.db: could not create: Permission
denied
```

```
WARNING: Group writable directory /etc/mail
/etc/mail/virtualuserstable.db: could not create: Permission
denied
```
