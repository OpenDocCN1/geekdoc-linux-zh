![](bbox=[0.18, 0.08, 0.88, 0.35])

Figure 24-3  DNS structure showing zones

+   * Delegation of authority

When referring to DNS, the term delegation means delegation of authority. ICANN (Internet Corporation for Assigned Names and Numbers, www.icann.org) delegates authority to the root and top-level domains. In other words, ICANN says which servers are authoritative for these domains. Authority is delegated to each domain below the top-level domains by the authoritative server at the next-higher-level domain. ICANN is not authoritative for most second-level domains. For example, Ubuntu is authoritative for the ubuntu.com domain. This scheme of delegating authority allows for local control over segments of the DNS database while making all segments available to the public.

# QUERIES

There are two types of DNS queries: *iterative* and *recursive*.¹

+   * Iterative queries

An iterative query sends a domain name to a DNS server and asks the server to return either the IP address of the domain or the name of the DNS server that is authoritative for the domain or one of its parents: The server does not query other servers when seeking an answer. Nameservers typically send each other iterative queries.

+   * Recursive queries

A recursive query sends a domain name to a DNS server and asks the server to return the IP address of the domain. The server may need to query other servers to get the answer.

Both iterative and recursive queries can fail. In this case, the server returns a message saying it is unable to locate the domain.

1. A third type of query is not covered in this book: inverse. An inverse query provides a domain name given a resource record. Reverse name resolution (page 831), not an inverse query, is used to query for a domain name given an IP address.