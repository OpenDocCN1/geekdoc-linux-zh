| Query Option | Enables You To |
|---|---|
| +tcp | Set the resolver to use the TCP service to query the name server. |
| +domain=somename | Create a search list for desired domains. |
| +search | Configure the resolver to use the search list specified in the /etc/resolv.conf file or through the +domain option. |
| +nsearch | Configure the resolver to search for name servers based on the zones in which they are defined. |
| +identify | Display the IP address and port number of the name server that answers the query. |
| +trace | Trace the DNS query for root name server information from the /etc/resolv.conf file. |

# Syntax

The syntax of the dig utility is dig [command options] [query options] [Fully Qualified Domain Name | IP address].

# The host Utility

The host utility is a DNS lookup utility, similar to the dig utility. It is used to convert system names to IP addresses and vice versa. The host utility has various options.

![](bbox=[0.04, 0.41, 0.12, 0.49])

| Option | Enables You To |
|---|---|
| name | Set the domain name to be looked up by the host utility. |
| -t {query type} | Set the type of query to be sent to the name server. |
| -W {seconds} | Set the time the resolver must wait for a reply before quitting. |
| -s | Force the resolver to terminate the querying process once it fails without retrying. |

# Syntax

The syntax of the host utility is host [Command Options] {FQDN | IP Address}.