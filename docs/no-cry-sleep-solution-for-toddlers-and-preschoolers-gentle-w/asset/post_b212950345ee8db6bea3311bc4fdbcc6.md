
## Virtual Hosting on Apache

Virtual hosting allows the Apache Web server to host multiple Web sites as part of its own. In effect, the server can act as several servers, each hosted Web site appearing separate to outside users. Apache supports both IP address-based and name-based virtual hosting. IP address-based virtual hosts use valid registered IP addresses, whereas name-based virtual hosts use fully qualified domain addresses. These domain addresses are provided by the host header from the requesting browser. The server can then determine the correct virtual host to use on the basis of the domain name alone. Note that SSL servers require IP virtual hosting. See httpd.apache.org for more information.

## IP Address-Based Virtual Hosts

In the IP address-based virtual hosting method, your server must have a different IP address for each virtual host. The IP address you use is already set up to reference your system. Network system administration operations can set up your machine to support several IP addresses. Your machine could have separate physical network connections for each one, or a particular connection could be configured to listen for several IP addresses at once. In effect, any of the IP addresses can access your system.

You can configure Apache to run a separate daemon for each virtual host, separately listening for each IP address, or you can have a single daemon running that listens for requests for all the virtual hosts. To set up a single daemon to manage all virtual hosts, use VirtualHost directives. To set up a separate daemon for each host, also use the Listen directive.

A VirtualHost directive block must be set up for each virtual host. Within each VirtualHost block, you place the appropriate directives for accessing a host. You should have ServerAdmin, ServerName, DocumentRoot, and TransferLog directives specifying the particular values for that host. You can use any directive within a VirtualHost block, except for ServerType (1.3), StartServers, MaxSpareServers, MinSpareServers, MaxRequestsPerChild, Listen, PidFile, TypesConfig, ServerRoot, and NameVirtualHost.

Although you can use domain names for the address in the VirtualHost directive, using the actual IP address is preferable. This way, you are not dependent on your domain name service to make the correct domain name associations. Be sure to leave an IP address for your main server. If you use all the available IP addresses for your machine for virtual hosts, you can no longer access your main server. You could, of course, reconfigure your main server as a virtual host. The following example shows two IP-based virtual hosts blocks: one using an IP address, and the other a domain name that associates with an IP address:

```
<VirtualHost 192.168.1.23>
ServerAdmin webmaster@mail.mypics.com
DocumentRoot /groups/mypics/html
ServerName www.mypics.com
ErrorLog /groups/mypics/logs/error_log
....
</VirtualHost>
```

```
<VirtualHost www.myproj.org>
ServerAdmin webmaster@mail.myproj.org
DocumentRoot /groups/myproj/html
ServerName www.myproj.org
ErrorLog /groups/myproj/logs/error_log
...
</VirtualHost>
```

## Name-Based Virtual Hosts

With IP-based virtual hosting, you are limited to the number of IP addresses your system supports. With name-based virtual hosting, you can support any number of virtual hosts using no additional IP addresses. With only a single IP address for your machine, you can still support an unlimited number of virtual hosts. Such a capability is made possible by the HTTP/1.1 protocol, which lets a server identify the name by which it is being accessed. This method requires the client, the remote user, to use a browser that supports the HTTP/1.1 protocol, as current browsers do (though older ones may not). A browser using such a protocol can send a host header specifying the particular host to use on a machine.

To implement name-based virtual hosting, use a VirtualHost directive for each host and a NameVirtualHost directive to specify the IP address you want to use for the virtual hosts. If your system has only one IP address, you need to use that address. Within the VirtualHost directives, you use the ServerName directive to specify the domain name you want to use for that host. Using ServerName to specify the domain name is important to avoid a DNS lookup. A DNS lookup failure disables the virtual host. The VirtualHost directives each take the same IP address specified in the NameVirtualHost directive as their argument. You use Apache directives within the VirtualHost blocks to configure each host separately. Name-based virtual hosting uses the domain name address specified in a host header to determine the virtual host to use. If no such information exists, the first host is used as the default. The following example implements two name-based virtual hosts.

Here, www.mypics.com and www.myproj.org are implemented as name-based virtual hosts instead of IP-based hosts:

```
ServerName turtle.mytrek.com

NameVirtualHost 192.168.1.5

<VirtualHost 192.168.1.5>
  ServerName www.mypics.com
  ServerAdmin webmaster@mail.mypics.com
  DocumentRoot /var/www/mypics/html
  ErrorLog /var/www/mypics/logs/error_log
  ...
</VirtualHost>

<VirtualHost 192.168.1.5>
  ServerName www.myproj.org
  ServerAdmin webmaster@mail.myproj.org
  DocumentRoot /var/www/myproj/html
  ErrorLog /var/www/myproj/logs/error_log
  ...
</VirtualHost>
```
