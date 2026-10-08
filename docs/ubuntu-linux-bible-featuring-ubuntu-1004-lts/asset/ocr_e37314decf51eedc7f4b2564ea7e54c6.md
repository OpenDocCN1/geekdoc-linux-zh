# Part III: Ubuntu System Administrators

2. Assuming the hostname or IP address of a specific host is not found in the /etc/hosts file, a system that is configured to consult DNS checks the contents of the text file / /etc/resolv.conf to identify the DNS servers that it should consult, in order. This file also often contains information such as the default domain that should be queried when up non-fully qualified hostnames. For example, the /etc/resolv.conf on one of my Ubuntu systems looks like the following:

```
domain vonhagen.org
ameserver 0.0.0.0
nameserver 192.168.66.64
nameserver 208.67.222.222
nameserver 208.67.220.222
```

In this example, non-fully qualified hostnames as 64bit are assumed to be within the domain vonhagen.org. The name servers are queried in order until one responds or a maximum number of connection failures and associated retries have elapsed, in which case the query fails. The name servers 208.67.222.222 and 208.67.220.222 are public name servers from the folks at OpenDNS.com, which provide public name services and are are well worth checking out! For a list of publicly available DNS servers all over the world, see www.serverlist.org.

# Tip

A name server specification of 0.0.0.0 is actually a shortcut for querying a local name server using the first IP address assigned to the local system. This is the loopback address, which is usually 127.0.0.1, but is not guaranteed to be. Using the shortcut 0.0.0.0 causes your request to be sent to an IP address that is known to be valid for the current host, whatever it may be.

3. When a DNS server responds, it first tries to resolve the query itself. DNS servers are configured through many specially formatted text files that are essentially anonymous to a domain or subdomain that the server can provide authoritative information for. If the hostname or IP address re\u001 is present in a zone where the DNS server is authoritative for or if it is already present in the server's cache of previously answered requests, the DNS server will reply directly to the request. If the request is in a subdomain that the DNS server knows an authoritative server for information for, it will forward the request to that DNS server for resolution. The DNS server will then reply to the client.

4. If the DNS server reports cannot resolve the query in one way or another, it queries one of the Internet's top-level name servers (as root servers) to identify the name server that is responsible for the domain or the range of IP addresses that contains the IP address for which the application is looking for hostname information.

5. The root name server returns a pointer to the appropriate name server, which your system queries for hostname or IP address. If this name server is not actually authoritative for the domain or IP address that you are querying, it may forward the query to other name servers—this hierarchy continues until a name server is found that is actually authoritative for the domain or IP address that you are querying.