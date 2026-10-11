The basic steps of the server can now be summarized as follows:

+   1. Create a socket.  
+      2. Bind a socket address (mandatory).  
+      3. Listen for a connection.  
+      4. Accept a connection.  
+      5. Communicate with the client program.  
+      6. Close the socket.

Notice that, for the server, the bind(2) step 2 (S2 in Figure 8.1) is not optional. The server cannot be contacted by clients unless the client has an address for connecting. On the other hand, the client bind(2) step C2 is optional. In order for a server to be contacted, then, a server address cannot be completely wild.

Notice also that step 3 (S3 in Figure 8.1) is something new. The server must express its interest in accepting connections to the kernel for its socket. This will be discussed further when the listen(2) function is covered.

The process of accepting a connection in step 4 (S4 in Figure 8.1) is another new socket concept. Once a client has connected to the server, the server must then accept the connection. This will be covered in detail when the accept(2) function is covered later in this chapter.

Briefly, the server differs from the client in the following ways:

+   • The server must bind a server address to the socket.  
+   • The server listens for a connection.  
+   • The server accepts connections.

# ## The listen(2) Function

The listen(2) function is how the server is able to express its interest in listening for connections. The function is very simple to call, and its function prototype is given as follows:

```
```c
#include <sys/socket.h>

int listen(int s, int backlog);
```
```

The two input arguments are the following:

+   • The socket s to use as the listening socket.  
+   • The backlog, which specifies the connect queue length in entries.