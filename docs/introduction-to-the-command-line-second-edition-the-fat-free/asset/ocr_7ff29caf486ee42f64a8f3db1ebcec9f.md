# # whois

**Purpose:** Lookup domain name registry information in the WHOIS database.

**Usage syntax:** whois [OPTIONS] [DOMAIN]

```
$ whois google.com
Registrar:
    Dns Admin
    Google Inc.
    Please contact contact-admin@google.com
    1600 Amphitheatre Parkway
    Mountain View CA 94043
    dns-admin@google.com +1.650\*\*\*\*\*\* Fax: +1.650\*\*\*\*\*\*
    Domain Name: google.com
    Registrar Name: Markmonitor.com
    Registrar Whois: whois.markmonitor.com
    Registrar Homepage: http://www.markmonitor.com
    Created on.............: 1997-09-15.
    Expires on.............: 2011-09-13.
    Record last updated on..: 2008-06-08.
    Domain servers in listed order:
    ns1.google.com ns2.google.com
...
```

Using the whois command to query domain information

The **whois** command is used to query an internet registry and display information about the registrant of a domain name. In the above example, the **whois** command displays information for google.com.

> *You can also use the **whois** command to lookup information about an IP address by executing **whois [IP ADDRESS]**.*

Common usage examples:

+   - `whois [DOMAIN]` Display information about a domain's registrant
+   - `whois [IP ADDRESS]` Display information about the owner of an IP address