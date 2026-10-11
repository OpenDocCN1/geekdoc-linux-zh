![](bbox=[0.22, 0.08, 0.88, 0.32])

# **Figure 24-4**   A recursive query that starts several iterative queries to find the answer

resolver communicates with a single DNS server, which can perform multiple iterative queries in response to the resolver’s recursive query.

All DNS servers must answer iterative queries. DNS servers can also be set up to answer recursive queries. A DNS server that is not set up to answer recursive queries treats a recursive query as thought it is an iterative query.

In Figure 24-4, the resolver on a client system is trying to discover the address of the server `ftp.site1.example.com.` on the network with the DNS layout shown in Figure 24-3 on page *777*. The resolver on the client sends a recursive query to its primary DNS server. This server interrogates the root server and one additional server for each zone until it receives an answer, which it returns to the resolver on the client. In practice, the query would not start with the root server because most servers usually have the location of the authoritative nameserver for the `com` domain stored in cache (memory).

# # SERVERS

There are three main types of DNS servers: primary (master), secondary (slave), and caching-only.

+   • A *primary master server*, also called a *primary server* or *master server*, is the authoritative server that holds the master copy of zone data. It copies information from the *zone* or *master file*, a local file that the server administrator maintains. For security and efficiency, a primary master server should provide iterative answers only. A primary master server that provides recursive answers is more easily subverted by a *DoS attack* (page *1080*) than one that provides iterative answers only.

+   • *Slave servers*, also called *secondary servers*, are authoritative and copy zone information from the primary master server or another slave server.