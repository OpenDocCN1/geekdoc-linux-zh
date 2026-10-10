more control of your system (and potentially do more damage) than they could from the out-side.

# TABLE 13-3

# Socket States

State Description
ESTABLISHED Socket has an established connection.
SYN_SENT Socket is actively trying to establish a connection.
SYN_RECV Connection request is received from the network.
FIN_WAIT1 Socket is closed and shutting down.
FIN_WAIT2 Socket is waiting for remote end to shut down.
TIME_WAIT Socket is waiting after closing to handle packets still in the network.
CLOSED Socket is not being used.
CLOSE_WAIT The remote end has shut down, waiting for the socket to close.
LAST_ACK The remote end has shut down, and the socket is closed, waiting for acknowledgment.
LISTEN Socket is waiting for an incoming connection.
CLOSING Both sides of the connection are shut down, but not all of your data has been sent.
UNKNOWN The state of the socket is unknown.

Fortunately, there are many tools and techniques for combating intrusion attacks. This section discusses the most common break-in methods and the tools available to protect your system. Although the examples shown are specific to CentOS systems, the tools and techniques are generally applicable to any other Linux or UNIX-like operating system.

# Evaluating Access to Network Services

CentOS and its UNIX kin provide many network services, and with them many avenues for cracker attacks. You should know these services and how to limit access to them..

What do I mean by a *network service*? Basically, I am referring to a resource or facility that a remote user can request of the server machine, such as a login, file sharing, instant messaging, or other service. Routing e-mail is a network service. So is serving web pages. Your Linux box