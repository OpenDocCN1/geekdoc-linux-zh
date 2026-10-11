
The following `<Location>` container limits access to `http://server/pop` to clients from the example.net domain, where *server* is the FQDN of the server:

```
<Location /pop>
    Order deny,allow
    Deny from all
    Allow from .example.net
</Location>
```

Contexts: server config, virtual host

## Use `<Location>` with care

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

# Directives II: Advanced Directives

This section discusses configuration directives that you may want to use after you have gained some experience with Apache.

## Directives That Control Processes

**MaxClients** *Specifies the maximum number of child processes.*

```
MaxClients num
```

where **num** is the maximum number of child processes (servers) Apache runs at one time, including idle processes and those serving requests. When Apache is running **num** processes and there are no idle processes, Apache issues *Server too busy* errors to new connections; it does not start new child processes. A value of 150 is usually sufficient, even for moderately busy sites.

Context: **server config**  
Default: 256  
Fedora/RHEL: 256

**MaxRequestsPerChild**

*Specifies the maximum number of requests a child process can serve.*

**MaxRequestsPerChild num**

where **num** is the maximum number of requests a child process (server) can serve during its lifetime. After a child process serves **num** requests, it does not process any more requests but dies after it finishes processing its current requests. At this point additional requests are processed by other processes from the server pool.

Set **num** to 0 to not set a limit on the number of requests a child can process, except for the effects of MinspareServers. By limiting the life of processes, this directive can prevent memory leaks from consuming too much system memory. However, setting MaxRequestsPerChild to a small value can hurt performance by causing Apache to create new child servers constantly.

Context: **server config**  
Default: 10000  
Fedora/RHEL: 4000

**MaxSpareServers**

*Specifies the maximum number of idle processes.*

**MaxSpareServers num**

where **num** is the maximum number of idle processes (servers) Apache keeps running to serve requests as they come in. Do not set this number too high, as each process consumes system resources.

Context: **server config**  
Default: 10  
Fedora/RHEL: 20

**MinSpareServers**

*Specifies the minimum number of idle processes.*

**MinSpareServers num**

where **num** is the minimum number of idle processes (servers) Apache keeps running to serve requests as they come in. More idle processes occupy more computer resources; increase this value for busy sites only.

Context: **server config**  
Default: 5  
Fedora/RHEL: 5

**StartServers** *Specifies the number of child processes that Apache starts with.*

```
StartServers num
```

where *num* is the number of child processes, or servers, that Apache starts when it is brought up. This value is significant only when Apache starts; MinSpareServers and MaxSpareServers control the number of idle processes once Apache is up and running. Starting Apache with multiple servers ensures that a pool of servers is waiting to serve requests immediately.

Context: *server config*  
Default: 5  
Fedora/RHEL: 8

## Networking Directives

**HostnameLookups** *Specifies whether Apache puts a client’s hostname or its IP address in the logs.*

```
HostnameLookups On | Off | Double
```

*On:* Performs DNS reverse name resolution (page 783) to determine the hostname of each client for logging purposes.

*Off:* Logs each client’s IP address.

*Double:* To provide greater security, performs DNS reverse name resolution (page 783) to determine the hostname of each client, performs a forward DNS lookup to verify the original IP address, and logs the hostname.

Contexts: *server config*, *virtual host*, *directory*  
Default: Off  
Fedora/RHEL: Off

> ### tip Lookups can consume a lot of system resources
>
> Use the *On* and *Double* options with caution: They can consume a lot of resources on a busy system. You can use a program such as *logresolve* to perform reverse name resolution offline for statistical purposes.
>
> If you perform hostname resolution offline, you run the risk that the name may have changed; you usually want the name that was current at the time of the request. To minimize this problem, perform the hostname resolution as soon as possible after writing the log.

**Timeout** *Specifies the time Apache waits for network operations to complete.*

```
Timeout num
```

where *num* is the number of seconds that Apache waits for network operations to finish. You can usually set this directive to a lower value; five minutes is a long time to wait on a busy server. The Apache documentation says that the default is not lower “because there may still be odd places in the code where the timer is not reset when a packet is sent.”

- Context: **server config**
- Default: 300
- Fedora/RHEL: 120

**UseCanonicalName**

*Specifies the method the server uses to identify itself.*

```
UseCanonicalName On | Off | DNS
```

**On**: Apache uses the value of the ServerName directive (page 852) as its identity.

**Off**: Apache uses the name and port from the incoming request as its identity.

**DNS**: Apache performs a DNS reverse name resolution (page 783) on the IP address from the incoming request and uses the result as its identity. Rarely used.

This directive is important when a server has more than one name and needs to perform a redirect. Fedora/RHEL sets this directive to Off because the ServerName directive (page 852) is commented out. Once you set ServerName, change UseCanonicalName to On. See page 873 for a discussion of redirects and this directive.

- Contexts: **server config**, **virtual host**, **directory**
- Default: Off
- Fedora/RHEL: Off

# LOGGING DIRECTIVES

**ErrorLog**

*Specifies where Apache sends error messages.*

```
ErrorLog filename | syslog[:facility]
```

where *filename* specifies the name of the file, relative to ServerRoot (page 865), that Apache sends error messages to; *syslog* specifies that Apache send errors to **syslogd** (page 582); and *facility* specifies which **syslogd** facility to use. The default facility is **local7**.

- Contexts: **server config**, **virtual host**
- Default: logs/error_log
- Fedora/RHEL: logs/error_log

**LogLevel**

*Specifies the level of error messages that Apache logs.*

```
LogLevel level
```

where *level* specifies that Apache log errors of that level and higher (more urgent). Choose *level* from the following list, which is presented here in order of decreasing urgency and increasing verbosity:

| Level   | Description                     |
|---------|---------------------------------|
| `emerg` | System unusable messages        |
| `alert` | Need for immediate action messages|
