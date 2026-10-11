
## Sending Simple Messages

  The second major feature is crucial for effective functionality—the framework must be able to send and receive messages. The message has three parts: addresses, the channel, and the message body.

  Earlier chapters describe two methods each for sending and receiving messages. These calls assume certain socket states. For example, you must have a connected socket to use the send() system call. The primary goal for getting and receiving messages includes simplifying these interfaces.

  What would simplify communications is to get the message to ship itself. One of the extended features described in Chapter 11 was data streaming—the automatic packaging and unpackaging of data. The class would know its internals rather well; it should assume that role.

  The C++ language does not lend itself to providing data streaming. It has a significant limitation—it must know the data before it uses it. Compare with Java—Java lets you define a class and attach a Serializable interface. From there, the class packages/unpackages itself automatically. Very easy. We can do this because it uses interpreted byte code. It assumes no machine-specific information.

  A C++ program must provide the packaging and unpackaging procedures. And, because C++ does not support interfaces, you must inherit from a common class that describes those procedures.

## Managing Exceptions

  The third major feature must control the various exceptions and errors that the network introduces to programming. While you create and configure your sockets and while sending and receiving messages, any number of asynchronous errors can occur.

  All errors originate from the socket, the connection, the route, or the other host. Quickly and efficiently collecting the errors helps the user-programmer to isolate the problem and recover appropriately.

  The framework uses the C++ exception management construct try...catch(), similar to that found in Java. The user-programmer must catch all exceptions that the framework throws; otherwise, the program terminates with an uncaught exception error. You can catch all unexpected exceptions at the root of the program and return some meaningful message to improve debugging.

## Configuring the Socket and Connections

  The last major feature is configuring the socket or connection you created. All of the socket types have different settings that allow you to tune them. The different tunable settings change the behavior of the socket or the send and receive channels.

## Grouping into Major Components

  The next step in creating a framework is identifying all of the major pieces or components. *Components* are networks of objects that work together to solve a particular problem or provide a service. Just as with objects, components have responsibilities and interfaces, so you can treat them like objects as well.

  Typically, these components are heterogeneous objects contained in a single interface. Some object analysts call these groups *packages*, due to the method of distribution, or *patterns*, and because the systems of objects often fit in generalized ways. But, they can also be hierarchies with abstract objects as the primary interface.

  This section describes the four basic components of the Socket Framework. Each of these components is a hierarchy as previously described.

### Exceptions: Handling Problems

  All frameworks should identify and use exceptions. The kinds of exceptions that you may want to capture include networking, I/O, boundary, and so on. The exception hierarchy depends on the *Exception* class for basic functionality. Figure 13.1 displays the exception component.

![](img/2591af4bdf00a0f382331fc9481f785e_307_0.png)

*All exception classes derive from Exception, which captures only a string and the error code.*

  An exception class hierarchy infrequently defines any startling or ingenious design. In fact, if you employ a class hierarchy for exceptions, be very careful that you do not create a potential for recursive exceptions. For example, if you allocate memory and have mapped the memory handler to an exception, you could crash the program from one bad *new*() call. Leave the design of exceptions to the simplest form with little more than values and a brief message.

### Messages: Packaging and Shipping the Data

  To send and receive messages through the I/O subsystem, you need blocks of data and buffers. The *Message* virtual class provides the basic interface to package (*Wrap*()) and unpackage (*Unwrap*()) itself. This interface helps approximate the serialization Java's I/O offers.

  Another class, `TextMessage`, supplies an example of how to use this interface. For example, the `wrap()` method creates a block of contiguous memory and copies the text into it. (The responsibility of freeing up the block is left to the caller.) The message of `TextMessage` is a variable-length C-style string.

  The un-packaging method, `Unwrap()`, does the reverse. It takes the block of data from the caller and begins to reassemble the internal information. Sometimes, the message may be incomplete, so `Unwrap()` must get more data to finish the reassembly. For example, the `TextMessage` may be larger than 64KB (the buffer limit), so the `TextMessage` class must be smart enough to ask for more data. The `Unwrap()` method returns a Boolean to indicate whether it’s done.

### Addressing: Identifying the Source and Destination

  Each message comes from and goes to some host. The addressing of these hosts is important for getting the message to the rightful owner. Another simple component is `HostAddress`. Using the struct `sockaddr` addressing names, this component manages the name and resolution to an IP level.

  The framework translates all addresses into this component. And, the component can support several addressing types.

### Sockets: Establishing, Configuring, and Connecting

  The last component has the most functionality. It is based on the `Socket` class and derives all basic connections. It uses the other components to finish the job done. The hierarchy places the basic functionality in the `Socket` class and all specializations in the inherited classes.

  All protocols listed in the requirements list have a dedicated class: `SocketServer`, `SocketClient`, `Datagram`, `Broadcast`, and `MessageGroup` (multicast). All protocol-specific configurations reside in the appropriate protocol-class. When you need to change a setting, look at the protocol you are using. If you do not find it, look in the parent.

  The classes also assume you are following proper rules. From the earlier `send()` example, the classes do not check for a connected socket. Instead, the program throws an exception.

## Creating the Framework Hierarchy

  The components ease the transition into connecting the objects together. The components provide the interface for the outside world and may hint at the features of the top-most parent (*superclass*). Before working on the framework hierarchy, you need to have defined the non-abstract classes within each component.

  At this point, you should have several classes, such as those listed in the last section. From there, you find the relationships and inheritances. Don’t be surprised to see features disappear and reappear from parent to child. This is normal, and often is still implementable.

## Relationships

  The first step is to identify the relationships between the components and the classes. Use general terms, such as uses, is-a, has-a, and throws, to label the connections between component or class.

  In Figure 13.2, the different components are connected to show how they interact with each other. Some diagram systems use special line ends (such as arrows). Use whatever you are most comfortable with. The most important factor is clarity.

![](img/2591af4bdf00a0f382331fc9481f785e_309_0.png)

**FIGURE 13.2**
*Each component uses a resource from the other.*

  The Socket component is connected with all other components, as expected. The classes may not all have these connections, but that is not important. Drilling down shows you more of the detail and which class really uses what.

## Mining Natural Inheritance

  The second step looks in the components and tries to see special relationships called inheritance. As described in Chapter 11, inheritance lets you create a related class from some other class (base class) and only change a few features (specialization) without rewriting the whole class. This is the primary power of object technology.

  The only component that has any interesting classes is Socket. It has five classes that are clearly related. See Figure 13.3. The Broadcast and MessageGroup (multicast) classes use UDP sockets and have similar functionality, so they must derive from Datagram. However, while SocketClient and SocketServer use TCP, they don’t operate the same. The client actively connects while the server waits for the connections.

![](img/2591af4bdf00a0f382331fc9481f785e_309_1.png)

**FIGURE 13.3**
*The Datagram, MessageGroup, and Broadcast classes appear to be related. The SocketServer and SocketClient are not close enough.*
