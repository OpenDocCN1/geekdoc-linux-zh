# ## Adapting to Different Load Levels

The parent's primary responsibility is to make sure that enough child processes are available to serve the incoming connections. This responsibility must be balanced against your computer's resource load. If you are not careful, the clients may begin to drop off due to timeouts because your server does not have enough listeners serving connections.

Using a dedicated number of listeners (*servlets*) forces a limit on the number of active connections. This is the primary restriction on having preforked servlets. Nevertheless, the idea of limiting the number of processes that your program creates and destroys is a good one. It lessens the turmoil on your process table and system resources. What might be a good way to minimize creation and destruction while meeting the needs of connecting clients?

You could make the servlet algorithm adaptable to the demands of the system. Your server has to respond to two different challenges: knowing when to create more servlets and knowing when to terminate extra ones. The second challenge is simple: The servlet terminates itself if it is idle for a while.

The first challenge, knowing when to create more servlets, is not so direct. You may recall that every TCP server has a listening queue (that is what the `listen()` system call does). The network subsystem enqueues every connection request, and the `accept()` system call acknowledges and creates a dedicated channel to the client. If a client sits in a queue too long, it may only wait for a couple of minutes before giving up.

Being able to see how many pending connections the queue has and what is the longest waiting request might help server tuning. You could use this information to monitor the system's responsiveness to the requests. As the queue fills, the server can create more servlets. If the connection delay gets too long, you may simply adjust the servlet's self-termination delay. Unfortunately, this is not something that the API calls offer. If you want servlet adaptability, you must use another approach.

One method of creating new servlets to respond to a volume of requests is like chumming fish. Where legal, fishermen cast out samples (chum) of different kinds of bait. The bait the fish eats is the bait the fisherman uses. The fish's response also indicates how large the school is.

Like chumming, the server throws out an extra servlet every once in a while. As long as the same number of extras terminate as were created (because there's nothing to do), the server continues this process. When the servlets stop terminating, your server increases the number of extra servlets it creates until the number stabilizes again.

The purpose of preforking is to minimize the time of creating and cleaning up after servlets. Creating and terminating servlets haphazardly brings you back to forking for every new connection. You have to plan carefully to avoid this result. Also, your algorithm must have a minimum number of servlets running for this to work.

This is where statistics help a little. The adapting algorithm has to face three possibilities: The number of connections is stable, it is increasing, or it is decreasing. If the number of connections is stable, the server sees the same number of servlets terminating as are created during a given period of time. For example, if your server creates a servlet every 60 seconds (with a 30-second idle timeout), you may see the first pattern in the diagram in Figure 9.1.

**Figure 9.1.** *Extra servlets are thrown out to see if connections are pending.*