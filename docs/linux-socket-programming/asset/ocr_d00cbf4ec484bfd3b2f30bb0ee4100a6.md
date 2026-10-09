![](bbox=[0.16, 0.05, 0.8, 0.23])

The $\ast$*Socket*$\ast$ component is connected with all other components, as expected. The classes may not all have these connections, but that is not important. Drilling down shows you more of the detail and which class really uses what.

# **Mining Natural Inheritances**

The second step looks in the components and tries to see special relationships called *inheritance*. As described in **Chapter 11**, inheritance lets you create a related class from some other class (base class) and only change a few features (specialization) without rewriting the whole class. This is the primary power of object technology.

The only component that has any interesting classes is $\ast$*Socket*$\ast$. It has five classes that are clearly related. See **Figure 13.3**. The $\ast$*Broadcast*$\ast$ and $\ast$*MessageGroup*$\ast$ (multicast) classes use UDP sockets and have similar functionality, so they must derive from $\ast$*Datagram*$\ast$. However, while $\ast$*SocketClient*$\ast$ and $\ast$*SocketServer*$\ast$ use TCP, they don't operate the same. The client actively connects while the server waits for the connections.

**Figure 13.3. The $\ast$*Datagram*$\ast$, $\ast$*MessageGroup*$\ast$, and $\ast$*Broadcast*$\ast$ classes appear to be related. The $\ast$*SocketServer*$\ast$ and $\ast$*SocketClient*$\ast$ are not close enough.**

![](bbox=[0.1, 0.58, 0.85, 0.68])

The $\ast$*Exception*$\ast$ and $\ast$*Message*$\ast$ components could have many classes and several levels of inheritance. As implemented, however, the hierarchies are very simple. (Please note that in UML, the arrows point to the parent class.)

# **Identifying Abstractions**

Going back to the Socket hierarchy, the classes do fit together, but it requires some additional classes. Clearly, the $\ast$*Socket*$\ast$ class must be the superclass, the mother of all sockets. It does not really have any function other than to provide a common set of features for all child classes.

The $\ast$*Socket*$\ast$ superclass provides all the get and set functions. It also includes the creation, send, receive, and close functions. But, it cannot honestly exist in real time and space. The reason is that it has no protocol. The protocol is defined elsewhere.