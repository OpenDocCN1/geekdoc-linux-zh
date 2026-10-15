
![](img/02e070097d401d3bf7de4bf1c470b267_972_0.png)

## FIGURE 20.21 System call sequences and interaction sequences for the general iterative connection-oriented client-server model.

the model implements the well-known ECHO service. If the user input is "daytime", the model implements the DAYTIME service. If the user input is "quit", the client and server processes disconnect gracefully. The service is offered at an arbitrary port.

## EXERCISE 20.20

Write the code for the iterative connection-oriented client–server model for the ECHO service. Compile and run the implementation on your UNIX system to verify that it works as expected.

## EXERCISE 20.21

Run the client and server processes in different windows on the same machine and on different machines on the Internet.

## 20.8.5 Concurrent Connectionless Client–Server Model

In this model, the client and server processes communicate using the connectionless style of communication based on the UDP protocol. The master server process waits for a request from a client process, creates a slave process, hands over the client request and socket to the slave process, and goes back to receive another client request. The slave process forms a response according to the application protocol, sends it to the client process, and exits. Figures 20.22 and 20.23 show the algorithms, system call graphs, and interaction

## Server process

## Master process

- 1. Create a socket for SOCK_STREAM style of communication
- 2. Bind an address to the socket using the bind() system call
- 3. Put the socket in passive mode using the listen() system call
- 4. Receive a connection request from a client using the accept() system call and create a slave process using the fork() system call to handle the request.
- 5. Go to Step 4

## Slave process

- 1. Receive the socket that was created by the accept() system call and is connected to the client-side socket
- 2. Receive a request from the client using the read() system call
- 3. If the received request is some kind of 'quit', then go to Step 5
- 4. Prepare a response according to the application protocol, send it to the client using the write() system call, and go to Step 2
- 5. Close the active socket created by the accept() system call, disconnect with the client process gracefully, and exit

FIGURE 20.24 Algorithm for the concurrent connection-oriented server process.

![](img/02e070097d401d3bf7de4bf1c470b267_974_0.png)

FIGURE 20.25 System call graphs and interaction sequences for the concurrent connection-oriented client-server model using slave processes.

Figures 20.24 and 20.25 show the algorithms, system call graphs, and interaction sequences for this client-server model. Note that the algorithm for the client process is the same as for an iterative connectionless server as discussed in Sections 20.6.12 and 20.8.1.

Figure 20.26 shows the pictorial view of the concurrent connection-oriented client-server model with k clients being handled by k slave processes and the master process waiting to accept a connection request from another client process.

![](img/02e070097d401d3bf7de4bf1c470b267_975_0.png)

## FIGURE 20.26 Connection-oriented concurrent server.

Here is the source code for the concurrent connection-oriented server software based on slave processes for the DAYTIME service. We have replaced the call to the TCPdaytime() function in the while() loop to a piece of code for creating a child (slave) process that closes the passive socket and calls the TCPdaytime() function to handle the client request. The parent process closes the active socket and goes back to accept the next connection from a client process.

```
% cat daytime_concurrent_server_TCP.c
#include <stdio.h>
#include <time.h>
#include <sys/types.h>
#include <sys/socket.h>
#include <netinet/in.h>

#define BUFF 256
#define PORT 6001
#define QLEN 5

int main(int argc, char *argv[])
{
    int asock, psock, pid, caddrlen;
    struct sockaddr_in caddr;

    /* Exit if program is not run with two command line arguments. */
    if (argc != 3) {
    printf("Usage: server protocol port\n");
    exit(1);
```
