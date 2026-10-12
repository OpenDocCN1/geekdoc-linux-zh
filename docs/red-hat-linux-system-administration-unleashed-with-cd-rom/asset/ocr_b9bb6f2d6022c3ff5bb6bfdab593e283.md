```
ErrorLog /home/test/logs/error_log
CustomLog /home/test/logs/custom_log
</VirtualHost>
```

Here, the ServerAlias directive is used to tell Apache if it receives any requests with the domain example.com, regardless of the attached hostname, it will use the specified VirtualHost to respond to the requests. So, to connect to the site, I can either type in www.example.com, or I can just type in example.com. Both will resolve to the VirtualHost on 192.168.2.50

You can also set up Apache to respond differently to different hosts in the same domain. For example, if you only have a single domain, you can set up various virtual hosts that all have the same domain name, yet different sub-domains. The following is an example:

```
Port 80
ServerName www.server.com
NameVirtualHost 192.168.2.50
```

```
<VirtualHost 192.168.2.50>
    ServerAdmin problems@example.com
    ServerName www.example.com
    DocumentRoot /home/example/html
</VirtualHost>
```

```
<VirtualHost 192.168.2.50>
    ServerAdmin problems@example.com
    ServerName www.dev.example.com
    DocumentRoot /home/example.dev/html
</VirtualHost>
```

```
<VirtualHost 192.168.2.50>
    ServerAdmin problems@example.com
    ServerName www.test.example.com
    DocumentRoot /home/example.test/html
</VirtualHost>
```

In addition to simply configuring Apache to respond differently to different IP addresses, you can also tell Apache to respond differently to different ports on the same IP address. For example, the following setup will send the client to the default area if he connects on the default port 80; however, if the client connects on port 443, he will be sent to the secure server area. Port 443 is the default port for handling secure HTTP connections.

```
Listen 80
Listen 443
```