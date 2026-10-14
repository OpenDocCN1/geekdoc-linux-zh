**Table 6.1. NetBIOS Name Resolution Methods**

| Name Resolution Method | Description |
|---|---|
| Local NetBIOS Name Cache | The NetBIOS name cache is stored in memory and keeps a list of recently accessed NetBIOS names and their IP addresses. |
| Local LMHOSTS File | The LMHOSTS file, stored in `%System-Root%\\System32\\Drivers\\etc`, can be parsed to resolve a NetBIOS name to an IP address. Some LMHOSTS entries can be pre-loaded into the NetBIOS name cache for faster access. |
| Local HOSTS File | The local HOSTS file, stored in `%System-Root%\\System32\\Drivers\\etc`, can be parsed in a similar fashion to the LMHOSTS file. |
| NetBIOS Name Server (WINS Server) | The NetBIOS name server (a.k.a. WINS Server) can be queried, via the network, for the mapping. |
| DNS Server | A DNS server can be queried just like a WINS server to return a mapping, although it is not as reliable as a WINS server. |
| Network Broadcast | Usually used as a last-ditch effort, the client can broadcast a request for a specific NetBIOS name to the local network. If the destination host is on-line and “hears” the broadcast, it will respond. Broadcasts are only useful on the local subnet. |

+   - If you are using DHCP, you can specify the NetBIOS node type as one of the DHCP parameters and the NodeType key will be set automatically.

![](bbox=[0.062, 0.803, 0.184, 0.863])

> > Be very careful when manipulating the Windows 2000 Registry. Modifying settings incorrectly can leave your system in an unusable state.

Table 6.2 outlines the different node types and their values, and gives a description of how they affect name resolution.