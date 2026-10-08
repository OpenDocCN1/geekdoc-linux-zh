# 414 IP ADDRESSES AND COMPUTER NAMES

computer name itself. The change of an alias requires only a little effort, whereas the change of a computer name can be very complicated.

| IP address | Computer name | Aliases |
| --- | --- | --- |
| 127.0.0.1 | localhost | |
| 192.168.3.155 | pes.example.org | pea |

+   Listing 15.1 Contents of the file /etc/hosts.

In a bigger network, the maintenance of a large number of hosts files is very labour-intensive and easily leads to inconsistencies because different computers you will often find divergent and incomplete name tables. The correspondence between names and addresses should be unique so that on each computer the same hosts can be addressed under the same names. Here, centralized administration is needed to ensure this consistency.

The unique nature of host names can be ensured by means of the Domain Name Service (DNS) for which a name server is set up. All data is centrally maintained on this computer and distributed via the network on demand.

Another alternative is the use of the Network Information Service (NIS) (see Chapter 21). The use of NIS, however, only makes sense in UNIX networks since Windows clients usually cannot handle NIS, whereas they can start NIS requests and use the answers.

# 15.2 Domain Name Service

Setting up a name server is sensible for a variety of reasons. The administrative effort of synchronizing the name tables in a bigger network can be reduced, in particular when Windows and other clients are used which do not allow central administration of hosts files. For dial-up connections it may be sensible to use a cache server. This avoids repeated requests to external name servers. More information on the DNS can be found in [rfc1033], [rfc1034], and [rfc1035].

A name server is responsible (authoritative) for a determined zone. Requests that the name server cannot answer are forwarded to the next higher server, which in turn may also forward the request. Since the superior server does not have all the data of the subordinate servers, it can also forward the request downward to the appropriate server. When you are connected to the Internet, it is therefore important to announce the existence of your own name server, for example to your local NIC. When you apply for your own domain, this is done either by the provider or the responsible Network Information Centre.

To ensure fail-safe operation, there should be at least two name servers for each zone, one primary server and at least one secondary (backup) server..