```
MinSpareServers 5
MaxSpareServers 10
```

This defines how many connections you may need hanging around. Unless you're running a high-traffic site, you can leave these values alone.

```
# Number of servers to start -- should be a reasonable ballpark figure.
StartServers 5
```

```
# Limit on total number of servers running, i.e., limit on the number
# of clients who can simultaneously connect -- if this limit is ever
# reached, clients will be LOCKED OUT, so it should NOT BE SET TOO LOW.
# It is intended mainly as a brake to keep a runaway server from taking
# Unix with it as it spirals down...

MaxClients 150

# MaxRequestsPerChild: the number of requests each child process is
# allowed to process before the child dies.
# The child will exit so as to avoid problems after prolonged use when
# Apache (and maybe the libraries it uses) leak. On most systems, this
# isn't really needed, but a few (such as Solaris) do have notable leaks
# in the libraries.

MaxRequestsPerChild 30
```

This defines how many servers should initially be available, and then how many connections it enables at maximum. Any more connections will be denied by the server. It also defines the amount of child process requests enabled by the server.

```
# Proxy Server directives. Uncomment the following line to
# enable the proxy server:

#ProxyRequests On
# To enable the cache as well, edit and uncomment the following lines:

#CacheRoot /usr/local/etc/httpd/proxy
#CacheSize 5
#CacheGcInterval 4
#CacheMaxExpire 24
#CacheLastModifiedFactor 0.1
#CacheDefaultExpire 1
#NoCache a_domain.com another_domain.edu joes.garage_sale.com
```