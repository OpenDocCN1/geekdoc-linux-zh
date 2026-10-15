# virtusertable feature

The virtusertable feature supports domain aliasing for incoming mail. This feature allows multiple virtual domains to be hosted on one machine and is used frequently at web hosting sites. The key field of the table contains either an email address (user@host.domain) or a domain specification (@domain). The value field is a local or external email address. If the key is a domain, the value can either pass the user field along as the variable %1 or route the mail to a different user. Here are some examples:

| Key | Value |
|---|---|
| @appliedtrust.com | %1@atrust.com |
| unix@book.admin.com | sa-book-authors@atrust.com |
| linux@book.admin.com | sa-book-authors@atrust.com |
| webmaster@example.com | billy.q.zakowski@colorado.edu |
| info@testdomain.net | aussername@hotmail.com |

All the host keys on the left side of the data mappings must be listed in the **cw** file, **/etc/mail/local-host-names**, or be included in the VIRTUSER_DOMAIN_LIST. If they are not, **sendmail** will not know to accept the mail locally and will try to find the destination host on the Internet. But DNS MX records will point **sendmail** back to this same server and you will get a “local configuration error” message in the resulting bounce message. Unfortunately, **sendmail** cannot tell that the error message for this instance should really be “virtusertable key not in cw file.”

# ldap_routing feature

LDAP, the Lightweight Directory Access Protocol, can be a source of data for aliases or mail routing information as well general tabular data as described earlier. The **cf/README** file has a long section on LDAP with lots of examples.

To use LDAP in this way, you must have built **sendmail** to include LDAP support. In your **.mc** file, add the lines

```
define(`confLDAP_DEFAULT_SPEC', `-h server -b searchbase')
FEATURE(ldap_routing)
LDAPROUTE_DOMAIN(`my_domain')
```

Those lines tell **sendmail** that you want to use an LDAP database to route incoming mail addressed to the specified domain. The LDAP_DEFAULT_SPEC option identifies the LDAP server and the LDAP basename for searches. LDAP uses port 389 unless you specify a different port by adding **-p ldap_port** to the define.

**sendmail** uses the values of two tags in the LDAP database:

+   - mailLocalAddress for the addressee on incoming mail
+   - mailRoutingAddress for the destination to which email should be sent

**sendmail** also supports the tag mailHost, which, if present, routes mail to the MX-designated mail handler for the specified host. The recipient address remains the value of the mailRoutingAddress tag.