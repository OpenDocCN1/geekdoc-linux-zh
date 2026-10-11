```
/*---In Child---*/
maxfd = sd;
FD_SET(sd, &set);
for (;;) 
{
    struct timeval timeout={2,0};                /* 2 seconds */
    /*---Wait for some action---*/
    if ( select(maxfd+1, &set, 0, 0, &timeout) > 0 )
    {
        /*---If new connection, connect and add to list---*/
        if ( FD_ISSET(sd, &set) )
        {
            int client = accept(sd, 0, 0);
            if ( maxfd < client )
                maxfd = client;
            FD_SET(client, &set);
        }
        /*---If command/request from client, process---*/
        else
        {
           /** Process client's request ***/
           /** If client just closed, remove from list ***/
        }
    }
}
```

You can use this algorithm to create a few processes—much less than the number you can create in a purely multitasking server—for example, 5–10 servlets. Each servlet, in turn, could support 5–10 connections.

> **Select Collision**
> You may have heard of a BSD problem called *select collision*. The previous algorithm assumes that the `select()` can wait on several descriptors and wake up only when the descriptors change state. The BSD 4.4 implementation has a limitation that causes all processes blocked in a `select()` to wake up. It appears that Linux does not have this limitation.

This approach could easily support hundreds of connections without interfering with each other. The balance between the number of tasks and the number of connection helps minimize the impact on the process table. However, having so many connections can lead to problems if you need to track your protocol's state.

You can use this algorithm easily with stateless servers. A stateless connection remembers nothing about previous transactions. This requires all transactions sent to your server to have no relationship with other transactions or each connection to have a single transaction. Also, if your server requires short- to medium-term connections, you can use this approach. Some examples are an HTTP server, a DB query server, and a Web redirector.