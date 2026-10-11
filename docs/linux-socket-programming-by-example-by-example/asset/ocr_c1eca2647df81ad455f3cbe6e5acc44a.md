# Nameless Sockets

Sockets do not always need to have an address. The socketpair(2) function, for example, creates two sockets that are connected to each other, but without addresses. They are, in essence, “nameless” sockets. Imagine a red telephone between the U.S. president’s office and the Soviet Union, during the Cold War. There is no need for a telephone number at either end, because they are directly connected. In the same way, the sockets created by socketpair(2) are directly connected and have no need for addresses.

# Anonymous Calls

Sometimes in practice, one of the two sockets in a connection will have no address. For a remote socket to be contacted, it must have an address to identify it. However, the local socket that is “placing the call” can be anonymous. The connection that becomes established has one remote socket with an address and another socket without an address.

# Generating Addresses

Sometimes you don’t care what your local address is, but you need one to communicate. This is particularly true of programs that need to connect to a service, like a RDBMS database server. Their local address is only required for the duration of the communication. Allocating fixed addresses could be done, but this increases network administration work. Consequently, address generation is often used when it is available.

# Understanding Domains

When the BSD socket interface was being conceived by the Berkeley team, the TCP/IP protocol was still undergoing development. At the same time, there were a number of other competing protocols being used by different organizations like the X.25 protocol. Still other protocols were being researched.

The socketpair(2) function that you have seen in the last chapter, and the socket(2) function, which has yet to be introduced, wisesly allowed for the possibility that other protocols might be used instead of TCP/IP. The domain argument of the socketpair(2) function allows for this contingency. For ease of discussion, let’s restate the function synopsis for the following socketpair(2) function:

```
#include <sys/types.h>
#include <sys/socket.h>

int socketpair(int domain, int type, int protocol, int sv[2]);
```