# Listing 8-8 The named.template File

```
@ IN SOA <DOMAIN>. hostmaster.<DOMAIN>. (
    <SERIAL> ; serial YYYYMMDDXXX
    7200     ; refresh
    3600     ; (1 hour) retry
    1728000  ; (20 days) expire
    3600)    ; (1 hour) minimal TTL

; Name Servers
IN NS ns.nitec.com.
IN MX 10 mail.nitec.com.

; CNAME records
www IN CNAME www.nitec.com.
```

The makesite script reads this template and replaces the <DOMAIN> and <SERIAL> tags with appropriate information. Because the idea is to create a virtual Web site with a proper DNS configuration, no A records need to be created. For example, the preceding configuration states that the www.<DOMAIN> (for instance, www.newdomain.com) is an alias of www.nitec.com. Using A records makes maintenance of many virtual Web sites time-consuming if IP changes are required. Thus, I use the CNAME record, so that if www.nitec.com host's IP needs to be changed, the virtual domain's configuration files do not need to be modified. Listing 8-9 shows the httpd.template file used to create the Apache server configuration.

# Listing 8-9 The httpd.template File

```
#
# Domain Configuration for <WWW-SITE>
#

<VirtualHost <WWW-SITE>>
    ServerName <WWW-SITE>
    ServerAdmin webmaster@<DOMAIN>
```