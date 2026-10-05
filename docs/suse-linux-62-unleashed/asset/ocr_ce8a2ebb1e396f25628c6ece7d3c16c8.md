# Networking and Internet Services

PART II

ARPanet switched to DNS in September 1984, and it has been the standard method for publishing and retrieving hostname information on the Internet ever since.

DNS is a distributed database built on a hierarchical domain structure that solves the inefficiencies inherent in a large monolithic file such as hosts.txt. Under DNS, every computer that connects to the Internet does so from an Internet domain. Each Internet domain has a nameserver that maintains a database of the hosts in its domain and handles requests for hostnames. When a domain becomes too large for a single point of management, subdomains can be delegated to resolve the administrative burden.

# /etc/hosts File

Although DNS is the primary means of name resolution, the /etc/hosts file is still found on most machines. It can help to speed up the IP address lookup of frequently requested addresses, such as the IP address of the local machine. Also, during boot time, machines need to know the mapping of some hosts to IP addresses (for example, your NIS servers) before DNS can be referenced. The IP address-to-hostname mapping for these hosts is kept in the /etc/hosts file.

The following is a sample /etc/hosts file:

| IP Address | Hostname | Alias |
| 127.0.0.1 | localhost | |
| 192.168.42.7 | vestax | www |
| 192.168.42.8 | mailhub | mailhub.domain.cxm |
| 192.168.42.6 | technics | |

The leftmost column is the IP address to be resolved. The next column is the hostname corresponding to that IP address. Any subsequent columns are aliases for that host. The second line, for example, the address 192.168.42.7 is for vestax. Another name for vestax is www. The domain name is automatically appended to the hostname by the system. However, many people append it themselves for clarity (for example, www.domain.cxm).

> Use of the .cxm domain name prevents conflict with any existing .com domain.

For the very least, you need to have the entries for

+   - Localhost