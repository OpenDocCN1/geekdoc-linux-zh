
Squid also supports ident and proxy authentication methods to control user access. The following example allows only the users dylan and chris to use the Squid cache:

```
ident_lookup on
acl goodusers user chris dylan
http_access allow goodusers
http_access deny all
```

| Options | Description |
|---|---|
| src ip-address/netmask | Client's IP address |
| src addr1-addr2/netmask | Range of addresses |
| dst ip-address/netmask | Destination IP address |
| myip ip-address/netmask | Local socket IP address |
| srcdomain domain | Reverse lookup, client IP |
| dstdomain domain | Destination server from URL; for dstdomain and dstdom_regex, a reverse lookup is tried if an IP-based URL is used |
| srcdom_regex [-i] expression | Regular expression matching client name |
| dstdom_regex [-i] expression | Regular expression matching destination |
| time [day-abbrevs] [h1:m1-h2:m2] | Time as specified by day, hour, and minutes. Day abbreviations: S = Sunday, M = Monday, T = Tuesday, W = Wednesday, H = Thursday, F = Friday, A = Saturday |
| url_regex [-i] expression | Regular expression matching on whole URL |
| urlpath_regex [-i] expression | Regular expression matching on URL path |
| port ports | Specify a port or range of ports |
| proto protocol | Specify a protocol, such as HTTP or FTP |
| method method | Specify methods, such as GET and POST |
| browser [-i] regexp | Pattern match on user-agent header |
| ident username | String match on ident output |
| src_as number | Used for routing of requests to specific caches |
| dst_as number | Used for routing of requests to specific caches |
| proxy_auth username | List of valid usernames |
| snmp_community string | A community string to limit access to your SNMP agent |

**TABLE 23-1 Squid ACL Options**

## Caches

Squid uses the Internet Cache Protocol (ICP) to communicate with other Web caches. Using the ICP protocol, your Squid cache can connect to other Squid caches or other cache servers, such as Microsoft proxy server, Netscape proxy server, and Novell BorderManager. This way, if your network’s Squid cache does not have a copy of a requested Web page, it can contact another cache to see if it is there instead of accessing the original site. You can configure Squid to connect to other Squid caches by connecting it to a cache hierarchy. Squid supports a hierarchy of caches denoted by the terms child, sibling, and parent. Sibling and child caches are accessible on the same level and are automatically queried whenever a request cannot be located in your own Squid’s cache. If these queries fail, a parent cache is queried, which then searches its own child and sibling caches—or its own parent cache, if needed—and so on. Use cache_host to set up parent and sibling hierarchical connections.

```
cache_host sd.cache.nlanr.net parent 3128 3130
```

You can set up a cache hierarchy to connect to the main NLANR server by registering your cache using the following entries in your squid.conf file:

```
cache_announce 24
announce_to sd.cache.nlanr.net:3131
```

## Logs

Squid keeps several logs. access.log holds requests sent to your proxy, cache.log holds Squid server messages such as errors and startup messages, and store.log holds information about the Squid cache such as objects added or removed. You can use the cache manager (cachemgr.cgi) to manage the cache and view statistics on the cache manager as it runs. To run the cache manager, use your browser to execute the cachemgr.cgi script (this script should be placed in your Web server’s cgi-bin directory).

## Web Server Acceleration: Reverse Proxy Cache

Though Squid caches can enhance access by clients to a Web server, Squid can also reduce the load on a Web server. Web servers that become overwhelmed by requests can move their cacheable pages to a Squid proxy server that can serve as a kind of alternate site, handling requests for those pages. In effect, the Web server becomes accelerated. Such a cache is known as a reverse proxy cache, focusing on the server instead of the client. A reverse proxy cache will intercept requests to a server, processing any for its cached pages. Only requests for noncached pages are forwarded to the original Web server.

To configure a reverse proxy cache, you use the httpd_accel directives. httpd_accel_host specifies the address of the original Web server, and httpd_accel_port is the port it uses. If the proxy supports only one Web server, you set httpd_accel_single_host to on, whereas if the proxy is supporting several Web servers, set it to off. If you want to use the proxy server both as a proxy for clients and as a reverse proxy for the Web server, you set the httpd_accel_with_proxy option to on. However, clients would then need to configure their browsers to access the Web server, as they would to access any standard proxy.
