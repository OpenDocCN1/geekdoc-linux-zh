
## Progress Check

- 1. Top-level domains signify organizational boundaries.
- 2. In order, www is the host, worldscollide is the domain name, and org is the top-level domain.
- 3. C. Domain names are hierarchical.

## Installing a DNS Server

Red Hat comes with the option to install a DNS server when the system is installed for the first time, though you can also install the RPMs at a later time. The DNS server of choice for Linux and for almost all UNIX servers is BIND, the Berkeley Internet Name Domain server.

(At one point, a rumor floated around the Internet that Windows NT’s name server bore striking similarity to BIND. This rumor was never confirmed or denied.) As of this writing, the latest BIND version is 9.2, which conveniently is also what Red Hat 8 currently uses.

> Because of the critical nature of the BIND software, it was taken over by the Internet Software Consortium (ISC) to ensure its continued development. You can find out more about the ISC at http://www.isc.org. The ISC is also in charge of development of a DHCP server as well as the INN news server.

BIND 9 was a major rewrite that introduced some significant changes over BIND 8, and some administrators have been slow to make the conversion. If your organization has a reason to remain with an older version of BIND, you will either have to find an RPM of the appropriate version or be willing to compile it yourself. If you're installing BIND for the first time, there is no reason not to start with BIND 9. Regardless of which branch you're tracking, keep an eye out for new releases. New bugs and security issues are discovered from time to time and should be corrected. Of course, new features are released, as well, but unless you have a need for them, those releases are less critical. All new BIND 9 releases are available at http://www.isc.org, or you can get an updated RPM from Red Hat.

![](img/ec2066d370d3af1a767664d36aa7ddfe_327_0.png)

> Although freely available with full source code to anyone who wishes to download it, BIND has the benefit of the ISC's commercial-quality management and support. Of course you'll have to pay for the commercial-level support, but the software supported by their commercial-level contracts is the same software you can download free.

Along with the BIND server itself, you'll find a few tools that you'll use for setting up and testing your name server. These tools are actually part of a separate RPM called bind-utils, in case you want to install them on a machine that doesn't need to run its own DNS server.

## Starting DNS at Boot Time

Since the default installation of BIND on Red Hat is pretty minimal, it's not terribly useful out of the box. As a result, it's not started by default when you boot your machine. We're going to configure it in the next few pages, but before we do so, let's make sure that it starts automatically when the server does. There are two easy ways to do this. The first is through the simple GUI interface for services. Hopefully you'll remember the Service Configuration tool from Module 4. While BIND is a complete package including both the name server, a name resolver, and various tools, the name server is the piece we're looking to start at boot time. This server is called named (pronounced “name-dee”), which is short for "name daemon." When you bring up the Service Configuration tool, if you have BIND properly installed, you can enable named by clicking the appropriate check box for each runlevel you are interested in, as shown in the following illustration. I'd suggest that unless you have other specific requirements, you now enable it for runlevels three through five.

![](img/ec2066d370d3af1a767664d36aa7ddfe_328_0.png)

Now suppose that you have your DNS server locked away in a server room somewhere and you don’t have immediately available all the comforts of a modern GUI desktop. Perhaps you’re even accessing the box through some form of remote console utility. Fortunately, you recall what you learned earlier in this book about init scripts and using symlinks to start and stop services at a particular runlevel. So to enable named in runlevel 5, for example, you simply navigate to `/etc/rc5.d` and replace the K45named symlink with an S55named symlink.

> **NOTE** If you’re wondering where I pulled the symlink numbers from in this example, I did steal them from what Red Hat’s Service Configuration tool would have used, but any valid values would have worked. However, don’t overlook interactions between services if you find the need to choose your own values.

## Hurry Up Already! And What Are We Skipping in the Process?

If all you are looking for is a simple configuration for a simple situation, take a look at the cookbook solutions in “Putting It All Together” at the end of the module. One of them may be exactly what you are looking for. Of course, I still recommend reading through the module to understand how BIND interprets the configuration files so that you can more easily troubleshoot problems in the future.

If you do take the time to read the documentation that comes with BIND, you may wonder why I don’t cover several of the features that are new to BIND, such as Secure DNS (DNSSEC) and IPv6 (Internet Protocol, version 6) support. The reason is simple: those are very heavy topics that require a significant background to understand. Both of their discussions more or less merit a book of their own. It’s unfortunate that DNS has become this complex, but the Internet isn’t the friendly place it used to be, either.

## BIND Documentation

BIND comes with a lot of great documentation, and I highly recommend taking the time to go through it. It’s hardly light reading, but it will make you a better systems administrator and a better DNS administrator. And the world needs as many good sysadmins as it can get!

In addition to what can be found in the man and info pages, there is a wealth of information installed under /usr/share/doc/bind-9.2.1 (adjusting the version number as necessary to match the RPM you’ve installed). The best way to read through the multiple HTML page files is to point your web browser to them, read them and click a link to bring up another, and so on. This is because several of the files are written in HTML (Hypertext Markup Language) and are much easier to read than their text counterparts. (By easier to read, I mean easier on the eye. The content is identical.)

Of the directories in the doc directory, the most important documentation is the arm subdirectory. In there you will find the BIND Administrators Reference Manual. As the title suggests, ARM is a reference manual and not a tutorial, but as you need more complex configurations out of your DNS server, you will find it a very valuable resource.

## 10.4 Configuring Clients

In this section and the next, we’ll delve into the wild and exciting process of configuring DNS clients and servers! Okay, maybe they’re not that exciting but there’s no denying their significance to the infrastructure of any networked site, so it’s best if you can get a few warm and fuzzy feelings about DNS configurations.

### Client-Side DNS (a.k.a. the Resolver)

So far, we’ve been studying servers and the DNS tree as a whole. The other part of this equation is, of course, the client—the host that is contacting the DNS server to resolve a host name into an IP address.

Under Linux, the client side of DNS is handled by the resolver. This is actually part of a library of C programming functions that gets linked to a program when the program is started.

Because all of this happens automatically and transparently, the user doesn’t have to know anything about it. It’s simply a little bit of magic that lets the user start browsing the Internet.

From the system administrator’s perspective, configuring the DNS client isn’t magic, but it’s very straightforward. There are only two files involved: **/etc/resolv.conf** and **/etc/nsswitch.conf**.

## The /etc/resolv.conf File

The **/etc/resolv.conf** file contains the information necessary for the client to know what its local DNS server is. (Every site should have, at the very least, its own caching DNS server.) This file has two lines: The first line indicates the default search domain, and the second indicates the IP address of the host’s name server.

The *default search domain* applies mostly to sites that have their own local servers. When the default search domain is specified, the client side will automatically append this domain name to lookups in case it is a bare host name or a local subdomain. For example, if we specify our default domain to be yahoocom and then try to connect to the host name my, the client software will automatically try contacting my.yahoo.com. Using the same default, if we try to contact the host **www.stat.net**, the software will try **www.stat.net.yahoocom** (a perfectly legal host name), find that it doesn’t exist, and then try **www.stat.net** alone (which does exist).

Of course, you may supply multiple default domains. However, doing so will slow the query process a bit, because each domain will need to be checked. For instance, if both **yahoocom** and **stanford.edu** are specified, and we perform a query on **www.stat.net**, we’ll get three queries: **www.stat.net.yahoocom**, **www.stat.net.stanford.edu**, and **www.stat.net**.

The format of the **/etc/resolv.conf** file is as follows:

```
search domainname
nameserver IP-address
```

where *domainname* is the default domain name to search, and *IP-address* is the IP address of your DNS server. For example, here’s my **/etc/resolv.conf** file:

```
search collab.net
nameserver 127.0.0.1
```

Thus when I contact **zap@hodd.collab.net**, I only need to specify **zap@hodd** as the host name. Since I run a name server on my own machine, I specify the local host address.
