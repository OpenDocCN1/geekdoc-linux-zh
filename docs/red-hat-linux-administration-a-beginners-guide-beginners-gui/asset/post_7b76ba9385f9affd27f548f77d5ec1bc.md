
| Option | Description |
| :--- | :--- |
| `allow-transfer { address-list; }` | Specifies which hosts can perform a zone transfer with your DNS server. In general, this list will include only hosts that are secondaries for your primaries. By default, anyone can perform a zone transfer, but I recommend you restrict this to only those with a legitimate reason to do so. |
| `listen-on { address-list; }` | By default, the `named` server will listen to port 53 for DNS queries on all interfaces, but you can change this by specifying other addresses in `address-list`. Format is the same as for `acl` address list explained earlier. To select which port `named` will listen to, add `port` `portnum` right after the `listen-on` statement but before the first curly brace. Value for `portnum` is the port number you want `named` to listen to. For example: `listen-on port 1031 (192.168.1.1);` tells BIND to listen to port 1031 on the interface configured to be `192.168.1.1`. And `listen-on { 192.168.1.1; };` tells BIND to listen to its default port 53 for DNS queries, on the interface configured to be `192.168.1.1`. |
| `query-source address address [port port;]` | When a server needs to contact another DNS server, it goes by default to any of the IP addresses on the system, and the source port is a random high port (port numbers 1024 to 65535). If you need a particular configuration to allow your DNS server through a firewall, you can specify a specific source `address` and `port` of origin for the message. If you need to specify one but not the other, you can use the wildcard (`*`) character. For example, the statement `query-source address * port 53;` says to send the query from whatever IP address `named` wants to use but from port 53 explicitly. |
| `max--transfer-time-in number;` | Specifies the number of minutes a zone transfer can run before it is terminated. Default is 120 minutes. |
| `transfer-format one-answer/many-answers;` | When the `named` process answers a request, it sends back only one answer at a time (the default), even though there may be space to pack multiple answers into one transfer. This is because old versions of BIND and other DNS servers still in use do not support multiple responses. If you know your DNS server will be working only with other BIND 8.x servers, you can change this option to `many-answers` for improved performance. |
| `transfers-in number;` | Maximum number of inbound zone transfers that can be running concurrently. Default is 10. Increasing this value may speed up the process of updates at the expense of increasing system load. |
| `transfers-out number;` | Maximum number of outbound zone transfers that can be running concurrently. Default is 10. As of this writing, this option is parsed by BIND but is not yet in use. |
| `transfers-per-ns number;` | Maximum number of inbound zone transfers that can be running concurrently from a single remote name server. Default is 2. Can be increased at the expense of more load on the remote name server. |
| `coresize size;` | If *named* crashes, Linux will generate a *coredump*, an image of the memory used by the program at the instant it crashed. Data can be used for “post mortem” analysis by programmers. Be aware: This image may be quite large; if you’re short on disk space for the DNS system, consider limiting the core file size. Default under Linux is unlimited. The *size* parameter can be specified in bytes (no suffix), K, MB, or GB. For example, all of the following are the same value, 1 gigabyte: *coresize 1073741824*; *coresize 1048576K*; *coresize 1024M*; and *coresize 1G*;. |
| `datasize datasize;` | Specifies memory allocated for *named*. Default under Linux = as much memory as you have. The *datasize* value follows the same conventions as the *size* value for *coresize*. Thus *1073741824* is the same as *1048576K* is the same as *1024M* is the same as *1G*. |
| `files number;` | Maximum number of files *named* can open at once. Be aware: The more files BIND has open at once, the more its performance is affected by having to deal with all those file handles. (C programmers are familiar with this issue because of the *select* system call.) |
| `stacksize number;` | Maximum amount of memory *named* can take off the system stack (used to track temporary variables in a program). Default under Linux is no limit. For *number*, follow the same conventions as for *coresize* and *datasize*. |
| `cleaning-interval number;` | Specifies interval between server’s removals of expired records from the cache. Default is every 60 minutes. If set to 0, no periodic cleaning will occur. |
| `interface-interval number;` | By default, the server scans the list of interfaces on the system every 60 minutes. If `listen-on` is enabled (defined earlier in this table), `named` begins listening for DNS requests on any new interfaces it finds. If an interface has disappeared, `named` will stop listening to requests on that interface. If this option is set to 0, the server will check for available interfaces only when `named` is started up. |
| `statistics-interval number;` | Specifies how often the `named` server generates server statistics and deposits them to the log file. Default is every 60 minutes. If set to 0, no statistics are generated. |
| `topology { address-list };` | When multiple forwarders exist, `named` shows preference to servers assumed to be closer than others. By default, the `named` server shows preference to itself and then to servers on the same subnet. You can specify another order of preference (the order of the *address-list*). You can also embed sublists representing a group of addresses. For example, in this configuration, `topology { \ 192.168.3.12; \ { 192.168.11.25; 192.168.42/24; } \ 192.168.8.24; \};` first choice is given to 192.168.3.12, equal preference is shown to 192.168.11.25 and all hosts on the 192.168.42.0 network, and last preference is given to 192.168.8.24. |

# The server Statement

The **server** statement tells BIND specific information about other name servers it might be dealing with. The format of the **server** statement is as follows:

```
server ip-address {
    bogus yes/no;
    transfer-format one-answer/many-answers;
};
```

where *ip-address* is the IP address of the server in question.

The first item in the statement, **bogus**, tells the server whether or not the other server is sending bad information. This is useful in the event you are dealing with another site that may be sending you bad information due to a misconfiguration. The default is "no". The second item, **transfer-format**, tells BIND whether this server can accept multiple answers in a single query response, or whether each answer should be sent separately. The many-answers option is much more efficient, but typically only servers running BIND version 8.x or later can handle this mode.

A sample **server** entry might look like this:

```
server 192.168.3.12 {
    bogus no;
    transfer-format many-answers;
};
```

## Zones

The **zone** statement allows you to define a DNS zone the definition of which is often confused. Here is the fine print: *A DNS zone is not the same thing as a DNS domain*. The difference is subtle, but important.

Let’s review: Domains are designated along organizational boundaries. A single organization can be separated into smaller administrative subdomains. Each subdomain gets its own **zone**. All of the zones collectively form the entire domain.

For example, the *bigcompany.com* is a domain. Within it are the subdomains *.engr.bigcompany.com*, *.marketing.bigcompany.com*, *.sales.bigcompany.com*, and *.admin.bigcompany.com*. Each of the four subdomains has its own *zone*. And *bigcompany.com* has some hosts within it that do not fall under any of the subdomains; thus it has a *zone* of its own. As a result, *bigcompany.com* is actually composed of five *zones* in total.

In the simplest model, where a single domain has no subdomains, the definition of *zone* and *domain* are the same in terms of information regarding hosts, configurations, and so on. The process of setting up zones in the **named.conf** file is discussed in the following section.

![](img/ec2066d370d3af1a767664d36aa7ddfe_343_0.png)

## Configuring Servers

Time for *big fun*: configuring a name server! Oh, you don’t think it’s fun? Well, wait until you find out how much people get paid for knowing this stuff.

Earlier, you learned about the differences between primary, secondary, and caching name servers. Briefly, primary name servers contain the databases with the latest DNS information for a zone. When a zone administrator wants to update these databases, the primary name
