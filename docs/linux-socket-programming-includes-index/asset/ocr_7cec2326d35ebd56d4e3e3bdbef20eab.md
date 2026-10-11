# Relationships

The first step is to identify the relationships between the components and the classes. Use general terms, such as uses, is-a, has-a, and throws, to label the connections between component or class.

In Figure 13.2, the different components are connected to show how they interact with each other. Some diagram systems use special line ends (such as arrows). Use whatever you are most comfortable with. The most important factor is clarity.

![](bbox=[0.38, 0.28, 0.72, 0.4])

**FIGURE 13.2**
*Each component uses a resource from the other.*

The Socket component is connected with all other components, as expected. The classes may not all have these connections, but that is not important. Drilling down shows you more of the detail and which class really uses what.

# Mining Natural Inheritance

The second step looks in the components and tries to see special relationships called inheritance. As described in Chapter 11, inheritance lets you create a related class from some other class (base class) and only change a few features (specialization) without rewriting the whole class. This is the primary power of object technology.

The only component that has any interesting classes is Socket. It has five classes that are clearly related. See Figure 13.3. The Broadcast and MessageGroup (multicast) classes use UDP sockets and have similar functionality, so they must derive from Datagram. However, while SocketClient and SocketServer use TCP, they don’t operate the same. The client actively connects while the server waits for the connections.

![](bbox=[0.29, 0.74, 0.81, 0.89])

**FIGURE 13.3**
*The Datagram, MessageGroup, and Broadcast classes appear to be related. The SocketServer and SocketClient are not close enough.*