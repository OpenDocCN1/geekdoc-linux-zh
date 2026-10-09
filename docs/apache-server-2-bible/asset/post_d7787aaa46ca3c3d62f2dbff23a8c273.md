
As you can see, the robot's User-Agent header is matched, along with the IP address of the host it uses. The above conditions allow for multiple IP addresses (123.45.67.8 and 123.45.67.9) to be checked.

## Creating an HTTP Referrer-Based URL Deflector

You can program a flexible URL deflector that acts on the Referrer HTTP header and configure it with as many referring pages as you like. Here's how:

```apache
RewriteMap  deflector txt:path/to/deflector.map
RewriteRule  ^/(.*)
  $1deflector:&(HTTP_REFERER)|/$1
RewriteRule .*DEFLECTED  &[HTTP_REFERER] [R,L]
RewriteRule .* - [PT]
```

This is used in conjunction with a corresponding rewrite map such as the following:

| http://www.badguys.com/bad/index.html | DEFLECTED |
|----------------------------------------|-----------|
| http://www.badguys.com/bad/index2.html | DEFLECTED |
| http://www.badguys.com/bad/index3.html | http://somewhere.com/ |

This automatically redirects the request back to the referring page if the URL matches the DEFLECTED value in the map file. In all other cases, the requests are redirected to specified URLs.

## Setting up a Proxy Server

![](img/e11fcbd2818a3495ac70085e5d8d1c26_295_0.png)

A proxy server is a system that sits between the client hosts and the servers that they need access to. When a client host requests a certain remote resource using a URL, the proxy server receives this request and fetches the resource to fulfill the client's request. In a general sense, a proxy server acts like a server to the client hosts and a client to the remote servers.

In typical proxy scenarios, this process enables the proxy server to store the requested content in a cache. Any new request that asks for information already in the cache no longer needs to be serviced by fetching it from the remote server. Instead, the new request is serviced from the cached data. This allows proxy servers to ease network bottlenecks. However, this is not all that a proxy server does.

This chapter teaches you to turn Apache into a proxy server that can perform a multitude of services. You learn how to turn Apache into a caching (forward) proxy server. Deploying such a server at the network bottleneck can reduce delays in response times, conserve bandwidth, and help reduce your overall communications expense. Because proxy is usually used for networks with large user communities, I also cover various aspects of client configuration including automatic proxy configuration.

### Who Should Use a Proxy Server?

The purpose of this proxy server is to fetch the requested resource from the remote server, return it to the requesting user, and cache it in local drives. Proxy service is ideal for scenarios in which more than one user is accessing the network. Many organizations have several host computers that access the Internet via a single Internet connection such as an ISDN router or other dedicated or on-demand connection. A proxy can be very helpful in such a network.

**In This Chapter**

- Understanding types of proxy servers
- Configuring Apache as a proxy server
- Setting up Web browsers for proxy

You can gain the following benefits by using a proxy for both Internet and intranet resources:

- Proxying: If the internal network uses nonroutable IP addresses for either security or cost reasons, you can use a proxy server to provide Internet resources to hosts that normally cannot access the Internet. This chapter teaches you how to do this.
- Caching: Using a caching proxy such as Apache (with mod_perl), you can provide seemingly faster access to Internet resources to the local users. This will not only enhance the user's perception of network performance but also cut down on bandwidth usage costs.
- Logging and Access Control: By using a proxy server, you can monitor Internet (or even intranet) usage by employees or students. You can block access to certain Web sites to protect your company from potential lawsuits, and you can stop abuse of company time. By analyzing your proxy server's access and error logs, you can identify usage patterns and make better network usage policy in the future.

### Understanding Types of Proxy Servers

Before talking about using Apache as a proxy server, let's discuss the types of proxy servers and how they work. There are two types of proxy servers:

- Forward proxy server: When this type of proxy server is used, users pass their requests to the proxy server and the proxy server gets the intended response from the target host of the request. Forward proxies are typically explicitly defined in user's programs (such as the Web browser).
- Reverse proxy server: When this type of proxy server is used, users are usually unaware of them because they think they are accessing the intended resource. All requests made by the users are sent to the reverse proxy, which serves the response from its cache or by requesting information from another host.

#### Forward Proxy

A forward proxy server usually sits between the user hosts and the remote resources that they want to access. A resource can be an Internet resource, as shown in Figure 10-1, or it can be an intranet resource. The next request for the same resource will be serviced from the cached data if the data has not expired.

![](img/e11fcbd2818a3495ac70085e5d8d1c26_297_0.png)

Figure 10-1: A forward proxy server

The user hosts know that they are using a proxy server because each host must be configured to use the proxy server. For example, you must tell a Web browser to use a proxy server before the browser can use it. All remote requests are channeled via the forward proxy server as shown in Figure 10-1, providing a manageable and cost-effective solution for reducing bandwidth usage and implementing user access policy.

This type of proxy server is also referred to as a caching proxy server. The reverse proxy server also caches data but it acts in the reverse of the forward proxy server.

#### Reverse Proxy

A reverse proxy server sits in front of an Internet resource, as shown in Figure 10-2, or in front of an intranet resource. In such a setup the reverse proxy retrieves the requested resource from the original server and returns it to the user host.

The user hosts that connect to the proxy server are unaware that they are connecting to a proxy server instead of directly to the resource’s server, unlike when a forward proxy server is used. As far as the end user is concerned, the requested resource is being accessed directly.

Figure 10-2 shows that users from Internet cannot connect to the Web server without going through the reverse proxy. Because this is a reverse proxy, the users are unaware of it and they think they are connecting to the Web server instead. The LAN users can directly connect to the Web server from the internal network, as shown in the figure.

![](img/e11fcbd2818a3495ac70085e5d8d1c26_298_0.png)

For example, if a reverse proxy server is used for a Web site called `www.csus.edu`, then all a CSUS (California State University, Sacramento) student has to do is point his or her browser to `www.csus.edu` and not tell the browser anything about any proxy configuration. The browser places a request to the server known as `www.csus.edu`. Little does the browser know that the `www.csus.edu` server is really a reverse proxy server that internally translates the request to a Web server called `internal-www.csus.edu` to get the content for the request. What does such a setup gain? Because the data is cached from each request, the proxy server can provide some load-balancing support for the real servers behind the scene.

> Apache currently does not support reverse proxy service; however, this will be implemented in the next version of the `mod_proxy` module.

## mod_proxy Directives

The proxy support in Apache comes from the `mod_proxy` module. This module is not compiled by default. You have to reconfigure Apache using `./config.status --enable-module=proxy` from the Apache source distribution directory and run `make && make install` to recompile and reinstall updated Apache server. Currently, it only implements a caching proxy server in Apache. It is capable of supporting HTTP 1.1, HTTPS (via CONNECT for SSL), and FTP protocols. The module can also be configured to connect to other proxy modules for these and other protocols. It provides the directives discussed in the following sections.
