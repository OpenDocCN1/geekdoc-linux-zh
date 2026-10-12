matter which one a resolver asks. The distinction between master and slave is made purely for reasons of reliability—to ensure that the failure of a single nameserver does not result in the loss of authoritative data for the domain. As a bonus, this redundancy also distributes the network load between several hosts so that no one nameserver is overwhelmed with requests for authoritative information.

> **NOTE**
> As a DNS administrator, it is your responsibility to ensure that your nameservers provide sufficient redundancy for your zones. Your slaves should be far away from the master so that power failures, network outages, and other catastrophes do not affect your name service.

Despite these precautions, the load on DNS servers would be crushing without the extensive use of local caches. As mentioned before, nameservers are allowed to cache the results of queries and intermediate referrals for some time so that they can serve repeated requests for data without referring to the source each time. If they did not do this, root nameservers (and the nameservers for other popular zones) would be contacted by clients all over the world for every name lookup, wasting a huge amount of resources.

# Name Resolution in Practice

When a web browser issues a request for an IP address, the request is sent to a local nameserver, which resolves the name, stores the result in its cache, and returns the IP address. To better understand this process, take a moment to see what happens behind the scenes when a web browser issues a request for the IP address of www.ibm.com. This example mimics the actions of the resolver by using the incredibly useful dig utility to follow the chain of delegations between zones until you find the A record you are looking for. Because most nameservers would follow the delegations for you, this example uses the +norec dig parameter to turn off recursion. That is, if the nameserver does not know how to answer your query, it will not issue further queries on its own.

> **NOTE**
> There are 13 root nameservers around the world. Several are located in the United States—Virginia, California, and Maryland. Others are located in London, Stockholm, and Tokyo. These root servers do not hold “master lists” of IP addresses and domain names, but simply hand off requests to other nameservers.
> 
> After a recent DOS (Denial of Service) attack on the root servers, at least one of them now runs an alternative application to BIND.

Begin by randomly selecting one of the 13 root nameservers (ranging from a.root-servers.net to m.root-servers.net; we picked e), and ask what it knows about an A record for www.ibm.com:

```
```
$ dig @e.root-servers.net www.ibm.com A +norec
```
```