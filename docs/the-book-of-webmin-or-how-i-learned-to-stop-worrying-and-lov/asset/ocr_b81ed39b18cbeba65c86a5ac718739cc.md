# HTTP Accel Uses Host Header

Configures Squid to use the host header information as described in the HTTP 1.1 specification. This option must be turned on for transparent operation, in order for virtual servers to be cached properly. This option correlates to the httpd_uses_host_header directive.

# WCCP Router Address, WCCP Incoming Address, WCCP Outgoing Address

The Web Cache Coordination Protocol is a standard method of implementing an interception proxy. Routers that support WCCP can be configured to direct traffic to one or more web caches using an efficient load balancing mechanism. WCCP also provides for automatic bypassing of an unavailable cache in the event of a failure. Usually, configuring Squid to use WCCP is as simple as configuring it for interception proxying, using the steps discussed later in the Interception Caching tutorial and then entering the address of the router in the WCCP Router Address field. The other two options are very rarely needed, but can be used in some complex network environments where incoming and outgoing data must travel via different routes or from different addresses. These options correspond to the wccp_router, wccp_incoming_address, and wccp_outgoing_address directives and are disabled by default.

# Tutorial: A Basic Squid Proxy Configuration

Squid is almost entirely preconfigured for traditional proxying as soon as it is installed from source distribution or from a binary package. It can be up and running in just a few minutes, if your needs are simple. This tutorial covers the first changes you’ll need to make to get your caching proxy up and running quickly.

> NOTE
> This tutorial assumes you have already installed Squid and have configured Webmin to know where to find all of the appropriate Squid files. If you’ve installed from a vendor-supplied package, Webmin will probably already know where to find everything.

# Opening Access to Local Clients

The only change that must be made before using your Squid installation is to open access for your local users. By default Squid denies access to all users from any source. This is to prevent your proxy from being used for illicit purposes by users outside of your local network (and you’d be amazed at how many nasty things someone can do with an open proxy).

Click the Access Control icon to edit the access control lists and access rules for your proxy. First, create a new ACL by selecting Client Address from the dropdown list and then clicking Create new ACL. This will open a new page where you can define your ACL. First, enter a name, like localnet, in the Name field. Next, specify your network either in terms of a network range, or by specifying a network and netmask. If you have only 10 addresses, for example, that you would like to be permitted to use your proxy you could enter, for example, a From IP of