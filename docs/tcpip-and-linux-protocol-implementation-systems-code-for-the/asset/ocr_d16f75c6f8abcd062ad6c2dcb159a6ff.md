# 7.3.4 Transport Layer Linkage

This section describes the functions that link the transport layer to the socket layer above and the the network layer below.

# Socket to Transport Layer

A socket's life is one of create, operate on, and close. This section describes how the user space calls are passed through to kernel functions. We will use the example of socket creation to show this.

Socket state information is maintained in a number of structures:

+   - struct socket, which is a protocol-independent structure.

+   - struct sock, which contains transport layer information. In most of the functions, the current socket's sock structure is called sk.

The main socket code is in net/socket.c. Functions in this file are coded to call functions specific to the type of socket created.

When a socket is created (socket call) there is a call to sys_socket. This calls sock_create and maps the socket to a file descriptor. This descriptor is passed back to the user process for future operations on the socket. socket_create allocates the socket and calls the create function for the family of sockets being created (in the case of an IP network socket PF_INET).

Here reference is made to the net_families array, so we now need to travel to the initialization code for the Linux networking in order to see how this and other structures are initialized.

The net_families array is initialized when the kernel is booted in the inet_init function in ipv4/af_inet.c. This function is part of the code run at boot-up as being the start of the function. One of the first operations in inet_init is to register the inet family of sockets with the socket functionality. Then the protocols are added to a hash table of protocols. These functions are in protocol.c.

The inet family is registered with the sock_register call, which is a function in socket.c that stores the family operations structure. This structure contains the family name and a create function for the socket family—inet_create.

The create function for PF_INET sockets is inet_create, which is the function called as net_families[family]->create in socket_create. inet_create allocates and initializes the sock structure. Important part of the initialization is the assignment of the socket operations to the ops field. The two main types of IP socket (SOCK_STREAM and SOCK_DGRAM) each have a set of functions associated with their operations. These are inet_stream.ops and inet.dgram.ops ops, which are statically initialized in ipv4/af_inet.c.

A further important structure to be initialized is the prot structure that contains specific functions for each protocol type. udp_prot and tcp_prot are static