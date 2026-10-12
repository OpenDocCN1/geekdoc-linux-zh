
# mod_imap

This module provides for server-side handling of image map files. Clickable regions are defined in a .map file. There are six directives available for use in the .map file. These are used to describe the layout of the clickable regions as well as which URLs they lead to.

# mod_include

This enables the use of Server-Side Includes on your server. See the section “Dynamic Content” later in the chapter for more information about how to use SSI.

# mod_info

The **mod_info** module provides comprehensive information about your server’s configuration. For example, it will display all the modules that are installed, as well as all the directives that are used in its configuration files.

# mod_log_agent

This enables you to log the content of the **UserAgent** header from HTTP requests. Using this information allows you to see which Web browsers visitors to your site are using.

# mod_log_config

This module allows you to define how your log files should look. See the section “Logging” for further information about this subject.

# mod_log_referer

This enables you to log the referer part of an HTTP request.

> **Note**
> As of Apache 1.3.5, this module is deprecated. Use the CustomLog directives instead. See the section on logging for more information on CustomLog.

# mod_mime

This module tries to determine the MIME type of files from their extensions.

# mod_mime_magic

This module tries to determine the MIME type of files by examining portions of their content.

# mod_mmap_static

This module uses the mmap() function to map static pages into system memory. This is used to reduce the server latency introduced by disk access. Because these pages are cached within system memory, the server will need to be restarted if the pages are updated on disk.

> **Caution**
> This module is still considered experimental!

# mod_negotiation

Using this module it is possible to select one of several document versions that best suits the client's capabilities. There are several options to select which criteria to use in the negotiation process. You can, for example, choose among different languages, graphics file formats, and compression methods.

# mod_proxy

This module implements proxy and caching capabilities for an Apache server. It can proxy and cache FTP, CONNECT, HTTP/0.9, and HTTP/1.0 requests. This is not an ideal solution for sites that have a large number of users and therefore have very high proxy and cache requirements. However, it is more than adequate for a small number of users.

# mod_put

This module implements the PUT and DELETE methods from the HTTP/1.1 protocol.

> **Caution**
> Because this module grants people write access, you will have to ensure that write access is limited only to trusted users!

This is one of the third-party modules that Red Hat has added. These are generally not part of the Apache distribution.

# mod_rewrite

This is the Swiss army knife of URL manipulation. It allows you to perform any imaginable manipulation of URLs using powerful regular expressions. It provides rewrites, redirection, proxying, and so on. There is very little that you cannot accomplish using this module.

See http://localhost/manual/misc/rewriteguide.html for a cookbook, which will give you a very good overview of what this module is capable of.

# mod_setenvif

This module allows you to manipulate environment variables. Using regular expressions it is possible to conditionally change the content of environment variables. The order in which SetEnvIf directives appear in the configuration files is important. It is possible that each SetEnvIf directive may reset an earlier SetEnvIf directive when used on the same environment variable. Be sure to keep that in mind when using the directives from this module.

# mod_spelling

This module automatically corrects minor typos in URLs. If no file matches the requested URL, this module will build a list of the files in the requested directory and will extract those files that are the closest matches. It will try to correct only one spelling mistake.

# mod_status

This module creates a Web page containing a plethora of information about a running Apache server. The page will contain information about the internal status as well as statistics about the running Apache processes. This can be a great aid when you are trying to configure your server for maximum performance. It is also a good indicator when something is amiss with your Apache server.

# mod_throttle

This module provides you with the possibility to throttle incoming requests so that the server will not become overloaded when there are too many requests. You may throttle requests directed either to a certain user's material or to a specific virtual host.

You can access the documentation for this module at `http://www.snert.com/Software/Throttle/`.
This is one of the third-party modules that Red Hat has added. These are generally not part of the Apache distribution.

# mod_unique_id

This module generates a unique request identifier for every incoming request. This ID will be put into the `UNIQUE_ID` environment variable.

# mod_userdir

This module enables you to map a subdirectory in each user’s home directory into your Web tree. The module provides several different ways to accomplish this.

# mod_usertrack

This module generates a cookie for each user session. This can be used to track the user’s click stream within your Web tree. You will need to enable a custom log that logs this cookie into a log file.

# mod_vhost_alias

This module provides excellent support for dynamically configured mass virtual hosting. It is especially useful for ISPs with very many virtual hosts. However, for the average user Apache’s ordinary virtual hosting support should prove to be more than sufficient.
There are two ways to host virtual hosts on an Apache server. You can either have one IP address with multiple CNAMES, or you can have multiple IP addresses with one name per address. Apache has different sets of directives to handle each of these options.

# Virtual Hosting

One of the more popular services to provide with a Web server is to host a virtual domain, also known as a virtual host. This is a complete Web site with its own domain name, as if it were a standalone machine, but it’s hosted on the same machine as other Web sites. Apache implements this capability in a simple way with directives in the `httpd.conf` configuration file.

A new way to dynamically host virtual servers was recently added. This is enabled using the `mod_vhost_alias` module. The module is primarily intended for ISPs and similar large sites that host a large number of virtual sites. This is a module for more advanced use, and as such it goes outside the scope of this introductory chapter. Instead, this section concentrates on the traditional ways of hosting virtual servers.

# Note

> For information on setting up your Linux machine with multiple IP addresses or giving your Linux machine multiple CNAMES, see Chapter 14, “Domain Name Service and Dynamic Host Configuration Protocol.”

# Address-Based Virtual Hosts

Once you have configured your Linux machine with multiple IP addresses, setting up Apache to serve them as different Web sites is quite simple. You need only put a VirtualHost directive in your httpd.conf file for each of the addresses that you want to make an independent Web site:

```
<VirtualHost gnulix.org>
ServerName gnulix.org
DocumentRoot /home/virtual/gnulix/public.html
TransferLog /home/virtual/gnulix/logs/access_log
ErrorLog /home/virtual/gnulix/logs/error_log
</VirtualHost>
```

It is recommended that you use the IP address, rather than the hostname, in the VirtualHost tag.

You may specify any configuration directives within the <VirtualHost> tags. For example, you may want to set AllowOverides directives differently for virtual hosts than you do for your main server. Any directives that are not specified default to the settings for the main server.

The directives that cannot be set in VirtualHost sections are ServerType, StartServers, MaxSpareServers, MinSpareServers, MaxRequestsPerChild, BindAddress, Listen, PidFile, TypesConfig, ServerRoot, and NameVirtualHost.

# Name-Based Virtual Hosts

Name-based virtual hosts allow you to run more than one host on the same IP address. You need to add the additional names to your DNS as CNAMES of the machine in question. When an HTTP client (Web browser) requests a document from your server, it sends with the request a variable indicating the server name from which it is requesting the document. Based on this variable, the server determines from which of the virtual hosts it should serve content.
