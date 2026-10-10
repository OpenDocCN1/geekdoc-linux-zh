You must then have a section for each name on that address, setting the configuration for that name. As with IP-based virtual hosts, you need to set only those configurations that must be different for the host. You must set the ServerName directive because it's the only thing that distinguishes one host from another:

```
<VirtualHost 212.85.67.67>
ServerName bugserver.gnuix.org
ServerAlias bugserver
DocumentRoot /home/bugserver/htdocs
ScriptAlias /home/bugserver/cgi-bin
TransferLog /home/bugserver/logs/access_log
</VirtualHost>

<VirtualHost 212.85.67.67>
ServerName pts.gnuix.org
ServerAlias pts
DocumentRoot /home/pts/htdocs
ScriptAlias /home/pts/cgi-bin
TransferLog /home/pts/logs/access_log
ErrorLog /home/pts/logs/error_log
</VirtualHost>
```

# TIP

If you're hosting websites on an intranet or internal network, users are likely to use the shortened name of the machine rather than the FQDN. For example, users might type `http://bugserver/index.html` in their browser location fields rather than `http://bugserver.gnuix.org/index.html`. In that case, Apache would not recognize that those two addresses should go to the same virtual host. You could get around this by setting up VirtualHost directives for both bugserver and bugserver.gnuix.org, but the easy way around it is to use the `ServerAlias` directive, which lists all valid aliases for the machine:

```
ServerAlias bugserver
```

For more information about `VirtualHost`, refer to the help system on http://localhost/_manual.

# Logging

Apache provides for logging just about any web access information in which you might be interested. Logging can help with the following:

+   - System resource management, by tracking usage
+   - Intrusion detection, by documenting bad HTTP requests
+   - Diagnostics, by recording errors in processing requests