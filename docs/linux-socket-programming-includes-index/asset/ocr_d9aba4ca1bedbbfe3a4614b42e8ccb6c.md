Every option has a level. Currently, Linux defines four socket levels: SOL\_SOCKET, SOL\_IP, SOL\_IPV6, and SOL\_TCP. Each option has a type: Boolean, integer, or structure. When you set or get an option, you place the option in optval and declare the size of the value in option. When you get an option, the call returns the number of bytes it used through option.

For example, if you want to disable SO\_KEEPALIVE, use the following:

```
```
/**** setsockopt() example: disable keepalive ***/

int value=0; /* FALSE */
if ( setsockopt(sd, SOL\_SOCKET, SO\_KEEPALIVE, &value,
sizeof(value)) != 0 )
perror("setsockopt() failed");
```
```

Likewise, if you want to know the socket type (SO\_TYPE), you can use this example:

```
```
/**** getsockopt() example: socket type ***/

int value;
int val\_size = sizeof(value);
if ( getsockopt(sd, SOL\_SOCKET, SO\_TYPE, &value,
&val\_size) != 0 )
perror("getsockopt() failed");
```
```

The following sections define each of the options you can use.

# ## General Options

The general options apply to all sockets. The level for these options is SOL\_SOCKET.

+   • **SO\_BROADCAST** This option permits your socket to send and receive broadcast messages.
+   The broadcast address sets the active subnet bits (see Chapter 2, "TCP/IP Network Language Fluency") to all ones. Not all networks support broadcasting (ether net and token ring do). Those networks that do support it allow only datagram messages.
+   (Boolean, disabled by default.)

+   • **SO\_DEBUG** This option enables logging of information about all messages sent or received. TCP is the only protocol that supports this feature. To learn how to read this queue, refer to the TCPv2 RFC. (Boolean, disabled by default.)

+   • **SO\_DONTROUTE** In rare circumstances, you may not want your packets routed to get to the destination. An example of this is router configuration packets. This option enables/disables routing. (Boolean, disabled by default.)

+   • **SO\_ERROR** Get and clear any pending socket error. If you do not pick up this error before the next I/O operation, errno gets the error. (Integer, 0 by default, get only.)