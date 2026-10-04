# Architecting the Human Factor • Chapter 17

the source address of unauthorized Web vulnerability scans, or worse yet, compromises.
Proxies should be firewalled to prevent inbound connections on the service port from noninternal addresses, and should be tested regularly, either manually or with the assistance of a vulnerability assessment service. Some Web servers, too, can be hijacked as proxies, so be sure to include all Web servers in your scans. If you want to do a manual test of a Web server or proxy, the process is very simple. Use your system’s telnet client to connect to the proxy or Web-server’s service port as shown here:

```
C:\telnet www.foo.org 80
Connecting to www.foo.org...
GET http://www.sun.com HTTP/1.0 <CR> <CR>
```

> [HTTP data returned here]
Review the returned data to ascertain if it is coming from www.sun.com or not. Many Web servers and proxies are configured to return a default page when they are unable to access the data you’ve requested, so although you get a whole lot of HTML code back from this test, you need to review the contents of the HTML to decide whether or not it is the page requested. If you're testing your own proxies from outside, you would expect to see a connection failure, as shown here:

```
C:\telnet www.foo.org 80
Connecting to www.foo.org... Could not open a connection to host at port 80 : Connect failed
```

This message indicates that the service is not available from your host, and it is what you’d expect to see if you were trying to use your corporate HTTP proxy from an Internet café or your home connection.

HTTP proxies provide other benefits, such as content caching and filtering. Caching serves two purposes, minimizing bandwidth requirements for commonly accessed resources and providing greater performance to the end user. Another user has already loaded the New York Times home page at http://www.nytimes.com recently, the next user to request that site will be served as fast as the local network can carry it from the proxy to the content as

![](bbox=[0.712, 0.946, 0.929, 0.966])