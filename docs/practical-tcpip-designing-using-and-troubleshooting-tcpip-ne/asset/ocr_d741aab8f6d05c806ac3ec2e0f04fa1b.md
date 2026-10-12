# ## Summary

+   - DNS names are organized hierarchically in a tree structure. Each node in the tree is a domain name

+   - the DNS database is distributed. One DNS server will often call on another to obtain the information needed to resolve a query

+   - authority for parts of the DNS tree are delegated to various organizations. These can in turn delegate parts of their sub-tree to other organizations, and so on

+   - DNS servers hold databases of name and IP number details. The part of the tree they have authority for is called a zone. A zone is not the same as a domain, although they frequently coincide, especially at end-user sites

+   - to resolve a name the DNS often has to follow the chain of delegation through several steps, getting progressively more detailed information at each step until finally it gets the full details for the name it's trying to resolve

+   - DNS servers are configured in many different ways, to fulfill different roles: primary and secondary servers are authoritative for a zone, caching-only servers improve DNS performance for their clients, and forwarders just rely on other servers to do all their work for them

+   - you can run your own DNS server(s) to resolve the names of your internal machines on your private LAN. These servers should not normally be visible from outside your site and are usually separate from the DNS server that holds the public entries (Web and mail server addresses, etc.) for your site

+   - for internal name lookups especially, you can configure your client resolver with either a domain name or a searchlist, which makes it easy for you to refer to a machine by a simple name rather than having to specify its fully qualified domain name

+   - reverse lookups convert IP numbers to their corresponding names. The mechanisms used are exactly the same as for name lookups. However they use the root servers for the special domain name in-addr.arpa to access the tree of IP numbers as opposed to more common tree of names.

# ## What's next?

Troubleshooting the DNS.

# ## Notes and related reading

The Oxford English Dictionary defines “domain” as “a district or region under rule, control, or influence, or contained within certain limits; realm; sphere of activity, influence, or dominion.” Your DNS domain is a specific part of the name space that is dedicated to you, so you can create your own names without clashing with anyone else's.