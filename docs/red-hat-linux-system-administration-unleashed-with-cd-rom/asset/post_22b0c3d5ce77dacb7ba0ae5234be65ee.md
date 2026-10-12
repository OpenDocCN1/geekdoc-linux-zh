
## Configuring /etc/gated.conf

The /etc/gated.conf file has a number of configuration statements that are divided into several categories. Statements of each type must be grouped together, and the types must be presented in a specific order. Using a statement out of order will cause an error when gated parses the file.

The gated daemon has many configuration options—far more than this book can accommodate. If you need to understand all the possibilities provided by gated, you will need to read its reference manual. However, showing some sample configurations will give you an introduction to what it can do.

### Host Routing Configuration

A host routing configuration for gated is actually quite straightforward. This is fitting, given that the work to be done is also fairly simple. Listing 14.4 gives an example.

### LISTING 14.4 A Host Routing Configuration for gated

```
# Enable RIP
rip yes {
  # Don't broadcast your own RIP updates
  nobroadcast ;
  interface 192.168.1.17
  # Use RIP-2
  version 2
  # Transmit updates via multicast to reduce load
  # on RIP-1 systems
  multicast ;
};
```

This example shows the basic structure of the configuration file, including comments introduced with a # sign, statements terminated by a semicolon, and statement grouping with braces.

### Interior Gateway Configuration

An interior gateway configuration is only a little more complex. Suppose that a gateway named igw interconnects subnets 192.168.5.0 and 192.168.17.0, and that subnet 192.168.17.0 has a gateway to the Internet. The igw gateway has interfaces 192.168.5.1 and 192.168.17.3. It advertises itself to hosts on subnet 5 as the default gateway because it is the gateway to the outside world. It uses RIP-2 to advertise routes on subnet 5. On subnet 17, igw advertises itself as the gateway to subnet 5, using OSPF. Listing 14.5 shows the configuration.

### LISTING 14.5 An Interior Routing Configuration for gated

```
# Don't let subnet 5 time out, because this is the only path to
# that subnet.
interfaces {
    interface 192.168.5.1 passive ;
};

# Define an OSPF router id; we use the address of the interface
# that speaks OSPF. The default is the address of the first
# interface encountered by gated
routerid 192.168.5.1 ;

# Enable RIP-2 and announce OSPF routes to subnet 5 with a cost
# of 5. The cost is low because this is an internal route.
rip yes {
    # Broadcast RIP-2 updates
    broadcast ;
    # The cost
    defaultmetric 5 ;
    interface 192.168.5.1
        version 2
        multicast ;
};

# Enable OSPF on the backbone area, subnet 17
ospf yes {
    backbone {
        interface 192.168.17.3 {
            # Use a fairly low priority to increase the
            # probability this will be elected as the
            # designated router.
            priority 5 ;
        } ;
    } ;
};
```

One thing to remember when configuring gated is that a syntax error in your /etc/gated.conf will prevent it from starting properly. However, you can use the program itself to check the syntax automatically. Suppose you are editing a copy of gated.conf in /tmp/gated.conf.new. You can test it with the command

gated -c -f /tmp/gated.conf.new /tmp/gated.trace

This checks the syntax without actually doing any routing, and writes tracing information to /tmp/gated.trace. You can then examine the trace for errors before moving the new configuration file onto /etc/gated.conf. I recommend that you always do this when you change the configuration, no matter how small the change. You can then have a running gated process reload its configuration by saying

```
/etc/rc.d/init.d/gated reload
```

## Name Services

From a machine's point of view, routing IP datagrams is central to the operation of the Internet. But humans find it very hard to deal with numeric IP addresses—quite simply, very few people have a good enough memory to be able to remember four three-digit numbers for every host they want to be able to use. The solution to this problem is to provide symbolic names for humans to use, but arrange for these symbolic names to be looked up and translated into numeric addresses whenever a machine must deal with them. So for example, if you want to look at the Web site for Red Hat, it's much easier to remember www.redhat.com as the correct location than 206.132.41.203—especially because this numeric address is liable to change at any time. Systems that provide lookup and translation facilities for symbolic names of this sort are called name servers, and this section describes how to operate and use name servers.

### Historical Background

In the early days of the Internet, all host name registrations were listed in a centralized official Network Information Center (NIC) host table. Each Internet site needed to update their local copy of this host table whenever it changed. As the Internet grew, this rapidly became unfeasible, so automated solutions were sought. This search led to the creation of the Domain Name Service, the Internet's "native" name service.

Most systems still use a static host table to a limited extent. The information in the table is needed when DNS is not running, such as during system startup or if there is a serious network problem. All hosts should have a static host table containing at least an entry for that host and for localhost, and quite possibly for gateways and servers on the network. Very small sites where host information rarely changes might find that a static host table is sufficient, especially if supplemented for Internet host names by an offsite name server made available by the Internet service provider.

The static host table has a very simple format. Comments begin with hash signs (#). Non-comment lines contain fields separated by whitespace. The first field on each line is a numeric IP address, and the second is the usual name of that address. Subsequent fields (if any) specify aliases. Listing 14.6 shows a sample minimal /etc/hosts file, containing entries only for localhost and for the system itself.

### LISTING 14.6 A Sample minimal /etc/hosts File

```
# Table of IP addresses and host names

127.0.0.1    localhost
192.168.1.2  radish.example.com radish
```

### DNS

The Internet's native name server is called DNS, the Domain Name Service. It uses a distributed database of records that are automatically disseminated to those who need them. If a DNS server receives a query about a host for which it has no information, it passes the request to an authoritative server (that is, a server which is responsible for maintaining accurate information about the domain in question). The server then caches the information it receives from the authoritative server, and uses the cached version to answer equivalent queries in the future.

The DNS uses a hierarchy of hostnames similar to the hierarchy of filenames in the UNIX file system. There is a DNS root domain at the top of the hierarchy, served by a group of DNS domain servers called the root servers.

### Geographic and Organizational Domains

Directly under the root domain are the top-level domains. These fall into two categories, geographic and organizational. Geographic domains exist for each country, and are named with a two-letter code that usually (but not always) corresponds to the ISO-3166 two-letter code. (For example, there is a top-level domain named UK for the United Kingdom, but the ISO-3166 code is GB.) Membership in the organizational domains is based on the type of organization to which the system belongs. The categories are shown in Table 14.3.

### TABLE 14.3 Membership of DNS Organizational Domains

| Domain | Description |
|---|---|
| com | Commercial organizations |
| edu | U.S. educational institutions |
| gov | U.S. government agencies |
| mil | U.S. military organizations |
| net | Network support organizations |
| int | International governmental or quasi-governmental organizations |
| org | Other types of organizations, including non-profits |
