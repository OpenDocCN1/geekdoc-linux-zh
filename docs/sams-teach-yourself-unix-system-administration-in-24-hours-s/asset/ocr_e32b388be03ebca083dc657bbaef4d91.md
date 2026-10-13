```
```
Compiled with: LDAPMAP MAP_REGEX LOG MATCHGECOS MIME7TO8 MIME8TO7
NAMED_BIND NETINET NETINET6 NETUNIX NEWDB NIS QUEUE SASL SCANF
SMTP TCPWRAPPERS USERDB
Invalid operation mode g

========== SYSTEM IDENTITY (after readcf) ==========
(short domain name) $w = staging
(canonical domain name) $j = staging.intuitive.com
(subdomain name) $m = intuitive.com
(node name) $k = staging.intuitive.com
============================================
```
```

Pleasantly, this Red Hat installation is running a recent version of sendmail (it's identified in the first line: 8.11.6).

The very same command run on Mac OS X reveals the following:

```
```
# sendmail -bt -d0.1 < /dev/null
Version 8.10.2
Compiled with: MAP_REGEX LOG MATCHGECOS MIME7TO8 MIME8TO7 NAMED_BIND
NETINET NETINFO NETISO NETUNIX NEWDB NIS QUEUE SCANF SMTP
USERDB XDEBUG

/etc/mail/sendmail.cf: line 81: fileclass: cannot open
->/etc/mail/local-host-names: Group writable directory

========== SYSTEM IDENTITY (after readcf) ==========
(short domain name) $w = dsl-132
(canonical domain name) $j = dsl-132.dsldesigns.net
(subdomain name) $m = dsldesigns.net
(node name) $k = dsl-132.dsldesigns.net
============================================

ADDRESS TEST MODE (ruleset 3 NOT automatically invoked)
Enter <ruleset> <address>
```
```

And on Solaris 8:

```
```
# /usr/lib/sendmail -bt -d0.1 < /dev/null
Version 8.10.2Sun
Compiled with: LDAPMAP MAP_REGEX LOG MATCHGECOS MIME7TO8 MIME8TO7
NAMED_BIND NDBM NETINET NETINET6 NETUNIX NEWDB NIS NISPLUS
QUEUE SCANF SMTP USERDB XDEBUG

========== SYSTEM IDENTITY (after readcf) ==========
(short domain name) $w = solaris
(canonical domain name) $j = solaris.dsldesigns.net
(subdomain name) $m = dsldesigns.net
(node name) $k = solaris.dsldesigns.net
============================================

ADDRESS TEST MODE (ruleset 3 NOT automatically invoked)
Enter <ruleset> <address>
```
```