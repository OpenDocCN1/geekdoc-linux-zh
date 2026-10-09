# **Example 6.5. Accept() with Connection Logging**

```
```c
/***** Accept Example (revised): Add client-connection   ***/
/***** logging. Compare with Listing 6.4                 ***/
***** (Inside the loop) ****/
...
client = accept(sd, &addr, &size);
if ( client > 0 )
{
    if ( addr.sin_family == AF_INET )
        printf("Connection[%s]: %s:%d\n", /* log connection */
               ctime(time(0)),             /* time-stamp connection */
               ntoh(addr.sin_addr), ntohs(addr.sin_port));
    /****-Interact with client-****/
...  
```
```

If the `accept()` system call yields an error, it returns a negative value to your server. Otherwise, it returns a new socket descriptor. The following are some common errors:

+      * `EBADF` The socket descriptor is not valid (see the description for `bind()` in Chapter 4).
   * `EOPNOTSUPP` The socket must be a `SOCK_STREAM` for this call.
   * `EAGAIN` The socket is set for non-blocking and the listening queue has no pending connections. A call to `accept()` with no one on the queue blocks the task unless the socket is made non-blocking.

The Echo Server simply sends back what it receives until it gets a `bye` message (see Listing 6.6).

# **Example 6.6. Echo Server Example**

```
```c
/**** Echo Service Example: Send back whatever we get   ***/
/**** until "bye<ret>". (Compare with Listing 6.5)        ***/
***** (Inside the loop & after accept()) ****/
...
if ( client > 0 )
{
    char buffer[1024];
    int nbytes;

    do
    {
        nbytes = recv(client, buffer, sizeof(buffer), 0);
        if ( nbytes > 0 )      /* if real data, echo back */
            send(client, buffer, nbytes, 0);
    } while ( nbytes > 0 && strncmp("bye\ r", buffer, 4) != 0 );
    close(client);
}
...  
```
```

Notice that the end condition is looking for a `\"bye\ \ r\"`, not `\"bye\ \ n\"`. Depending on how the input processing works (Telnet does none), the server may get one or the other. For robustness, consider testing both. Try out this program with Telnet as your client. The complete program, named `simple-server.c`, is on the Web site.