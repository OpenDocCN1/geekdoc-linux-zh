# **Messaging Server**

A messaging server is any server on the network that hosts 1 or more NetMail agents. In the cDirectory tree, the *Messaging Server* object represents the physical server where you have installed the NetMail software.

The Messaging Server object is represented as a container with server attributes. It contains 1 or more Agent objects and it defines the messaging server’s properties.

Each Messaging Server object is associated with a Server object.

You can implement your entire messaging system on a single server or you can distribute NetMail services across multiple messaging servers.

In environments with multiple messaging servers, the servers can be configured to work together as a single, integrated messaging system called a *distributed environment*. They can also be configured to operate as independent sub-systems called *standalone environments*.

# **Distributed Messaging Servers**

In a distributed messaging system, multiple messaging servers work together as a single, integrated system.

Distributed messaging servers look for other Messaging Server objects in the Internet Services container. If a Messaging Server object or an alias of that object exists in the Internet Services container, other distributed messaging servers can find and interact with it.