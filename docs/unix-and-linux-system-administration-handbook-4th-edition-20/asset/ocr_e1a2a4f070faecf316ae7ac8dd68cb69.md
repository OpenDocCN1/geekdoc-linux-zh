# Summing up

about the same rate that new ones are being inserted. Once stable, the system should not be swapping, and its paging rates should be reasonable.

If your name server runs on a dedicated machine, a good rule of thumb is for the machine to double the amount of memory consumed by the name server daemon after it has been running for a week. The top and vmstat commands show memory usage; see Analyzing memory usage page 1125 for more details.

Authoritative servers need enough memory to store all the data for which they are authoritative. Most sites can manage this, but for top-level domains and DNS hosting sites may need huge memory or special software that facilitates storing part of the data on.

You can control the amount of resources that a name server uses through configuration options. See the list of tuning options for BIND on page 608 and for dns on page 630.

# Security

DNS security is covered in a whole section of its own, starting on page 642. We won't duplicate this discussion here except to remind you that if you use a firewall, be sure that your DNS system does not emit queries to your firewall blocks the answers. Make sure that your DNS administrators have ongoing communication with your security and network administrators.

By default, DNS uses UDP with random unprivileged source ports (>1023) for queries; the answers are UDP packets addressed to those ports. DNSSEC and internationalized domain names, DNS responses may be larger than the path MTU and therefore fragmented. Ergo, your firewall should not block fragmented UDP packets. If a UDP query fails due to fragmentation, often it is issued as a TCP query, so your firewall should be kind to TCP DNS replies, too.

# Summing up

Exhibit B illustrates the design recommended in the previous paragraphs.

# Exhibit B DNS server architecture

![](bbox=[0.265, 0.735, 0.855, 0.915])