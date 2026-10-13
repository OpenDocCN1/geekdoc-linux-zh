NetBIOS name-to-IP address mappings can also be hard coded in LMHOSTS tables and stored on each machine. The LMHOSTS table is a flat ASCII file of IP address and name pairs. If both WINS and LMHOSTS information are available for resolving names, clients will first consult their local NetBIOS cache and then WINS before using LMHOSTS information. It is also possible to prime the client NetBIOS cache at system startup with LMHOSTS entries that have been flagged as #PRE (Example 3.2).

# Example 3.2 LMHOSTS Stanza

```
149.110.5.12    Wizard   #PRE
```

The broadcast and point-to-point capabilities of various LAN clients for name-to-address resolution are based on their node type as defined in Table 3.2.

# Table 3.2 Name Resolution Methods

| Node Type | Name Resolution Method |
|---|---|
| B-NODE | Broadcast to resolve names. Uses a mixture of directed and broadcast UDP and TCP for resolving name. All network nodes must listen for broadcasts. |
| P-NODE | Point-to-point only node. Uses directed UDP and TCP connections. Relies on access to name server to resolve names. |
| M-NODE | Mixed node. Tries broadcast first and then point-to-point with name server if no response to broadcast. |
| H-NODE | Hybrid node. Tries point-to-point first and then falls back to broadcast if the name server cannot be contacted. |
| MS ENHANCED | Same as an H-NODE but will also use the |

# Server Message Block (SMB)

Thus, far, we have taken a brief look at MS Windows network services and protocols at the network, transport, and to a limited degree, the session layer. Now we are ready to move higher in the stack and probe the Server Message Block (SMB) protocol, which is where Samba lives and breathes (Figure 3.2). SMB is a session-, presentation-, and application-layer protocol that provides a means for remotely sharing files, printers, and various communication resources between networked computers. The SMB protocol was first defined in a joint Microsoft and Intel document titled Microsoft Networks/OpenNET-File Sharing Protocol in 1987. Early SMB implementations included MS LAN Manager in 1987 and OS/2 LAN Server in 1988. In 1992 SMB became an Open Group interoperability standard, "Protocols for X/Open PC Interworking: SMB, Version 2,