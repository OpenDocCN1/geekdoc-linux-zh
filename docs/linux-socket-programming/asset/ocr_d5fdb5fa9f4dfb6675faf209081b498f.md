You can use this algorithm to create a few processes—much less than the number you can create in a purely multitasking server— for example, 5–10 servlets. Each servlet, in turn, could support 5–10 connections.

# NOTE

# Select Collision

You may have heard of a BSD problem called *select collision*. The previous algorithm assumes that the select() can wait on several descriptors and wake up only when the descriptors change state. The BSD 4.4 implementation has a limitation that causes all processes blocked in a select() to wake up. It appears that Linux does not have this limitation.

This approach could easily support hundreds of connections without interfering with each other. The balance between the number of tasks and the number of connection helps minimize the impact on the process table. However, having so many connections can lead to problems if you need to track your protocol's state.

You can use this algorithm easily with stateless servers. A stateless connection remembers nothing about previous transactions. This requires all transactions sent to your server to have no relationship with other transactions or each connection to have a single transaction. Also, if your server requires short- to medium-term connections, you can use this approach. Some examples are an HTTP server, a DB query server, and a Web redirector.

# Implementation Problems

As you might have noticed, this approach does have a couple of limitations. First, the primary server cannot balance the number of connections between each servlet. You can add code to place a ceiling on the number of connections:

```
```
 /*************************************************************/
 /** Limiting the number of connections to a servlet ***/
 /*************************************************************/
 if ( FD_ISET(sd, &set) )
 if ( ceiling < MAXCONNECTIONS )
 {
 int client = accept(sd, 0, 0);
 if ( maxfd < client )
 maxfd = client;
 FD_SET(client, &set);
 ceiling++;
 }
```
```

This approach effectively yields the connection to another servlet. However, the distribution of connections between your servlets may be random.

The other problem is with regard to the context of your connection. When a client connects to your server, unless it is a single-transaction connection, your server passes through different states. For example, state one is login and state two is a session.

The previous code fragment always returns to the point of waiting for and getting some message. If you want to incorporate states, you must track where each connection is. With this information, you