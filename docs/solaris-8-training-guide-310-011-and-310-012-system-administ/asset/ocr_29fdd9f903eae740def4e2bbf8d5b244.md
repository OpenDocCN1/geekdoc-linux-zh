of client can create much network traffic, so make sure your network has the needed capacity. The JavaStation has no local administration; booting, administration, and data storage are handled by servers via the network.

# AutoClient

An AutoClient system is nearly identical to a diskless client, except that it caches all of its needed system software from a server. AutoClient systems use Solaris diskless and CacheFS technologies. CacheFS is a general-purpose, file-system caching mechanism that improves performance and scalability by reducing server and network load. (See Chapter 17, “The NFS Environment,” for a complete description of how CacheFS works.) An AutoClient system has the following characteristics:

+   - It requires a 100MB or larger local disk for swapping and caching. Its root (/) file system and the /usr file system are on a server somewhere on the network, but they are cached locally.
- It can be set up so that it can continue to access its cached root (/) and /usr file systems when the server is unavailable.
- It relies on servers to provide other file systems and software applications.
- It contains no permanent data, making it a field-replaceable unit (FRU).

An AutoClient system uses its local disk for swap space and to cache its individual root (/) file system and the /usr file system from a server’s file systems. With the AutoClient configuration, administration is streamlined because the system administrator can maintain many AutoClient systems from a central location. Changes do not have to be made on individual systems. You must obtain a license for each AutoClient system you want to add to your network.

Table 3.2 gives a brief overview of each system configuration. It outlines which file systems are local and which are accessed over the network.