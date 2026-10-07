TransferLog /home/virtual/gnulix/logs/access_log
ErrorLog /home/virtual/gnulix/logs/error_log
</VirtualHost>

Use the IP address, rather than the hostname, in the VirtualHost tag.

You can specify any configuration directives within the <VirtualHost> tags. For example, you might set AllowOverride directives differently for virtual hosts than you do for your main server. Any directives that aren't specified default to the settings for the main server.

# Name-Based Virtual Hosts

Name-based virtual hosts enable you to run more than one host on the same IP address. You must add the additional names to your DNS as CNAMEs of the machine in question. When an HTTP client (Web browser) requests a document from your server, it sends with the request a variable indicating the server name from which it's requesting the document. Based on this variable, the server determines which of the virtual hosts it should serve content.

> > NOTE Some older browsers are unable to see name-based virtual hosts because this is a feature of HTTP 1.1, and the older browsers are strictly HTTP 1.0-compliant. However, many other browsers are partially HTTP 1.1-compliant, and this is one of the parts of HTTP 1.1 that most browsers have supported for a while.

Name-based virtual hosts require one more step than IP address-based virtual hosts. You must first indicate which IP address has the multiple DNS names on it. This is done with the NameVirtualHost directive:
NameVirtualHost 212.85.67.67

You must have a section for each name on that address, setting the configuration for that name. As with IP-based virtual hosts, you need to set only those configurations that are different for the host. You must set the ServerName directive because it's the only thing that distinguishes one host from another:

```
<VirtualHost 212.85.67.67>
ServerName bugserver.gnulix
ServerAlias bugserver
ServerRoot /home/bugserver/htdocs
ScriptAlias /home/bugserver/cgi-bin
TransferLog /home/bugserver/logs/access_log
</VirtualHost>
```