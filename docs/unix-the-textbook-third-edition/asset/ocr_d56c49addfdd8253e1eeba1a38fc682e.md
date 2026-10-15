```
if (server = gethostname(argv[1]))
    memcpy(&saddr.sin_addr.s_addr, server->h_addr,
           server->h_length);
else
    if ((saddr.sin_addr.s_addr = inet_addr(argv[1])) ==
        INADDR_NONE) {
        printf("No such host\n");
        exit(1);
    }
...
```

```
/* Send connection request to the server process */
if ((connect(s, &saddr, sizeof(saddr))) == -1) {
    perror("connect failed");
    exit(1);
}
```

Note that gethostname() returns a pointer to the hostent structure, which contains relevant information about the host, including its address and address length, as discussed in Section 20.6.6. We copy the address of the host to the relevant field of the address variable for the server-side socket, saddr, using the bcopy() or the newer memcpy() function. The atoi() function received criticism and the newer recommended replacement is strtol(). We use the strtol() function in the client-server software that we design and develop in this chapter. You can also replace

```
saddr.sin_addr.s_addr = inet_addr(argv[1]);
```

with the following call:

```
inet_pton(AF_INET, argv[1], address.sin_addr);
```

# 20.6.10 Accepting a Client Request for Connection

Whether it is used on an iterative server or a concurrent server, the passive socket may only be used to wait for client requests for connections and not for client-server communication. This is so because, after accepting a client's request for connection and before starting communication with the client, the server process needs to go back and listen for more incoming connection requests from clients. Thus, a client-side socket does not communicate with the passive socket on the server side. Instead, a new socket is created on the server side that is connected with the client-side socket for communication between the two processes. Because it is used to interact with the client process, the newly created socket is also known as the active socket. As stated earlier, this new socket on the server side is created and connected to the client-side socket through the rendezvous of the accept() call on the server side and the connect() call on the client side.

The main server socket—the passive socket—remains allocated throughout the life of a server process. However, the sockets created by accept() have the life span of a