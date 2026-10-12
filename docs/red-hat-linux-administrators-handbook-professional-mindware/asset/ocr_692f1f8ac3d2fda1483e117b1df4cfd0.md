the `<VirtualHost>`. So, when configuring virtual hosts, you need to decide what changes need to be made in each of the virtual host configurations.

The directives either override the configuration given in the primary server or supplement it, depending on the directive. For example, the Docu mentRoot directive in a `<VirtualHost>` container overrides the primary server's DocumentRoot, whereas the AddType directive supplements the main server's MIME types.

Now, when a request arrives, Apache uses the IP address and port on which it arrived to find a matching virtual host configuration. If no virtual host matches the address and port, it is handled by the primary server configuration. If it does match a virtual host address, Apache uses the config uration of that virtual server to handle the request.

In the previous example, the virtual host configuration used is the same as the primary server, except that the DocumentRoot is set to `/www/apachehandbook/public/htdocs`, and the ServerName is set to `www.apachehandbook.com`. Directives commonly set in `<VirtualHost>` containers are DocumentRoot, ServerName, ErrorLog, and TransferLog.

You can put almost any configuration directive in the `<VirtualHost>` container, with the exception of ServerType, StartServers, MaxSpareServers, MinSpareServers, MaxRequestPerChild, BindAddress, Listen, PidFile, TypeConfig, ServerRoot, and NameVirtualHost. User and Group may be used inside `<VirtualHost>` containers if the suEXEC wrapper is used.

You can have as many `<VirtualHost>` containers as you want. You can have one or more of your virtual hosts handled by the primary server, or have a `<VirtualHost>` for every available address and port and leave the primary server with no requests to handle.

# Apache configuration for IP-based virtual hosts

Setting up IP-based virtual hosts in a single primary Apache server configuration is very simple. Simply create a `<VirtualHost>` container per virtual IP-address. For example, to create a virtual host called `vhost1.domain.com` (192.168.0.50) with `/www/vhost1/` as the DocumentRoot directory, add the following lines to the httpd. conf file:

```
<VirtualHost 192.168.0.50>
DocumentRoot "/www/vhost1/"
ServerName vhost1.domain.com
</VirtualHost>
```