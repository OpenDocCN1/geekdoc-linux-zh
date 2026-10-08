The values of the count and destination type fields in the route command determine the presence of the G and H flags in the netstat -r display and thus the route type, as shown in the following table.

| Count | Destination Type | Flags | Route Type |
|---|---|---|---|
| =0 | network | U | Route to a network directly from the local host |
| >0 | network | UG | Route to a network through a remote host gateway |
| =0 | host | UH | Route to a remote host directly from the local host |
| >0 | host | UGH | Route to a remote host through a remote host gateway |
| =0 | default | U | Wildcard route directly from the local host |
| >0 | default | UG | Wildcard route through a remote host gateway |

# DIAGNOSTICS

The following error diagnostics can be displayed.

add a route that already exists

The specified entry is already in the routing table.

add too many routes

The routing table is full.

delete a route that does not exist

The specified route was not in the routing table.

# WARNINGS

Reciprocal route commands must be executed on the local host, the destination host, and all intermediate hosts if routing is to succeed in the cases of virtual circuit connections or bidirectional datagram transfers.

The HP-UX implementation of route does not presently support a change subcommand.

# AUTHOR

route was developed by the University of California, Berkeley.

# FILES

+   - /etc/networks
- /etc/hosts

# SEE ALSO

netstat(1), ifconfig(1M), ping(1M), getsockopt(2), recv(2), send(2), gethostbyaddr(3N), gethostbyname(3N), getnetbyaddr(3N), getnetbyname(3N), inet(3N), routing(7).