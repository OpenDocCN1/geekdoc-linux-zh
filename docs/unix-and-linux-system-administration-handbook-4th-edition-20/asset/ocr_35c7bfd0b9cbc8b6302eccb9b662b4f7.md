# Monitoring the status of network connections

With arguments, **netstat** displays the status of active TCP and UDP ports. In-listening") servers that are waiting for connections are normally hidden, but you can see them with **netstat -a**. The output looks like this:

| Proto | Recv-Q | Send-Q | Local Address | ForeignAddress | State |
|---|---|---|---|---|---|
| tcp | 0 | 0 | *: | * | LISTEN |
| tcp | 0 | 0 | *:mysql | * | LISTEN |
| tcp | 0 | 0 | *:imaps | dhcp-32hw:4208 | ESTABLISHED |
| tcp | 0 | 0 | *:ssh | nubark:54195 | ESTABLISHED |
| tcp | 0 | 0 | *:http | dhcp-30hw:2563 | ESTABLISHED |
| tcp | 0 | 0 | *:imaps | dhcp-18hw:2851 | ESTABLISHED |
| tcp | 0 | 0 | *:http | * | LISTEN |
| tcp | 0 | 0 | *:37203 | baikal:mysql | ESTABLISHED |
| tcp | 0 | 0 | *:ssh | * | LISTEN |

This example is from the host otter, and it has been proven; for example, UDP and UNIX connections are not displayed. The output above shows inbound SSH connection, two inbound IMAPS connections, one inbound HTTP connection, outbound MySQL connection, and a bunch of ports listing for other connections.

Addresses are shown as *hostname.service*, where the *service* is a port number. For well-known services, **netstat** shows the port symbolically, using the mapping defined in /etc/services. You can obtain numeric addresses and ports with the **-n** option to **netstat**. Like most network tools, **netstat** is painful to use without the **-n** flag if your DNS is broken.

Send-Q and Recv-Q show the sizes of the local host's send and receive queues for the connection; the queue sizes on the other end of a TCP connection might be different. These numbers should tend toward 0 and at least not be nonzero. (Of course, if you are running **netstat** over a network terminal, the queue for your connection may never be 0).

The connection state has meaning only for TCP; UDP is a connectionless protocol. The most common states you'll see are ESTABLISHED for currently active connections, LISTEN for servers waiting for connections (not normally shown without **-a**), and, TIME_WAIT for connections in the process of closing.

**netstat -a** is primarily useful for debugging higher-level protocols once you have determined that basic networking facilities are working correctly. It verifies you that servers are set up correctly and facilitates the diagnosis of certain types of miscommunication, particularly with TCP. For example, a connection that stays

+   4. Connections for "UNIX domain sockets" are also shown, but since they aren't related to networking, we do not discuss them here.