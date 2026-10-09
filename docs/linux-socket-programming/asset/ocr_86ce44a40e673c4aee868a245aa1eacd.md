Alternatively, some compilers may even be "smart" and note the destination before calling the function. As the function populates the vector, it's really revising the actual destination.

The parameters themselves are a particular problem. Most programmers do not designate which parameters are input only, output only, or input/output. But, because the interface has to determine which parameters to send and which to fill, you need to indicate that in the interface somehow. Often the documentation is the interface. Consider the following example:

```
```c
/***** Network interface example      ****/
/*--------------------------------------*/
                    ***PUBLICATION NOTES***
/* getuserinfo - get the finger information from a host    */
/*  user - (input) user's login id                         */
/*  host - (input) the external host name                  */
/*  data - (output) the results of the call                */
/* RETURN VALUE: success or failure (check errno)          */
int getuserinfo(char* user, char* host, userinfo_t *data); ```
```

This example is more typical. You organize the parameters in the following order: input only, input/output, and output only. Each parameter is passed by reference, and the call assumes that the user reads the publication notes.

# Holding Connected Sessions

The communication between client and server at a service-call level assumes seamless channels. You don't want your user to log in more than once or even be aware that the client program makes multiple connections. This is part of the concept of holding network sessions.

The simplest form of a service call is *stateless*, requiring no more from the server than to do some tasks. But if you want to create a session, you have to do additional work on both the client and server sides.

The network session includes implicit guarantees that most people understand and expect. Chapter 5 introduces some of these guarantees. In RPC service calls, you have to deploy them.

# Establishing a Dialog

The first step in providing the Session layer's functionality is determining the communication order and keeping it. Most RPC connections require some form of authentication, but the client drives the communication.

The initial connection between the client and your server usually requires a login process. The client must provide some level of verification (like username and password). For security, you must ensure that this interchange is secured through some form of encryption, because anyone on the same subnet can see the messages between client and server. After logging in, the client and server establish which communicates first.

Sometimes losing a message can confuse the connection. Both the client and server end up waiting for each other. As noted in Chapter 5 and described in Chapter 10, "Designing Robust Linux