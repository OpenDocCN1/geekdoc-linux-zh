# TABLE 13-1 Output from netstat -atun

| COLUMN | DESCRIPTION |
| --- | --- |
| Proto | Protocol, typically TCP or UDP. On some systems, protocols associated with IPv6 communication may be shown as TCP6 and UDP6. |
| Recv-Q | Received communication in the queue, in bytes, usually 0. |
| Send-Q | Transmitted communication in the queue that is not yet acknowledged, in bytes, usually 0. |
| Local Address | Local IP address and port number. See explanation that follows for more information. |
| Foreign Address | Remote IP address and port number. Unless there's an established connection, it's normally set to IPv4 address and port number 0.0.0.0:*, which is listening for connections from any IPv4 address. It may also be set to IPv6 address and port number ::*. See explanation that follows for more information. |
| State | Connection state, normally LISTEN or ESTABLISHED. A network service that is in the LISTEN state has not made a connection. |

> TIP
IPv4 address 0.0.0.0 is known as the default address, a placeholder for any address.

This is a lot of output, indicative of a system that's probably listening for too many connections. The output is described in Table 13-1, with columns listed from left to right. To see the actual column headers, you'll have to pipe the output to the less command pager. Alternatively, if a bastion host is configured on the local system, you'll see a list of such listen connections be seen in a normal output, and you'll see an example of such later in this section.
With Table 13-1 in mind, take another look at the output from netstat -at command shown in Figure 13-2. Take the first couple of lines of output, one at a time:

The first line is a TCP connection associated with port 2208, listening for requests from systems with any IP address (0.0.0.0). An Internet search might send you into a panic, as there are entries that suggest that port is a common backdoor for black-hat hackers. But it is also used by the Hewlett-Packard Linux Imaging and Printing Project, and may be necessary for communication with such printers. In addition, since the local address is set to the loopback address of 127.0.0.1, the system might be listening just to the loopback adapter.

```
tcp 0 127.0.0.1:2208 0.0.0.0:* LISTEN
```