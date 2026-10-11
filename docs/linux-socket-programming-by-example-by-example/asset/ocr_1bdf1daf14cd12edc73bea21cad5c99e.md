+   1. The peer responds appropriately to indicate that all is well. No indication is returned to the application, because this is the application’s assumption to begin with.
+   2. The peer can respond indicating that it knows nothing about the connection. This indicates that the peer has been rebooted since the last communication with that host. The error ECONNRESET will then be returned to the application with the next socket operation.
+   3. No response is received from the peer. In this case, the kernel might make several more attempts to make contact. TCP will usually give up in approximately 11 minutes if no response is solicited. The error ETIMEDOUT is returned with the next socket operation when this happens. Other errors such as EHOSTUNREACH can be returned if the network is unable to reach the host any longer, for example (this can happen because of bad routing tables or router failures).

The time frames involved for SO_KEEPALIVE limit its general usefulness. The probe message is sent only after approximately two hours of inactivity. Then, when no response is elicited, it might take another 11 minutes before the connection returns an error. Nevertheless, this facility does eventually allow idle disconnected sockets to be detected, and then closed by the server. Consequently, servers that support potentially long idle connections should enable this feature.

# Setting the SO_BROADCAST Option

The topic of broadcasting with UDP has not been covered yet. However, it should be easily appreciated that the use of a broadcasting capability could be misused and cause grief on the affected networks. To avoid broadcasting when broadcasting wasn’t intended, the socket is created with the broadcasting feature disabled. If broadcasting is truly intended, then the C programmer is expected to take the trouble to enable this feature for the socket first.

The topic of broadcasting will be covered in Chapter 13, “Broadcasting with UDP.” Consequently, only the option itself will be described here. The SO_BROADCAST option is a Boolean flag option, which is defined, fetched, and set with the int data type. The following example shows how to enable the SO_BROADCAST option:

```
#define TRUE 1
#define FALSE 0

int z; /* Status code */
int s; /* Socket s */
int so_broadcast;
```