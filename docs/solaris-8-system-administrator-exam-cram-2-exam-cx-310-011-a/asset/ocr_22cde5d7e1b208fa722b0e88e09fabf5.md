| Keyword | Maps | Description |
|---|---|---|
| aliases | mail.aliases, mail.byaddr | Mail addresses and aliases |
| bootparams | bootparams | Location of root, swap, and dump partitions for diskless workstations |
| ethers | ethers.byaddr, ethers.byname | Ethernet addresses of systems |
| group | group.bygid, group.byname | Group name, group ID (GID), and member information |
| hosts | hosts.byaddr, hosts.byname | Hostnames and network (IPv4) addresses |
| ipnodes | ipnodes.byaddr, ipnodes.byname | Hostnames and network (IPv6) addresses |
| netgroup | netgroup, netgroup.byhost, netgroup.byuser | Network groups and members defined in the domain |
| netmasks | netmasks.byaddr | Netmasks associated with known networks |
| networks | networks.byaddr, networks.byname | Networks and their associated names |
| passwd | netid.byname, passwd.adjunct.byname, passwd.byname, passwd.byuid | Password information for user accounts |
| protocols | protocols.byname, protocols.bynumber | IP protocols used within the domain |
| rpc | rpc.bynumber | RPC program numbers for RPC services used within the domain |
| services | services.byname, services.byservice | IP services and their port numbers |

![](bbox=[0.148, 0.711, 0.256, 0.783])

NIS was previously known as “Yellow Pages.” For this reason, many of the NIS files and commands contain the yp prefix.

# NIS Master and Slave Servers

Each NIS environment, or domain, must have only one NIS master server. The NIS maps reside on the master server. To provide load distribution and redundancy, one or more slave servers can be configured. Whenever the NIS maps are updated on the master server, they are propagated to the slave servers.