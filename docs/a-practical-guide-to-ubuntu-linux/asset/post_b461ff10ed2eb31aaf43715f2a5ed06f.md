
# CONFIGURATION DIRECTIVES

being loaded. If this module is loaded, Apache runs the MIMEMagic directive, which tells the mod_mime_magic.c module where its hints file is located.

```
<IfModule mod_mime_magic.c>
MIMEMagicFile /usr/share/file/magic.mime
</IfModule>
```

See page 933 for another example of an <IfModule> container.
Contexts: server config, virtual host, directory, .htaccess

<Limit> access-control directives to specified HTTP methods.

```
<Limit [method] > ... </Limit>
```

where method is an HTTP method. An HTTP method specifies which action is to be performed on a URL. The most frequently used methods are GET, PUT, POST, and OPTIONS; methods are case sensitive. GET (the default method) sends any data indicated by the URL. POST stores data from the body section of the communication at the specified URL. POST creates a new document containing the body of the request at the specified URL. OPTIONS requests information about the capabilities of the server.

The <Limit> container binds a group of access-control directives to specified HTTP methods: Only methods named by this container are affected by this group of directives.
The following example disables HTTP uploads (PUTs) from systems that are not a subdomain of example.com:

```
<Limit PUT>
order deny,allow
deny from all
allow from .example.com
</Limit>
```

Contexts: server config, virtual host, directory, .htaccess

# Use <LimitExcept> instead of <Limit>

It is safer to use the <LimitExcept> container than to use the <Limit> container, as the former protects against arbitrary methods. When you use <Limit>, you must be careful to name explicitly all possible methods that the group of directives could affect.
It is safer not to put access-control directives in any container.

<LimitExcept> access-control directives to all except specified HTTP methods.

```
<LimitExcept [method] > ... </LimitExcept>
```

where method is an HTTP method. See <Limit> for a discussion of methods.
This container causes a group of access-control directives not to be bound to specified HTTP methods. Thus methods not named in <LimitExcept> are affected by this group of directives.

The access-control directives inside the following <LimitExcept> container affect HTTP methods other than GET, POST, and OPTIONS. You could put this container in a <Directory> container to limit its scope:

```
<LimitExcept GET POST OPTIONS>
Order deny,allow
Deny from all
</LimitExcept>
```

Contexts: server config, virtual host, directory, .htaccess

<Location> Applies directives to specified URIs.

```
<Location URI> ... </Location>
```

where URI points to content; it specifies a file or the root of the directory hierarchy in the directory container apply. While the <Directory> container points within the local filesystem

The following <Location> container limits access to http://server/pop to clients from the example.net domain, where server is the FDN of the server:

```
<Location /pop>
Order deny,allow
Deny from all
Allow from .example.net
</Location>
```

Contexts: server config, virtual host

# Use <Location> with care

Use this powerful container with care. Do not use it to replace the <Directory> container: When several URIs point to the same location in a filesystem, a client may be able to circumvent the desired access control by using a URI not specified by this container.

<LocationMatch> Applies directives to URIs specified by a regular expression.

```
<LocationMatch regexp> ... </LocationMatch>
```

where regexp is a regular expression that matches one or more URIs. This container works the same as <Location>, except that it applies to any URIs that *regexp* matches.

Contexts: server config, virtual host

<VirtualHost> Applies directives to a specified virtual host.

```
<VirtualHost addr[:port] [addr[:port]] ... </VirtualHost>
```

where addr is the IP address (or FDN, although it is not recommended) of the virtual host (or * to represent all addresses) and port is the port that Apache listens on for the virtual host. This directive does not control which addresses and ports Apache listens on; use a Listen directive (page 910) for that purpose. This container holds commands that Apache applies to a virtual host. For more information see "NameVirtualHost" on page 920 and "Virtual Hosts" on page 937.

Context: server config

# DIRECTIVES II: ADVANCED DIRECTIVES

This discussion covers configuration directives that you may want to use after you have gained some experience with Apache.

# DIRECTIVES THAT CONTROL PROCESSES

MaxClients Specifies the maximum number of child processes.

```
# MaxClients num
```

where num is the maximum number of child processes (servers) Apache runs at one time, including idle processes and processes that are serving requests. When Apache is running num and there are no idle processes, Apache issues Server too errors to new connections; it does not start new processes. A value of 150 is usually sufficient, even for moderately busy sites.

Context: server config
Change in httpd.conf
Default: 256
Ubuntu: 150

MaxRequestsPerChild Specifies the maximum number of requests a child process can serve.

```
# MaxRequestsPerChild num
```

where num is the maximum number of requests a child process (server) can serve during its lifetime. After a child process serves num requests, it does not process any more requests but dies after it finishes processing its current requests. Apache can start another child process to replace the one that dies. Additional requests are processed by other processes from the server pool.

Set num to 0 to not set a limit on the number of requests a child can process, for the effects of MinSpareServers. By limiting the life of processes, this directive can prevent memory leaks from consuming too much memory. However, setting MaxRequestsPerChild to a too-small value can hurt performance by causing Apache to create new child servers constantly.

Context: server config
Specify in httpd.conf
Default: 10000
Ubuntu: 0

MaxSpareServers Specifies the maximum number of idle processes.

```
# MaxSpareServers num
```

where num is the maximum number of idle processes (servers) Apache keeps running to serve requests as they come in. Do not set this number too high, as each process consumes system resources.

Context: server config
Specify in httpd.conf
Default: 10
Ubuntu: 10

MinSpareServers Specifies the minimum number of idle processes.

```
# MinSpareServers num
```

where num is the minimum number of idle processes (servers) Apache keeps running to serve requests as they come in. More idle processes occupy more computer resources; increase this value for busy sites only.

Context: server config
Specify in httpd.conf
Default: 5
Ubuntu: 5

VirtualHost Specifies the address and port for a name-based (host-by-name) virtual host.

```
# VirtualHost addr[::port]
```

where addr is the IP address (or FQDN, although it is not recommended) that Apache will use for serving a name-based virtual host and port is the port that Apache listens on that virtual host. Specify addr as * to allow the server to process requests on all interfaces as name-based virtual hosts.

This directive does not control which addresses and ports Apache uses; use a Listen directive (page 910) for that purpose. For more information see “<VirtualHost>” on page 918 and “Virtual Hosts” on page 937.

Context: server config
Specify in sites-available/*
Default: none
Ubuntu: *

StartServers Specifies the number of child processes that Apache starts with.

```
# StartServers num
```

where num is the number of child processes (servers) that Apache starts when it is brought up. This value is significant only when Apache starts; MinSpareServers and MaxSpareServers control the number of idle processes once Apache is running. Starting Apache with multiple servers ensures that a pool of servers is waiting to serve requests immediately.

Context: server config
Specify in httpd.conf
Default: 5
Ubuntu: 5 (prefork MPM) or 2 (worker MPM)

# NETWORK DIRECTIVES

HostnameLookups Specifies whether Apache puts a client's hostname or its IP address in the logs.

HostnameLookups On | Off | Double

**On:** Performs DNS name resolution (page 831) to determine the hostname of each client for logging purposes.

**Off:** Logs client's IP address.

**Double:** To provide greater security, DNS name resolution (page 831) to determine the hostname of each client, performs a forward DNS lookup to verify the original IP address, and logs the hostname. Denies access if it cannot verify the original IP address.

Contexts: server config, virtual host, directory
Specify in httpd.conf
Default: Off
Ubuntu: Off

# Lookups can consume a lot of system resources

Use the **On** and **Double** options with caution: They can consume a lot of resources on a busy system. You can use a program as logresolve to perform reverse name resolution offline for logistical purposes.

If you perform hostname resolution offline, you run the risk that the name may have changed; You usually want the name that was current at the time of the request. To minimize this problem, perform the hostname resolution as soon as possible after writing the log.

Timeout Specifies the amount of time Apache waits for network operations to complete.

Timeout *num*

where *num* is the number of seconds that Apache waits for network operations to finish. You can usually set this directive to a lower value; five minutes is a long to wait on a busy server. The Apache documentation says that the default is not lower “because there may still be odd places in the code where the timer is not reset when a packet is sent.

Context: server config
Specify in httpd.conf
Default: 300
Ubuntu: 300
