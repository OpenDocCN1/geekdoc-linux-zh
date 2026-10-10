# Part IV Networking

The confAUTH_OPTIONS line can be used to set options used with SMTP authentication. This example (with A and p options) would allow authenticated users with plaintext logins to send mail. The TRUST_AUTH_MECH line would cause Sendmail to allow authentication mechanisms other than plain passwords (if dn were removed). The confAUTH_MECHMS line can configure the types of authentication mechanisms that can be used (if dn were removed). The next few lines about set the location of the Certificates directory for Sendmail to /etc/pki/tls/certs, then identify different files in that directory that hold the certificates and keys needed for authentication. The confDONT_BLAME_SENDMAIL line should be uncommented if the key file needs to be readable by applications other than Sendmail. (Typically, you would not want the file to be readable by everyone.)

```
dn\| define(`confTO_QUEUEWARN', `4h')dn\|
\dn\| define(`confTO_QUEUERETURN', `5d')dn\|
\dn\| define(`confQUEUE_LA', `12')dn\|
\dn\| define(`confREFUSE_LA', `1B')dn\|
\ \define(`confTO_IDENT', `0')dn\|
```

The commented lines above actually show the default values set for certain time-out conditions. You can remove comments and change these values if you like. The confTO_QUEUEWARN option sets how long after delivery of a message has been deferred to send a warning message to the sender. Four hours (4h) is the default. The confTO_QUEUERETURN option sets how long before an undeliverable message is returned. The confQUEUE_LA and confREFUSE_LA options set the system load average levels at which mail received is queued or refused, respectively. The confTO\_IDENT option sets the time-out when waiting for a response to an IDENT query to be received (by default it is 0, which means no time-out).

```
FEATURE(`no_default_msa', `dn|')dn\|
FEATURE(`smrsh', `/usr/sbin/smrsh')dn\|
FEATURE(`mailertable', `hash -o /etc/mail/mailertable.db')dn\|
FEATURE(`virtusertable', `hash -o /etc/mail/virtusertable.db')dn\|
FEATURE(`redirect')dn\|
FEATURE(`always_add_domain')dn\|
FEATURE(`use_cw_file')dn\|
FEATURE(`use_ct_file')dn\|
FEATURE(`local\_procmail', `:procmail -t -Y -a $h -d $u')dn\|
FEATURE(`access_db', `hash T:IMPF; -o /etc/mail/access.db')dn\|
FEATURE(`blacklist_recipients')dn\|
```

The FEATURE macro is used to set some special Sendmail features. The no_default_msa feature tells Sendmail not to generate a default MSA daemon (which normally is set to listen on port 587). The smrsh feature defines /usr/sbin/smrsh as the simple shell used by Sendmail to receive commands. The mailertable and virtusertable options set the locations of the mailertable and virtusertable databases. The redirect option allows you to reject mail for users who have moved and provide new addresses. The always_add_domain option causes the local domain name to be added to the hostname on all delivered mail. The use_cw_file and use_ct_file options tell Sendmail to use the file /etc/mail/local-host-names for alternative