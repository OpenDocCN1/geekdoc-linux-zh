To make sure that this simple Squid configuration is working, follow this procedure:

+   1. On the Squid server, restart the squid daemon. To do this, type /etc/init.d/squid restart.
+       (If Squid isn't running, use start instead of restart.)
+   2. On the Squid server, start your connection to the Internet (if it is not already up).
+   3. On a client computer on your network, set up (with Mozilla or another Web browser) to use the Squid server as a proxy server (described later in this chapter). (In Mozilla, select Edit \u2192 Preferences \u2192 Advanced \u2192 Proxies, then choose Manual proxy configuration and add the Squid server's computer name and, by default, port 3128 to each protocol.)
+   4. On the client computer, try to open any Web page on the Internet with the browser you just configured.

If the Web page doesn't appear, see the “Debugging Squid” section for how to fix the problem.

# Modifying the Squid configuration file

If you want to set up a more complex set of access permissions for Squid, you should start with the default squid.conf configuration file (described earlier).

To begin, open the /etc/squid/squid.conf file (as the root user). You will see a lot of information describing the values that you can set in this file. Most of the tags that you need to configure Squid are used to set up caching and provide host access to your proxy server.

> **TIP:** Don't change the squid.conf.default file! If you really mess up your squid.conf file, you can start again by making another copy of this file to squid.conf. If you want to recall exactly what change you have made so far, type the following from the /etc/squid directory:
> 
> ```
> # diff squid.conf squid.conf.default | less
> ```
> 
> This will show you the differences between your actual squid.conf and the version you started with.

# Configuring access control in squid.conf

To protect your computing resources from being used by anyone, Squid requires that you define which host computers have access to your HTTP (Web) services. By default, all hosts are denied access to Squid HTTP services except for the local host. With the acl tag, you can create access lists. Then, with the http_access tag, you can authorize access to HTTP (Web) services for the access lists you create.

The form of the access control list tag (acl) is:

```
```
acl name type string
acl name type file
```
```

The name is any name you want to assign to the list. A string is a string of text, and file is a file of information that applies to the particular type of acl. Valid acl types include dst,