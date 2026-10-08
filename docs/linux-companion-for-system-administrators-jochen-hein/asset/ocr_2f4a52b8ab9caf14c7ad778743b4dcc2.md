consistent and up to date on different computers can be very costly. In such cases, the file can be distributed, for example, by means of NIS (Network Information System; see Chapter 21).

Communication between two computers takes place via these ports. At one end, a program must establish a connection via this port; at the other end, another program must monitor this port and carry out the necessary actions. There are two alternatives:

+   - The server is started (in the background) and listens on the port. Thus, the server is entirely responsible for the complete establishment of the connection.

+   - The server is started by inetd if a request arrives on the corresponding port. The ports to be monitored and the options and programs are configured in the file /etc/inetd.conf. A port cannot be simultaneously monitored with the two alternatives.

Whether an appropriate server is running on the other side of the connection can be determined in tcp applications by establishing a telnet to this port. Thus, for example, the echo service is used to check whether characters can be transmitted in both directions. You may also use telnet to activate application protocols such as smtp (Simple Mail Transfer Protocol) and test the server in this way.

Often, the protocols echo and discard are used for a first test. Listing 14.3 shows an example. On the other hand, these services can also be used for called 'Denial Of Service' attacks. For this reason these services are not available on many systems – and rightly so, because they are not normally needed in the first place.

```
(Linux):$ telnet localhost echo
Trying 127.0.0.1...
Connected to localhost.
Escape character is '^'
This is a test
This is a test
^
telnet> quit
Connection closed.
```

Listing 14.3 telnet as a test tool

If you want an overview of the currently started services on your system, you can use the netstat -a command. This displays all existing connections, together with all ports on which a service is offered.