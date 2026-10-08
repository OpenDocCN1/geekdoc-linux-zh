# Hacking Exposed Web Applications

(we’ll discuss Stealth in the upcoming section “Automated Vulnerability Scanning Software").

These files provide a wealth of information about users, the filesystem, log information, peer information, and other data about the server.

# Servlet Engines

Java and servlet-hacking is a realm in itself. Some engines have particular quirks, some vulnerabilities are shared across engines. Some of the most useful exploits are information disclosure attacks. Older versions of BEA WebLogic and Apache Tomcat suffer from %70 attack. Normally, for a request to a URL such as http://www.victim.com/login.jsp displays the page. However, for a request for http://www.victim.com/login.js70 would result in the source code of login.jsp displayed. This works because the %70 represents the letter p, which creates the js extension, but when the parsing engine interprets .js%70 as jp it believes it is a static, non-executable script.

A similar vulnerability reveals a directory listing. In this case, the submitted URL contains %3f.jsp. For example, http://www.victim.com/private/%3f.jsp returns the directory listing for the /private/ directory. The %3f value corresponds to the forward slash (\).

# Miscellaneous Web Server Hacking Techniques

As noted in Chapter 1, Web applications are often found enschon of peripheral technologies, such as load balancers and proxy servers. This section takes a brief look at how such technologies can be circumvented or subverted to gain direct access to Web servers.

# Using Reverse Proxies to Map to a Network

A normal proxy configuration allows hosts on an internal network to make HTTP requests for Web sites on the Internet. A misconfigured proxy allows hosts on the Internet to make HTTP requests for sites on the proxy's internal network, even for nonroutable IP addresses such as 10.0.3.4.

The first step is to identify the proxy. This attack targets the functionality of a proxy, the vulnerability is based on a misconfiguration opposed to a specific vendor or patch level. The simplest test for this vulnerability is to use lynx. For example, to test a proxy listening on port 8000, first set your proxy to the victim's host proxy, then simply connect directly to any desired port:

```
[rohan]$ export http_proxy=http://proxy.victim.com:8000/
[rohan]$ lynx http://internal:port/
```

The variable internal be the hostname or IP address of a host on the target network. This name or IP address must be accessible to the proxy server, not the host from which the query originates. You can also select an arbitrary port. Some services such as