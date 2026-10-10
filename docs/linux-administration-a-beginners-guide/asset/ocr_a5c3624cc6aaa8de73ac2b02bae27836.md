This of course applies to all the files that we tell NIS to share. Other popular shared files include /etc/group and /etc/hosts.

> **NOTE:** Although it is technically correct to refer to NIS's tables as a database, they are more typically called maps. (In this context, we are mapping keys to values.) Using the *list*/*passwd* file as an example, we map a user's login name (which we know is always unique) to the rest of the password entry.

# The NIS Servers

NIS can have only one authoritative server where the original data files are kept (this is somewhat similar to DNS). This authoritative server is called the *master* NIS server. If your organization is large enough, you may need to distribute the load across more than one machine. This can be done by setting up one or more *secondary* (slave) NIS servers. In addition to helping distribute the load, secondary servers also provide a mechanism to better handle server failures. The secondary NIS server can continue answering queries even while the master or other secundaries are down.

Secondary NIS servers receive updates whenever the *primary* NIS server is updated, so that the masters and slaves remain in *sync*. The process of keeping the secundaries in sync with the primary is called a *server push*. The NIS master, as part of its update script, also pushes a copy of the map files to the secundaries. Upon receiving these files, the secundary servers update their databases as well. The NIS master does not consider itself completely up-to-date until the secundaries are up-to-date as well.

> **NOTE:** A server can be both a server and a client at the same time.

# Domains

Primary NIS servers establish *domains* that are similar to the domains of a PDC. A significant difference is that the NIS domain does not require the NIS server administrator to explicitly allow a client to join. Furthermore, the NIS server only sends out data; it does not perform authentication. The process of authenticating users is left to each individual host; NIS merely provides a centralized list of users.

> **NOTE:** Bear in mind that the NIS model assumes that all clients are members of the same administrative domain and are thus managed by the same system administrators.

> **TIP:** Since NIS domains must be given names, it's a good practice (though not mandatory) to use names that are different from your DNS domain names. You'll have a much easier time discussing your network domains with fellow administrators when everyone knows which is which.