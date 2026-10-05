# Networking and Internet Services
PART II

> Note
The preceding example placed the virtual domain in the host's subnet. It can be in a different subnet (and often is). In that case, a new reverse DNS zone data file must be set up for the additional subnet, and several routing and forwarding steps must be taken so the different subnet is visible to browsers around the world.

# Delegating Authority

With millions of domain names and URLs on the Internet, the only way to keep track is with a distributed system. DNS implements this distribution through delegation to subdomains.

This section implements a trivial delegation whose purpose is illustrative only. No MX, no CNAME, no secondary server, not even reverse DNS. Just the same subnet as the rest of the examples in this chapter.

Imagine that a new department, called subdomain, wants to administer their own DNS. That makes less work for the domain.cxm administrators. Table 8.2 shows that the department has four hosts.

Table 8.2 The Subdomain Department's Servers
| Host | IP |
|---| sylvia | 192.168.42.40 |
| brett | 192.168.42.41 |
| rena | 192.168.42.42 |
| valerie | 192.168.42.43 |

From a DNS point of view, the four hosts are sylvia.subdomain.domain.cxm, brett.subdomain.domain.cxm, rena.subdomain.domain.cxm, and valerie.subdomain.domain.cxm. domain.cxm. The nameserver for subdomain.cxm is on host sylvia. The following is a synopsis of the steps to accomplish this:

+   1. Add authority for subdomain.domain.cxm on sylvia.
2. Test the subdomain, domain.cxm local resolution.
3. Delegate from namark to sylvia for the subdomain.
4. Test the subdomain.domain.cxm delegation.