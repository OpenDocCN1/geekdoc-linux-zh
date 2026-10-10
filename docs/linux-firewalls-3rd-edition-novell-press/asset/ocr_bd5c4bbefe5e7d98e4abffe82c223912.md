```
> netstat -a -P -A inet
```

+   1.  **Active** Internet connections (servers and established)

+   2.  Proto  **Recv-Q**  **Send-Q**  Local  Address  Foreign  Address  State  PID/Program  name

+   3.  tcp 0 143  internal:ssh netservcr:62360  **ESTABLISHED**

+   4.  tcp 0 0 \*:smtp \*:∗ LISTEN

+   5.  tcp 0 0 my.host.domain:www \*:∗ LISTEN  638/httpd

+   6.  tcp 0 0 internal:domain \*:∗ LISTEN  588/named

+   7.  tcp 0 0 localhost:domain \*:∗ LISTEN  588/named

+   8.  tcp 0 0 \*:pop-3 \*:∗ LISTEN  574/xinetd

+   9.  udp 0 0 \*:domain \*:∗

+   10. udp 0 0 internal:domain \*:∗ 588/named

+   11. udp 0 0 localhost:domain \*:∗ 588/named

Line 1 identifies the listing as including local servers and active Internet connections. This selection was indicated with the `-A` **inet** option to **netstat**.

Line 2 contains these column headings:

+   - **Proto** refers to the transport protocol the service runs over, TCP or UDP.

+   - **Recv-Q** is the number of bytes received from the remote host but not yet delivered to the local program.

+   - **Send-Q** is the number of bytes sent from the local program that haven't been acknowledged by the remote host yet.

+   - **Local Address** is the local socket, network interface, and service port pair.

+   - **Foreign Address** is the remote socket, remote network interface, and service port pair.

+   - **State** is the local socket's connection state for sockets using the TCP protocol, either **ESTABLISHED** connection or **LISTEN**ing for a connection request, as well as a number of intermediate connection establishment and shutdown states.

+   - **PID/Program name** is the process ID (PID) and program name that owns the local socket.

Line 3 shows that an SSH connection is established over the internal LAN network interface from a machine known as **netserver**. The **netstat** command was typed from this connection.