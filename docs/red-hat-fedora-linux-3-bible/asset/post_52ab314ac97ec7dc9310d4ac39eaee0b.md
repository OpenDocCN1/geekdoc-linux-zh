
## Getting a domain name

For people to be able to send mail to the users on your mail server, you must have your own domain name. Chapter 25 describes how to get your own domain names and set up a DNS server. The critical issue for your mail server is to make sure that the MX record for your domain on the DNS server points to the address of your mail server.

## Configuring basic sendmail settings (sendmail.mc)

Much of the configuration of your sendmail server comes from information in your `/etc/mail/sendmail.mc` file. Because this file sets sendmail default values that can be used in most cases, you may not have to do much with `sendmail.mc`. However, I recommend you step through this section so you understand how your mail server is configured.

Changes you make to the `sendmail.mc` file do not immediately take effect. First you must compile the `sendmail.mc` settings to generate the `/etc/mail/sendmail.cf` file. I describe how to do that in the "Starting sendmail and generating database files" section.

The resulting `/etc/mail/sendmail.cf` file contains over 1,700 lines of settings and comments that are used to direct the behavior of your sendmail daemon. The m4 macros you use in the `sendmail.mc` file are different from the resulting settings in the `sendmail.cf` file.

To find out which macros to use for a setting you find in the `sendmail.cf` file, refer to the `/usr/share/doc/sendmail/README.cf` file. If you are interested in details on the contents of your `sendmail.cf` file, I have included an exhaustive description of sendmail.cf at the Red Hat Linux Bible Web site: www.wiley.com/redhatarabible.

> **CAUTION:** Because of the way sendmail is configured in Fedora, you should not directly modify the `sendmail.cf` file. The `sendmail.cf` file is regenerated automatically when sendmail restarts if `sendmail.mc` changes. As a result, any modifications made directly to `sendmail.cf` will be lost.

The following code samples are from the `/etc/mail/sendmail.mc` file that accompanies the Fedora version of sendmail.

> **NOTE:** Lines that begin with `dnl` (delete to new line) in the `sendmail.mc` file are comment lines. In most cases, I have left them out in the examples shown.

```
divert(-1)dnl
include(`/usr/share/sendmail-cf/m4/cf.m4')dnl
VERSIONID(`setup for Red Hat Linux')dnl
OSTYPE(`linux')dnl
```

The first few lines of the `sendmail.mc` file do some housekeeping. The `divert` line removes extra output when the configuration file is generated. The `include` line causes rule sets needed by sendmail to be included. The `VERSIONID` line identifies the configuration file as being for Red Hat Linux systems, such as Fedora (though this setting is not checked, so it could be anything you like). The `OSTYPE`, however, must be set to `linux` to get the proper location of files needed by sendmail.

```
dnl define(`SMART_HOST',`smtp.your.provider')
```

By default, the sendmail daemon tries to send your outgoing e-mails directly to the mail server to which they are addressed. If you want all e-mail to be relayed through a particular mail server instead, you can remove the comment `dnl`, which stands for “delete to new line” from the `SMART_HOST` line above. Then, change `smtp.your.provider` to the fully qualified domain name of the mail server you want to use. Of course, you need to be sure that the `SMART_HOST` you define will accept relays from your mail server.

```
define(`confDEF_USER_ID',`8:12')dnl
```

Instead of running as the root user, the daemon runs as the mail user (UID 8) and mail group (GID 12), based on the `confDEF_USER_ID` line set previously. This is a good policy, since it prevents someone who might compromise your mail server from gaining root access to your machine.

```
dnl define(`confAUTO_REBUILD')dnl
define(`confTO_CONNECT', `1m')dnl
```

If you remove `dnl`, the `confAUTO_REBUILD` line will tell sendmail to automatically rebuild the aliases database, if necessary. The `confTO_CONNECT` line sets the time sendmail will wait for an initial connection to complete to one minute (1m).

```
define(`confTRY_NULL_MX_LIST',true)dnl
define(`confDONT_PROBE_INTERFACES',true)dnl
```

With `confTRY_NULL_MX_LIST` true, if a receiving server is the best mail exchange (MX) for a host, try connecting to that host directly. If `confDONT_PROBE_INTERFACES` is true, the sendmail daemon will not insert local network interfaces into the list of known equivalent addresses.

```
define(`PROCMAIL_MAILER_PATH',`/usr/bin/procmail')dnl
dnl define(`ALIAS_FILE',`/etc/aliases')dnl
dnl define(`STATUS_FILE',`/var/log/mail/statistics')dnl
```

The next three lines (`PROCMAIL_MAILER_PATH`, `ALIAS_FILE`, and `STATUS_FILE`) set locations for the program that distributes incoming mail (`procmail`, by default), the mail aliases file, and the mail statistics file, respectively.

```
define(`UUCP_MAILER_MAX', `2000000')dnl
define(`confUSERDB_SPEC',`/etc/mail/userdb.db')dnl
define(`confPRIVACY_FLAGS', `authwarnings,noverify,noexpn,restrictqrun')dnl
define(`confAUTH_OPTIONS', `A')dnl
```

The `UUCP_MAILER_MAX` line sets the maximum size (in bytes) for messages received by the UUCP mailer. The `confUSERDB_SPEC` line sets the location of the user database (where you can override the default mail server for specific users). The `confPRIVACY_FLAGS` line causes sendmail to insist on certain mail protocols. For example, `authwarnings` causes `X-Authentication-Warning` headers to be used and noted in log files. The `noverify` and `noexpn` settings prevent those services from being requested. The `restrictqrun` option prevents the `-q` option to sendmail.

```
dnl define(`confAUTH_OPTIONS', `A p')dnl
dnl TRUST_AUTH_MECH(`EXTERNAL DIGEST-MD5 CRAM-MD5 LOGIN PLAIN')dnl
dnl define(`confAUTH_MECHANISMS', `EXTERNAL GSSAPI DIGEST-MD5 CRAM-MD5
   LOGIN PLAIN')dnl
dnl define(`confCACERT_PATH', `/usr/share/ssl/certs')
dnl define(`confCACERT',`/usr/share/ssl/certs/ca-bundle.crt')
dnl define(`confSERVER_CERT','/usr/share/ssl/certs/sendmail.pem')
dnl define(`confSERVER_KEY','/usr/share/ssl/certs/sendmail.key')
dnl define(`confDONT_BLAME_SENDMAIL','groupreadablekeyfile')dnl
```

Some of the group of lines just shown that begin with `dnl` (so they are commented out) can be uncommented (remove the initial `dnl`) to provide certain features. Others are set explicitly. The `confAUTH_OPTIONS` line can be used to set options used with SMTP authentication. This example (with a and p options) would allow authenticated users with plain text logins to send mail. The `TRUST_AUTH_MECH` line causes sendmail to allow authentication mechanisms other than plain passwords (if `dnl` was removed). The `confAUTH_MECHANISMS` line can configure the types of authentication mechanisms that can be used (if `dnl` are removed). The next few lines above set the location of the certificates directory for sendmail to `/usr/share/ssl/certs`, then identify different files in that directory that hold the certificates and keys needed for authentication. The `confDONT_BLAME_SENDMAIL` line should be uncommented if the key file needs to be readable by applications other than sendmail. (Normally, you would not want the file to be readable by everyone.)

```
dnl define(`confTO_QUEUEWARN', `4h')dnl
dnl define(`confTO_QUEUERETURN', `5d')dnl
dnl define(`confREFUSE_LA', `32')dnl
dnl define(`confREFUSE_LA', `18')dnl
dnl define(`confTO_IDENT', `0')dnl
```

The commented lines above actually show the default values set for certain timeout conditions. You can remove comments and change these values if you like. The `confTO_QUEUEWARN` option sets how long after delivery of a message has been deferred to send a warning message to the sender. Four hours (4h) is the default. The `confTO_QUEUERETURN` option sets how long before an undeliverable message is returned. The `confREFUSE_LA` and `confREFUSE_LA` options set the system load average levels at which mail received is queued or refused, respectively. The `confTO_IDENT` option sets the timeout when waiting for a response to an IDENT query to be received (by default it is 0, which means no timeout).
