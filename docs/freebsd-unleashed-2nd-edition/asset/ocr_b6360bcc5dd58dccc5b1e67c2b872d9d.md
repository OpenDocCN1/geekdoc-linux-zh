# ### Access Control by Address and Password

It's possible to require that a user satisfy both address restrictions *and* password authentication before access control allows access to a restricted area. This is done with the *Satisfy* directive:

```
```
Allow from 64.41.131.102
Require valid-user
Satisfy all
```
```

*Satisfy all* is the default setting if both *Allow* and *Require* directives are present; this behavior means that the incoming user must meet the *Allow* requirements *and* supply a valid username and password before access will be granted. You can also use *Satisfy* *any* to tell the server that the user must supply a valid password *or* be coming from an allowed address; this is useful if you want users at certain locations to have unconditional access to an area, but require authentication from all other users (for instance, if you're providing a service that you must administer as a regular user, but you don't want to be forever entering passwords for access).

# ## Virtual Hosting

*Virtual hosting* is the practice of keeping the Web site contents for multiple different domains or hostnames on the same server; a single installation of Apache serves requests for all of them. For instance, *www.mystore.com* and *www.frankspage.com* might both be configured in DNS to point to the same IP address on your FreeBSD machine, and Apache is responsible for serving both of them, as well as its own hostname (as specified in the *ServerName* directive).

As you've seen, HTTP/1.0 provided no indication of what hostname the HTTP client was trying to reach (as specified by the user), so in earlier days, virtual hosting had to be done by pointing each hostname to a separate IP address and then binding each IP address as an IP alias to the same Ethernet card. Each virtual host was then specified by IP address, so a request coming from a Web browser would always be sure to get the correct Web site in response. The downside was that binding these large blocks of IP addresses to the same card became unwieldy, and it caused unnecessary consumption of IP address space (which, as you saw in Chapter 21, is not infinite).

The need for this cumbersome process has been much alleviated, however, by HTTP/1.1. The mandatory *Host*: header specifies what hostname the client is trying to reach. Therefore, “name-based” virtual hosts are the norm on the modern Web. Clients that don't support the *Host*: header are almost unheard of these days, so we will be discussing only name-based virtual hosts; if you're interested in address-based virtual hosts, you can find information on them at the Apache Web site.

The bulk of the *httpd.conf* file specifies the “default” server—a global set of definitions that apply to all requests that Apache receives. In the default server, the *ServerName*