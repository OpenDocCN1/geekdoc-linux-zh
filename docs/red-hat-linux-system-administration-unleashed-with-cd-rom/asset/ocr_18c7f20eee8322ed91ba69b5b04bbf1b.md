This checks the syntax without actually doing any routing, and writes tracing information to /tmp/gated.trace. You can then examine the trace for errors before moving the new configuration file onto /etc/gated.conf. I recommend that you always do this when you change the configuration, no matter how small the change. You can then have a running gated process reload its configuration by saying

```
/etc/rc.d/init.d/gated reload
```

# Name Services

From a machine's point of view, routing IP datagrams is central to the operation of the Internet. But humans find it very hard to deal with numeric IP addresses—quite simply, very few people have a good enough memory to be able to remember four three-digit numbers for every host they want to be able to use. The solution to this problem is to provide symbolic names for humans to use, but arrange for these symbolic names to be looked up and translated into numeric addresses whenever a machine must deal with them. So for example, if you want to look at the Web site for Red Hat, it's much easier to remember www.redhat.com as the correct location than 206.132.41.203—especially because this numeric address is liable to change at any time. Systems that provide lookup and translation facilities for symbolic names of this sort are called name servers, and this section describes how to operate and use name servers.

# Historical Background

In the early days of the Internet, all host name registrations were listed in a centralized official Network Information Center (NIC) host table. Each Internet site needed to update their local copy of this host table whenever it changed. As the Internet grew, this rapidly became unfeasible, so automated solutions were sought. This search led to the creation of the Domain Name Service, the Internet's "native" name service.

Most systems still use a static host table to a limited extent. The information in the table is needed when DNS is not running, such as during system startup or if there is a serious network problem. All hosts should have a static host table containing at least an entry for that host and for localhost, and quite possibly for gateways and servers on the network. Very small sites where host information rarely changes might find that a static host table is sufficient, especially if supplemented for Internet host names by an offsite name server made available by the Internet service provider.

The static host table has a very simple format. Comments begin with hash signs (#). Non-comment lines contain fields separated by whitespace. The first field on each line is a numeric IP address, and the second is the usual name of that address. Subsequent fields