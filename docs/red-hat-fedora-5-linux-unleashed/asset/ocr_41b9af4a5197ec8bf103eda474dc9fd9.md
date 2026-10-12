There are two ways to host virtual hosts on an Apache server. You can have one IP address with multiple CNAMEs, or you can have multiple IP addresses with one name per address. Apache has different sets of directives to handle each of these options. (You learn more about virtual hosting in Apache in the next section of this chapter.)

Again, the available options and features for Apache modules are too numerous to describe completely in this chapter. You can find complete information about the Apache modules in the online documentation for the server included with Fedora or at the Apache Software Foundation’s website.

# ### Virtual Hosting

One of the more popular services to provide with a web server is to host a virtual domain. Also known as a *virtual host*, a virtual domain is a complete website with its own domain name, as if it were a standalone machine, but it’s hosted on the same machine as other websites. Apache implements this capability in a simple way with directives in the `httpd.conf` configuration file.

Apache now can dynamically host virtual servers by using the `mod_vhost_alias` module you read about in the preceding section of the chapter. The module is primarily intended for ISPs and similar large sites that host a large number of virtual sites. This module is for more advanced users and, as such, it is outside the scope of this introductory chapter. Instead, this section concentrates on the traditional ways of hosting virtual servers.

# #### Address-Based Virtual Hosts

After you’ve configured your Linux machine with multiple IP addresses, setting up Apache to serve them as different websites is simple. You need only put a `VirtualHost` directive in your `httpd.conf` file for each of the addresses you want to make an independent website:

```
<VirtualHost 212.85.67.67>
ServerName gnulix.org
DocumentRoot /home/virtual1/gnulix/public_html
TransferLog /home/virtual1/gnulix/logs/access_log
ErrorLog /home/virtual1/gnulix/logs/error_log
</VirtualHost>
```

Use the IP address, rather than the hostname, in the `VirtualHost` tag.

You can specify any configuration directives within the <VirtualHost> tags. For example, you might want to set `AllowOverrides` directives differently for virtual hosts than you do for your main server. Any directives that aren’t specified default to the settings for the main server.