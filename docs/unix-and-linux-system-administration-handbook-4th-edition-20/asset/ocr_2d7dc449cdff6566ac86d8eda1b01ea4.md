induce the wrath of upset users, but it's taken a lot of work and experience to get this point.

# Issues of state

One of the design decisions made when designing a network filesystem is determining what part of the system will track the files each client has open, information referred to generically as “state.” A server that does not record the status of files and clients is said to be stateless; one that is stateful. Both approaches have been used over the years, and both have benefits and drawbacks.

Stateful servers keep track of all open files across the network. This mode of operation introduces many layers of complexity (more than you might expect) and makes recovery in the event of a crash far more difficult. When the server returns from a hiatus, a negotiation between the client and server must reconcile the last known state of the connection. Statelessness allows clients to maintain more control over files and facilitates the management of files that are opened in read/write mode.

On a stateless server, each request is independent of the requests that preceded it. If either the server or the client crashes, nothing is lost in the process. Under this design, it is painless for servers to crash or reboot, since no context is maintained. However, it's impossible for the server to know which clients have opened files for write, so the server cannot manage concurrency.

# Performance concerns

Network filesystems should provide users with a seamless experience. Accessing a file over the network should be no different from accessing a file on a local filesystem. Unfortunately, wide area networks have high latencies, which causes operations behave erratically, and low bandwidth, which results in slow performance for larger files. Most file service protocols, including NFS, incorporate techniques to minimize performance problems on both local and wide area networks.

Most protocols try to minimize the number of network requests. For example, read-ahead caching reads portions of a file into a local memory buffer to avoid delay when a new section of the file is read. A little extra network bandwidth is consumed in an effort to avoid a full round trip with the server. Similarly, some systems cache writes in memory and remember their updates in batches, reducing the delay incurred when communicating write operations to the server. These types of batch operations are generically referred to as request coalescing.

# Security

Any service that provides convenient access to files on a network has great potential to cause security problems. Local filesystems implement access control algorithms, safeguarding files with granular access permissions. On a network, the problems are multiplied since there may be race conditions