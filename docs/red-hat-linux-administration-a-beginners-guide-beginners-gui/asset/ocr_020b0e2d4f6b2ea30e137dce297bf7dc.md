Once the databases are established on the server, clients can query the server for database entries. Typically this happens when a client is configured to look to the NIS *map* when an entry cannot be found in the client’s local database. A host may have a simple file containing only those entries needed for the system to work in single-user mode (when there is no network connectivity)—for example, the /etc/passwd file. When a program makes a request to look up user password information, the client checks its local *passwd* file and sees that the user doesn’t exist there; the client then makes a request to the NIS server to look for a corresponding entry in the *passwd* table. If NIS does have an entry, it is returned to the client and then to the program that requested the information in the first place. The program itself is unaware that NIS was used. The same is true if the NIS map returns an answer indicating that the user password entry does not exist. The program would be passed the information without knowing how much activity had happened in between.

This of course applies to all the files that we tell NIS to share. Other popular shared files include /etc/group and /etc/hosts.

> **NOTE**
> 
> *Although it is technically correct to refer to NIS’s tables as a database, they are more typically called maps. (In this context, we are mapping keys to values.) Using the /etc/passwd file as an example, we map a user’s login name (which we know is always unique) to the rest of the password entry.*

# # The NIS Servers

NIS can have only one authoritative server where the original data files are kept (this is somewhat similar to DNS). This authoritative server is called the *master* NIS server. If your organization is large enough, you may need to distribute the load across more than one machine. This can be done by setting up one or more *secondary (slave)* NIS servers. In addition to helping distribute the load, secondary servers also provide a mechanism to better handle server failures. The secondary NIS server can continue answering queries even while the master or other secondary servers are down.

> **NOTE**
> 
> *A server can be both a server and a client at the same time.*

Secondary NIS servers receive updates whenever the primary NIS server is updated, so that the masters and slaves remain in sync. The process of keeping the secondary servers in sync with the primary is called a *server push*. As part of its update scripts, the NIS master also pushes a copy of the map files to the secondary server. Upon receiving these files, the secondary servers update their databases, as well. The NIS master does not consider itself completely up-to-date until the secondary servers are up-to-date, as well.