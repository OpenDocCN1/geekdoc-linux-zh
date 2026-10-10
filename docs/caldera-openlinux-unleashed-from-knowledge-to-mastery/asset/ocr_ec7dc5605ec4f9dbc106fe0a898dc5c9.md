AllowOverrides can be set to be All or any combination of Options, FileInfo, AuthConfig, and Limit. Explanations for these options follow.

+   * Options The .htaccess file can add options not listed in the Options directive for this directory.
+   * FileInfo The .htaccess file can include directives for modifying document type information.
+   * AuthConfig The .htaccess file may contain authorization directives.
+   * Limit The .htaccess file may contain allow, deny, and order directives.

# # Virtual Hosting

One of the more popular services to provide with a Web server is to host a virtual domain, also known as a virtual host. This is a complete Web site with its own domain name, as if it were a standalone machine, but it’s hosted on the same machine as other Web sites. Apache implements this capability in a simple way with directives in the httpd.conf configuration file. There are two ways to host virtual hosts on an Apache server. Either you can have one IP address with multiple CNAMES, or you can have multiple IP addresses with one name per address. Apache has different sets of directives to handle each of these options.

# ## Address-Based Virtual Hosts

After you have configured your Linux machine with multiple IP addresses, setting up Apache to serve them as different Web sites is quite simple. You need only put a VirtualHost directive in your httpd.conf file for each of the addresses that you want to make an independent Web site:

```
```apache
<VirtualHost www.virtual.com>
 ServerName www.virtual.com
 DocumentRoot /home/virtual/public_html
 TransferLog /home/virtual/logs/access_log
 ErrorLog /home/virtual/logs/error_log
</VirtualHost>
```
```

You should use the IP address, rather than the hostname, in the VirtualHost tag.

You may specify any configuration directives within the <VirtualHost> tags. For example, you may want to set AllowOverrides directives differently for virtual hosts than you do for your main server. Any directives that are not specified default to the settings for the main server.

The directives that cannot be set in VirtualHost sections are ServerType, StartServers, MaxSpareServers, MinSpareServers, MaxRequestsPerChild, BindAddress, Listen, PidFile, TypesConfig, ServerRoot, and NameVirtualHost.