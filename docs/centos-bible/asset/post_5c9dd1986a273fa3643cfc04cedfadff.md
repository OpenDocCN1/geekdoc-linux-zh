
## Part III Administration

The following is an example of what the output might look like:

| Proto | Recv-Q | Send-Q | Local Address | Foreign Address | State | PID/Program Name |
| --- | --- | --- | --- | --- | --- | --- |

The output is organized into columns defined as follows:

- **Proto** — Protocol used by the socket
- **Recv-Q** — The number of bytes not yet copied by the user program attached to this socket
- **Send-Q** — The number of bytes not acknowledged by the host
- **Local Address** — Address and port number of the local end of the socket
- **Foreign Address** — Address and port number of the remote end of the socket
- **State** — Current state of the socket. Table 13-3 provides a list of socket states.
- **PID/Program Name** — Process ID and program name of the process that owns the socket

During a DOS attack, the foreign address is usually the same for each connection. In this case, it is a simple matter of typing the `whois` command, followed by the foreign IP address, to determine who owns the IP address of the machine causing the attack.

During a DDOS attack, the foreign address will likely be different for each connection. In this case, it is impossible to track down all of the offenders because there will likely be thousands of them. The best way to defend yourself is to contact your ISP and see if it can filter the traffic at its border routers.

## Protecting against Intrusion Attacks

Crackers have a wide variety of tools and techniques to assist them in breaking into your computer. Intrusion attacks focus on exploiting weaknesses in your security, so the crackers can take more control of your system (and potentially do more damage) than they could from the outside.

### TABLE 13-3 Socket States

| State | Description |
| --- | --- |
| ESTABLISHED | Socket has an established connection. |
| SYN_SENT | Socket is actively trying to establish a connection. |
| SYN_RECV | Connection request is received from the network. |
| FIN_WAIT1 | Socket is closed and shutting down. |
| FIN_WAIT2 | Socket is waiting for remote end to shut down. |
| TIME_WAIT | Socket is waiting after closing to handle packets still in the network. |
| CLOSED | Socket is not being used. |
| CLOSE_WAIT | The remote end has shut down, waiting for the socket to close. |
| LAST_ACK | The remote end has shut down, and the socket is closed, waiting for acknowledgment. |
| LISTEN | Socket is waiting for an incoming connection. |
| CLOSING | Both sides of the connection are shut down, but not all of your data has been sent. |
| UNKNOWN | The state of the socket is unknown. |

Fortunately, there are many tools and techniques for combating intrusion attacks. This section discusses the most common break-in methods and the tools available to protect your system. Although the examples shown are specific to CentOS systems, the tools and techniques are generally applicable to any other Linux or UNIX-like operating system.

## Evaluating Access to Network Services

CentOS and its UNIX kin provide many network services, and with them many avenues for cracker attacks. You should know these services and how to limit access to them.

What do I mean by a *network service*? Basically, I am referring to a resource or facility that a remote user can request of the server machine, such as a login, file sharing, instant messaging, or other service. Routing e-mail is a network service. So is serving web pages. Your Linux box has the potential to provide thousands of services. Many of them are listed in the /etc/services file. Look at a snippet of that file:

```
# /etc/services:
# service-name port/protocol [aliases ...] [# comment]
chargen 19/tcp ttyst source
chargen 19/udp ttyst source
ftp-data 20/tcp
ftp-data 20/udp
# 21 is registered to ftp, but also used by fso
ftp 21/tcp ftp ftpsp fspd
ftp 21/udp
ssh 22/tcp # SSH Remote Login Protocol
ssh 22/udp # SSH Remote Login Protocol
telnet 23/tcp
telnet 23/udp
# 24 - private mail system
smtp 25/tcp mail
```

After comment lines, you will notice three columns of information. The left column contains the name of each service. The middle column defines the port number and protocol type used for that service. The rightmost field contains an optional alias or list of aliases for the service.

As an example, examine the last entry in the file snippet. It describes the SMTP (Simple Mail Transfer Protocol) service, which is the service used for delivering e-mail over the Internet. The middle column contains the text 25/tcp, which tells us that the SMTP protocol uses port 25 and uses the Transmission Control Protocol (TCP) as its protocol type.

What exactly is a port number? It is a unique number that has been set aside for a particular network service. It allows network connections to be properly routed to the software that handles that service. For example, when an e-mail message is delivered from some other computer to your Linux box, the remote system must first establish a network connection with your system. Your computer receives the connection request, examines it, sees it labeled for port 25, and thus knows that the connection should be handed to the program that handles e-mail (which happens to be sendmail).

I mentioned that SMTP uses the TCP protocol. Some services use UDP, the User Datagram Protocol. All you really need to know about TCP and UDP (for the purpose of this security discussion) is that they provide different ways of packaging the information sent over a network connection. A TCP connection provides error detection and retransmission of lost data. UDP doesn't check to ensure that the data arrived complete and intact; it is meant as a fast way to send non-critical information.

## Disabling Network Services

Although there are hundreds of services (listed in /etc/services) that potentially could be available and subject to attack on your CentOS system, in reality, only a few dozen services are installed, and only a handful of those are on by default. Most network services are started by either the xinetd process or by a start-up script in the /etc/init.d directory.

xinetd is a daemon that listens on a great number of network port numbers. When a connection is made to a particular port number, xinetd automatically starts the appropriate program for that service and hands the connection to it. The xinetd daemon improves on its predecessor, inetd, by offering features that include more flexible access control, more logging settings, and denial-of-service prevention.

The configuration file /etc/xinetd.conf is used to provide default settings for the xinetd server. The directory /etc/xinetd.d contains files telling xinetd what ports to listen on and what programs to start. Each file contains configuration information for a single service, and the file is usually named after the service it configures. For example, to enable the rsync service, edit the rsvc file in the /etc/xinetd.d directory, and look for a section similar to the following:

```
service rsvc
{
    disable = yes
    socket_type = stream
    wait = no
    user = root
    server = /usr/bin/rsync
    server_args = --daemon
    log_on_failure += USERID
}
```

Note that the first line of this example identifies the service as rsvc. This exactly matches the service name listed in the /etc/services file, causing the service to listen on port 873 for TCP and UDP protocols. You can see that the service is off by default (disable = yes). To enable the service, change the line to read like this:

```
disable = no
```

> **NOTE** *The rsvc service is a nice one to turn on if your machine is an FTP server. It allows people to use an rsvc client (which includes a checksum-search algorithm) to download files from your server. With that feature, users can restart a disrupted download without having to start from the beginning.*

Because most services are disabled by default, your computer is only as insecure as you make it. You can double-check that insecure services, such as rlogin and rsh (which are included in the rsh-server package), are also disabled by making sure that disable = yes is set in the /etc/xinetd.d/rlogin and rsh files.

> **TIP** *You can make the remote login service active but disable the use of the /etc/hosts.equiv and .rhosts files, requiring rlogin to always prompt for a password. Rather than disabling the service, locate the server line in the rsh file (server = /usr/sbin/rshd) and add a space followed by -L at the end. Of course, that doesn't change the fact that your password and data will still be sent unencrypted over the network.*
