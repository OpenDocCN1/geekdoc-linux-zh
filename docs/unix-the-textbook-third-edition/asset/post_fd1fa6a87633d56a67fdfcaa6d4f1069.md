
```
% grep ^ssh /etc/services
ssh 22/tcp #Secure Shell Login
ssh 22/tcp #Secure Shell Login
ssh 22/udp #Secure Shell Login
sshell 614/tcp #SSLshell
sshell 614/udp
%
```

## 20.10.1.3 Locating inetd Protocols on PC-BSD and Solaris

Another file that inetd reads when it runs is /etc/services. This file is the database of protocol names and contains the name of a protocol, the IANA assigned number for the protocol, and aliases for the protocol. Any protocol that inetd uses for a service must have an entry in the /etc/protocols file. It has one line per protocol in the following format:

```
protocol-name number [aliases]
```

Here, protocol-name is the name of the protocol such as tcp, number is the IANA assigned number for the protocol such as 6 for tcp, and aliases are alternative names for the protocols, such as TCP for tcp. Here is the line for the tcp protocol in the /etc/protocols file:

```
% grep ^tcp /etc/protocols
tcp 6 TCP # transmission control protocol
%
```

## 20.10.1.4 Adding or Deleting inetd Services on PC-BSD

As an administrator, you can delete a service that inetd offers by simply removing the line for the relevant service from the /etc/inetd.conf file. Similarly, you can add a new service in inetd by adding a line for the corresponding service in the /etc/inetd.conf file.

After making the requisite changes in the /etc/inetd.conf file, you can reconfigure inetd dynamically so that it offers the updated set of services without having to terminate and restart it. You can do so by sending SIGHUP (no hang-up signal) to inetd using the kill or killall command. Table 20.25 shows four ways of performing this task. Note that the killall command is used with a process name and the kill with a process ID (PID). Note the use of grave accents (`) for the substitution of the cat /var/run/inetd.pid command, with the resultant execution of the command.

### EXERCISE 20.27

Display the lines for all "internal" services listed in the /etc/inetd.conf file on your system.

TABLE 20.25 Ways of Restarting inetd

|  |  |
|---|---|
| 1 | killall -HUP inetd |
| 2 | killall -1 inetd |
| 3 | kill -HUP `cat /var/run/inetd.pid` |
| 4 | kill -1 `cat /var/run/inetd.pid` |

## EXERCISE 20.28

Display the line in the /etc/protocols file for the UDP protocol. What numerical value is associated with the UDP protocol? How many protocols are defined in this file?

## 20.11 CONCURRENT CLIENTS

It seems obvious to think of concurrent servers to serve multiple clients simultaneously in an efficient manner, thereby reducing the average response time experienced by a client. However, the need for concurrent clients is not so obvious. There are several real-life examples of concurrent clients that are necessitated due to the application protocol. Many of the well-known services require concurrent clients, including SSH, TELNET, FTP, and HTTP. A client for each of these services has to deal with two descriptors: a standard input descriptor (keyboard) to read user input and a socket descriptor used by the client to communicate with the server process. Either descriptor may become ready for I/O asynchronously; a user may type the next command for the client using the keyboard any time that he/she desires to do so and the server response for a previous client request may arrive at the client-side socket at any instant of time, depending on the load on the server process and network traffic.

We explain the need for a concurrent client by using the example of a connection-oriented (TCP) SSH client. A TCP client for SSH expects input from two descriptors, one for the keyboard and the other for the socket that is connected to the SSH server-side socket. The client needs to receive user input (i.e., the next shell command to be executed on the remote host) entered through the keyboard and the server’s response through the connected socket, as shown in Figure 20.32. Since the two descriptors become ready asynchronously, you may implement such concurrent clients by using the select() system call.

Another scenario under which a concurrent client becomes necessary arises because BSD UNIX does not allow independent processes to share main memory. The X Window System allows multiple clients to paint (i.e., redraw) a bitmapmed display, so that the windows of the respective clients may be updated when required. Since the X display is

![](img/02e070097d401d3bf7de4bf1c470b267_990_0.png)
