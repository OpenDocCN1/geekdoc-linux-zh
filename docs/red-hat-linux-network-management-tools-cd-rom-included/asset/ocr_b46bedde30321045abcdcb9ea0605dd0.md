tion and the command interface. When the user specifies a file transfer or executes a remote command, another session is established to service the request. After the transfer is complete, the newly created session is closed. This process is repeated for each separate transaction.

Sockets are ports that the system allocates on the user’s behalf when executing network applications or other services. Because the operating system generates a unique socket number, no two simultaneously running applications on the same system will have the same socket number. On some UNIX systems, the allocation of sockets begins above 1024.

In the context of a connection, TCP uses four pieces of information to uniquely identify one session from another: source IP address, source port, destination IP address, and destination port. This is important to remember because many sessions to the same application or service can be established, even from the same host. For example, two different users can *telnet* to the same destination host without any conflicts among the ports. This is accomplished by the fact that TCP uses all four addressing elements to distinguish a unique session. Figure 3.5 shows the relationship of the TCP elements in different sessions.

| TCP Connection #1 | **Source Entity** | **Destination Entity** |
| :--- | :--- | :--- |
| | **IP: 10.0.2.1** | **IP: 10.0.2.2** |
| | Source Address: 10.0.2.1 | Destination Address: 10.0.2.2 |
| | TCP Port: 1001 | TCP Port: 23 |

| TCP Connection #2 | **Source Entity** | **Destination Entity** |
| :--- | :--- | :--- |
| | **IP: 10.0.2.1** | **IP: 10.0.2.2** |
| | Source Address: 10.0.2.1 | Destination Address: 10.0.2.2 |
| | TCP Port: 1002 | TCP Port: 23 |

**Figure 3.5 Two TCP sessions from same source/destination.**

# ### Positive Acknowledgment

One way TCP provides reliability is by ensuring that every message transmitted is confirmed by the receiving entity. The confirmation of TCP messages is known as positive acknowledgment and is used to ensure that the receiving entity has obtained all the segments that have been sent. When a TCP message is sent, the sending entity starts a timer. If no acknowledgment is received before the time expires, TCP assumes the message was lost or dam-