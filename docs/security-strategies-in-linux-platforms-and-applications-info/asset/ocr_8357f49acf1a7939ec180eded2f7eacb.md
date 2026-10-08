# PART 2 | Layered Security and Linux

A couple of security-related Apache directives Listen and ServerTokens. The Listen directive can specify an alternative port for Web pages. For example, the following directive can be found in the configuration for an SSL-enabled Web site. Port 443 is the standard for the secure Hypertext Transfer Protocol (HTTPS).

Listen 443

The Listen directive can also specify the IP address of a network card, which is useful if there are multiple network cards on the local system. For example, the following directive would listen for requests through port 443 on the noted IP address:

```
Listen 192.168.100.10:443
```

The ServerTokens directive can be of special interest. It determines what's seen if a user navigates to a nonexistent Web page. While it is normally "error message," that message can provide far too much information to a black-hat hacker. In the default configuration ServerTokens Full is set to, which leads to the following error message sent in a response to a nonexistent Web page:

```
Apache/2.2.3 (Red Hat) DAV/2 PHP/5.1.6 mod_ssl/2.2.3
OpenSSL/0.9.8e-fips-rel5 Server/192.168.100.1 Port 80
```

If a black-hat hacker recognizes a version of one of these applications that happens to be vulnerable, he is in business and your systems will be at risk. Ideally, this information should be kept as minimal as possible. For example, the ServerTokens Prod directive leads to the following error message:

```
Apache Server at 192.168.100.1 Port 80
```

Perhaps an even better way to deny information to a black-hat hacker is a custom error page. Look for the DocumentRoot and ErrorDocument directives in the Apache configuration file. It help you identify an appropriate location for a custom error file. In other words, black-hat hackers don't even have to know that this is an Apache server.

# KeepAlive Directives

The most important security-related directive in the Apache configuration file is KeepAlive, which supports persistent connections from remote systems.

In a more secure system, the values of KeepAlive directives are kept to a minimum. But such a configuration is not consistent with the availability of Web pages served by Apache. Good values for KeepAlive directives improve client performance.

Related directives (MaxKeepAliveRequests, KeepAliveTimeout) are almost self-explanatory and are well explained by the comments in the Red Hat version of the configuration file. In brief, while MaxKeepAliveRequests specifies the maximum number of allowed keep-alive requests on each connection, the KeepAliveTimeout specifies the wait period for the next request, in seconds.