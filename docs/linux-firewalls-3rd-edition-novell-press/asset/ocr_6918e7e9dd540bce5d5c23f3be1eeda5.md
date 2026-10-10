The server allocates a new socket on its end, (*web server IP address, 80*) and associates it with the client socket.

# **FIGURE 1.6**
A TCP client connection request.

![](bbox=[0.1, 0.22, 0.9, 0.45])

The web server responds with an acknowledgment (*ACK*) to the *SYN* message, along with its own synchronization request (*SYN*), as shown in Figure 1.7. The connection is now half open.

# **FIGURE 1.7**
A TCP server connection request acknowledgment.

![](bbox=[0.1, 0.64, 0.9, 0.95])