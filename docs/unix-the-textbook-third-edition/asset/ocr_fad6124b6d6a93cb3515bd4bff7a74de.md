```
Active Internet connections (including servers)
Proto Recv-Q Send-Q Local Address          Foreign Address        (state)
tcp4   0      0 *.6001                 *.*                    LISTEN
tcp4   0      0 202.147.169.196.ssh    39.59.72.116.60434     ESTABLISHED
tcp4   0      0 *.ssh                  *.*                    LISTEN
[output truncated]
% telnet 202.147.169.196 6001
Trying 202.147.169.196...
Connected to 202.147.169.196.
Escape character is '^]'.
Hello, world!
Hello, world!
Connection closed by foreign host.
% ps
  PID TT  STAT      TIME COMMAND
  8437 1  Ss       0:01.13 -csh (csh)
 33690 1  S        0:00.00 ./tcpechos tcp 6001
 33725 1  R+       0:00.01 ps
% kill -9 33690
%
```

# EXERCISE 20.10

Repeat this session on your UNIX system to verify that it works as expected.

# 20.6.12.2 Design of a Client Process

The client processes that we discuss in this chapter run with three command line arguments, the IP address in DDN or domain name of the server process, the protocol port at which the service is offered, and the transport-level protocol for which the service is offered (tcp, udp, etc.). Thus, the syntax for the execution of a client process is shown next.

```
client-name ip-address (or domain name) protocol-port
                                    transport-protocol
```

If any of the command line arguments is invalid, the program displays an error message and terminates.

The first function that we design for the client software is CreateConnectedSock(), which takes the three arguments that you pass to the client process as command line arguments. It converts the port number from a string to an integer using the strtol() library call and initializes the address variable for the server process. It then creates a TCP or UDP socket, depending on the value of the transport-level protocol. Next, it establishes a connection with the server-side socket using the connect() system call and returns the socket descriptor. As has been discussed earlier, in the case of the UDP client-server software, no connection is established between the client- and