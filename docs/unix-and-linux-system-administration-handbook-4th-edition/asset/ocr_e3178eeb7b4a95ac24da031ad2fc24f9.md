memory. max-cache-size limits the amount of memory the server will use for caching answers to queries. If the cache grows too large, named deletes records before their TTLs expire, to keep memory use under the limit.

IP port utilization
use-v4-udp-ports { range beg end; }; [range 1024 65535]
use-v6-udp-ports { range beg end; }; [range 1024 65535]

avoid-v4-udp-ports { port_list }; [empty]
avoid-v6-udp-ports { port_list }; [empty]

query-source v4-address [ port ] [any] # CAUTION, don’t use port
query-source v6-address [ port ] [any] # CAUTION, don’t use port

Source ports have become important in the DNS world because of a weakness in the DNS protocol discovered by Dan Kaminsky that allows DNS cache poisoning when name servers use predictable source ports and query IDs. The use- and avoid- options for UDP ports together with changes to the named software have mitigated this attack. Do not use the query-source address options to specify a fixed outgoing port for DNS queries or you will undo the Kaminsky protection that a large range of random ports provides.

The defaults for the use-v*-udp-ports are fine and you shouldn’t need to change them. If your firewall blocks certain ports in this range (for example, port 2049 for SunRPC) then you have a small problem. When your name server sends a query and uses one of the blocked ports as its source, the firewall blocks the answer, and the name server eventually stops waiting and sends out the query again. Not fatal, but annoying to the user caught in the crossfire.

To avoid this problem, use the avoid-v*-udp-ports options to make BIND stay away from the blocked ports. Any high-numbered UDP ports blocked by your firewall should be included in the list.19 If you update your firewall in response to some threatened attack, be sure to update the port list here, too.

The query-source options let you specify the IP address to be used on outgoing queries. For example, you might need to use a specific IP address to get through your firewall or to distinguish between internal and external views.

Queries go out from random high-numbered ports, and the answers come back to those same ports. Ergo, your firewall must be prepared to accept UDP packets on random high-numbered ports. Some sysadmins used to set a specific outgoing port number so that they can configure the firewall to recognize it and accept UDP packets only for that port. However, this configuration is no longer safe in the post-Kaminsky era.

If you use the query-source option, specify only the IP address from which you want queries to be sent; do not specify a port number.