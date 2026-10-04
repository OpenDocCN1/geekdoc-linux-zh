# Attacking and Defending DNS • Chapter 8

+   - The server with authority is the trusted server based on the chain of trust delegated from root servers.
- Zone records (see Table 8.2) are the different types of information each domain can hold.

# ### Table 8.2 Common Zone Records

| Record Symbol | Record Meaning | Explanation |
| --- | --- | --- |
| NS | Name server | This record will return the name of the authoritative server for the requested domain. |
| SOA | State of authority | This record gives information about the zone, such as administrator contact, and timeouts and intervals. |
| PTR | Pointer records | This record associates an IP address with a canonical name (normally used for reverse DNS records). |
| A | IP address | This assigns an IP address to a host or canonical name. |
| CNAME | Canonical name | This returns a host or canonical name. |
| TXT | Text | Displays possible comments about the requested domain. |
| AAAA | IPv6 | Similar to an A record but returns the IPv6 address of the requested domain. |

The demand for new technology has pushed DNS to support a plethora of additional DNS records. Recently, the new AAAA record was added over time as necessary. The primary DNS technology has been manipulated over the years to support everything from virtual private networking (VPN) and domain controller entries to trusted Public Key Infrastructure (PKI) exchanges. The primary DNS structure has sustained the test of time and will be included in the core data communication structures for years to come.

![](bbox=[0.71, 0.943, 0.927, 0.966])