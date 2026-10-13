# # AutoClient Configuration

An *AutoClient* is similar to a diskless client, except that it has a limited amount of local storage space (minimum of 100MB) used for a specific purpose. Like the diskless client, the AutoClient must remotely access its root (/) and /usr file systems from an OS server configured as an AutoClient server. Unlike the diskless client, the AutoClient uses local disk space to store or cache the root (/) and /usr file systems.

In addition, the local hard disk is used for swap space. Like the diskless configuration, the OS server provides hard disk space for the /home and /var file systems that are unique to each diskless client.

Compared to the diskless configuration, the AutoClient configuration is somewhat more expensive because its client requires a hard disk; however, the hard disk is small. Like the diskless configuration, only one copy of common files is required, and this copy is shared among the clients. In addition, all data unique to each client is stored on an OS server, simplifying backup and restore procedures. Therefore, in terms of client hardware, AutoClients, like diskless clients, can be replaced or upgraded easily.

The disadvantages of the diskless configuration are reduced or, in some cases, eliminated by the AutoClient configuration. After the AutoClient has cached the operating system, it no longer requires access to the OS server for those files. In addition, the local swap space eliminates much of the network load.

# # Comparison of Configurations

Table 13.6 compares the significant differences among the system configurations supported in the Solaris 8 network environment.

**Table 13.6  A Comparison of System Configurations**

| System Type | Local Swap | Local File Systems | Remote File Systems |
|---|---|---|---|
| Standalone | Yes | root, /usr, /var, /export/home | None or optional |
| Diskless client | No | None | root, /usr, /var, /home |
| AutoClient | Yes | root, /usr | /var, /home |

Standalone systems that function as servers typically provide file systems——such as /export/root, /export/home, and /export/swap——that store files remotely accessed by diskless clients and AutoClients. In addition, servers and standalone systems provide the /opt file system for storing application software.