LDAP database entries support a wild card entry, @domain, that reroutes mail addressed to anyone at the specified domain (as was done in the virtusertable).

By default, mail addressed to user@host1.mydomain would first trigger a lookup on user@host1.mydomain. If that failed, sendmail would try @host1.mydomain but not user@mydomain. Including the line

```
LDAPROUTE_EQUIVALENT('host1.mydomain')
```

would also try the keys user@mydomain and @mydomain. This feature enables a single database to route mail at a complex site. You can also take the entries for the LDAPROUTE_EQUIVALENT clauses from a file, which makes the feature quite usable. The syntax for that form is

```
LDAPROUTE_EQUIVALENT_FILE('filename')
```

Additional arguments to the ldap_routing feature let you specify more details about the LDAP schema and control the handling of addressee names that have a +detail part. As always, see the cf/README file for exact details.

# Masquerading features

An email address is usually made up of a username, a host, and a domain, but many sites do not want the names of their hosts exposed on the Internet. The MASQUERADE_AS macro lets you specify a single identity for other machines to hide behind. All mail appears to emanate from the designated machine or domain. This is fine for regular users, but for debugging purposes, system users such as root should be excluded from the masquerade.

For example, the sequence

```
MASQUERADE_AS('atrust.com')
EXPOSED_USER('root')
EXPOSED_USER('Mailer-Daemon')
```

would stamp mail as coming from user@atrust.com unless it was sent by root or the mail system; in these cases, the mail would carry the name of the originating host. MASQUERADE_AS is just the tip of a vast masquerading iceberg that extends downward through a dozen variations and exceptions. The allmasquerade and masquerade_envelope features (in combination with MASQUERADE_AS) hide just the right amount of local info. See the cf/README for details.

# MAIL_HUB and SMART_HOST macros

Masquerading makes all mail appear to come from a single host or domain by rewriting the headers and, optionally, the envelope. But most sites will want all mail to actually come from (or go to) a single machine so that they can control the flow of viruses, spam, and company secrets. You can achieve this control with a combination of MX records in the DNS, the MAIL_HUB macro for incoming mail, and the SMART_HOST macro for outgoing mail.