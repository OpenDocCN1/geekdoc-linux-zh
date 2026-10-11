The following `<Location>` container limits access to `http://server/pop` to clients from the example.net domain, where *server* is the FQDN of the server:

```
<Location /pop>
    Order deny,allow
    Deny from all
    Allow from .example.net
</Location>
```

Contexts: server config, virtual host

# ## Use `<Location>` with care

> **caution** Use this powerful container with care. Do not use it to replace the `<Directory>` container: When several URLs point to the same location in a filesystem, a client may be able to circumvent the desired access control by using a URL not specified by this container.

`<LocationMatch>` *Applies directives to matched URIs.*

```
<LocationMatch regex> ... </LocationMatch>
```

where *regex* is a regular expression that matches one or more URIs. This container works the same way as `<Location>`, except that it applies to any URIs that *regex* matches:

```
# Disable autoindex for the root directory and present a
# default welcome page if no other index page is present.
#
<LocationMatch "*/$">
    Options -Indexes
    ErrorDocument 403 /error/noindex.html
</LocationMatch>
```

Contexts: server config, virtual host

`<VirtualHost>` *Applies directives to a specified virtual host.*

```
<VirtualHost addr[:port] [addr[:port]] ... > ... </VirtualHost>
```

where *addr* is an FQDN or IP address of the virtual host and *port* is the port that Apache listens on for the virtual host. This container holds commands that Apache applies to a virtual host. For an example and more information, refer to “Virtual Hosts” on page 874.

Context: server config

# # Directives II: Advanced Directives

This section discusses configuration directives that you may want to use after you have gained some experience with Apache.

# ## Directives That Control Processes

**MaxClients** *Specifies the maximum number of child processes.*

```
MaxClients num
```