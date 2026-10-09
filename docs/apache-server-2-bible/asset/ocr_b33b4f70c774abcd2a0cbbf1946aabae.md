```
```
# # Domain Configuration for www.vhost1.com
#
<VirtualHost www.vhost1.com>
ServerName www.vhost1.com
ServerAdmin webmaster@vhost1.com
DocumentRoot /tmp/vhost1/htdocs
ScriptAlias /cgi-bin/ /tmp/vhost1/cgi-bin/
ErrorLog logs/www.vhost1.com.error.log
TransferLog logs/www.vhost1.com.access.log
</VirtualHost>
#
# End of Domain Configuration for www.vhost1.com
#
```
```

This is the <VirtualHost> configuration that the makesite script creates.

> Tip | If you are creating a name-virtual host for the first time, make sure you add NameVirtualHost IP_Address as the last line in the httpd.conf file before running makesite script for the first time.

Also check the /etc/named.conf file; you should see the following:

```
```
// vhost1.com was created on 2001-04-25-17-25
zone "vhost1.com" {
type master;
file "vhost1.zone";
};
```
```

As you can see, the script created the appropriate zone configuration information for the virtual host. You can find the DNS zone information in /var/named/vhostl.zone file, which shows:

```
```
@       IN  SOA vhost1.com. hostmaster.vhost1.com. (
                20010425000         ; serial YYYYMMDDXXX
                7200                ; refresh
                3600                ; (1 hour) retry
                1728000             ; (20 days) expire
                3600)              ; (1 hour) minimal TTL
: Name Servers
IN  NS  ns1.domain.com.
IN  NS  ns2.domain.com.
IN  MX  10 mail.domain.com.
: CNAME records
www   IN  CNAME  www.domain.com.
```
```