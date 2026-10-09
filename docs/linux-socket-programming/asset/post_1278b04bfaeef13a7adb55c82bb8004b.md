
**Sockets.** You can keep track of whose turn it is to talk. The easiest method is to periodically send a message indicating each other's state using the OOB data protocols.

# Checkpointing

Some service-directed connections can have critical transactions. The transactions cannot permit data loss (for example, bank transactions). After the client and server have established a dialog, you might want to periodically force a checkpoint.

Checkpointing is like the `commit` command in some databases. During the session, you may have several transactions. These transactions change the server's state (such as transferring funds or paying bills). Both the client and server keep track of the transactions and the expected results. The checkpoint is like checking the balance after several transfers.

You may experience another twist in checkpointing. Clients sometimes have to log the transactions locally to a file for auditing. If this is the case, you might want to encrypt each transaction.

# Recoverable Connections

A session requires a single connection that apparently remains open at all times. That requirement may not always be possible; the network can drop a connection at any time. Also, the Socket API does not directly tell you when it has lost a connection.

Having a recoverable connection means that you not only attempt to reconnect, but it also means that your program must determine the *liveness* of the connection (the channel is clear and active). Chapter 10 describes a few ways to check for connection liveness.

Recovering a connection is easy if you have designed the requirement into your program. Part of the problem with losing a session is trying to keep track of where you were. Somewhat like using a bookmark, you need to mark the place where you left off. Both the client and server must support the bookmark, or *Session ID*. Without the Session ID, you may find that recovering the connection becomes very difficult if not impossible.

After your program finds that the connection was dropped, it can simply reconnect to the server. Doing it with the minimal amount of user interaction is part of seamless connections.

# Seamless Connections

The target here is to provide the user an easy-to-use interface with the minimum amount of user awareness. In contrast, some applications have an *in-your-face* approach that requires the user to re-enter passwords or to establish the network connection manually.

You need to provide the user only as much interaction with the network as he desires. This may mean that you keep track of login information during a defined session. For example, if you define a session to be the duration of your client-program's execution, you could watch all the user logins, remembering them for future use.

However, you must be fully aware of security issues. Keeping passwords in a file for automatic login is often an unnecessary security risk. (It is surprising that some professional applications offer this feature—by default!) Likewise, you may want to drop the connection and forget the login information after a certain time period of inactivity. In the extreme, if the connection must be ultra-secure, you may want to force a login upon each reconnection. Use your best judgment and consult with your end users.

# Supplying Middleware Methods

You can write a set of service calls that interface with a server. The service calls provide a passive (or active) interface between the network, hiding the implementation of the network connection. More often than not, the interface, or *middleware*, is passive, doing no computation—only copying and translating information from one place to another.

Middleware is an important process for modern products. Most applications interface with it from various levels and requirements. Making your middleware components very robust is critical.

The first step in creating good, solid middleware service calls is to define the interface for longevity. You cannot expect to write an interface for others to use that you intend to revise within six months. The short-term interface for a foundational technology like networking is likely to be unpopular.

You can create long-lasting interfaces—critical for all serious projects—by identifying the *brainchild* (a set of goals, intents, philosophies, and theories) for the services. After you have solidified your brainchild, you can work on the network stubs.

# Stubbing Network Calls

If you are writing a passive interface, the interface between your client program and the network support functions only needs to be a set of simple procedure calls. These procedure calls implement different parts of the brainchild. The procedures can also be routines that do more than repackage the parameters.

The `getphino()` and `getuserinfo()` examples, discussed earlier, are examples of interfaces that do nothing more than retrieve data. These calls could easily be part of a security desk brainchild; when the security officer needs to identify someone by face and credentials, he or she uses a tool that retrieves and displays that information.

The network stubs identify what the caller expects and what the server needs to fulfill the request. The interface must be simple as well; the more information your user-developer has to provide, the more difficult it becomes to use.

# Adding the Service Call Implementation

After your client-side service call accepts the request, the call has to package up data and ship it to the server. The server, in turn, implements the server-side service calls that accept and unpack the data and request. This is the heart of middleware.

# Defining Client-Side Services

Client-side services often are based on on-demand processing; the network interaction is only active during the request. The *service requestor*'s basic needs are destination, request, and data. Most requests are transactional, so the middleware does not have to support any more than packaging and shipping the information. The service call module is inactive between requests. UDP fits this case well because a single message passes between client and server.

You may find occasions that require an open connection—a conversation instead of a simple request. TCP fits better in this circumstance. In fact, the client-side services' role changes slightly because the channel has to be held open, and you may have the potential of holding more than one conversation with more than one server. Along with the basic needs of an on-demand connection, your module must keep track of the session and connection. Network modules that support this level of connectivity usually add two more interfaces, an open- and close-session service call.

## Answering with Server-Side Services

The server-side services act in the same way as the client-side. Just as you can create network modules for the client-side program, you can write network modules for the server. Servers usually do much more than serve up data. However, the similarities between client and server network service modules abruptly end there.

The first big issue you face as you begin to write the server's *service provider* is the potential that several requests will arrive at the same time. You could accept and process each one sequentially (remember that the kernel enqueues all messages until the `recv()` system call reads it). However, you cannot be sure how long the request may have to wait in the queue. That can be a very long time.

Multitasking the server reduces the delays from a transactional system. Linux runs more efficiently when the programs are multitasked (using threads and processes). Each new request creates a task to serve it. The organization differs little from the program hierarchy that Chapter 6, "*A Server Primer*" demonstrates.

- 1. The client program calls the client-side network module.
- 2. The client-side network module (service requestor) packages the request and data and ships them through the network. It waits for a reply.
- 3. The server-side network module (service provider) accepts the request and passes it to the server program.
- 4. The server program (request processor) processes the request and returns the results.
- 5. The server-side network module accepts the results, packages it, and pushes it through the network.
- 6. The client-side network module accepts the results message, unpackages it, and returns it to the client program.
- 7. The client program accepts the results.

You may note that the hierarchical placement of the network services module differs between the client side and the server side. Often, the client-side network module is a leaf (the very bottom) in the program hierarchy. The server program, on the other hand, places the network module at the apex of the hierarchy, after all initialization is done. Writing reusable modules for this upside-down interface can be problematic.

To solve the upside-down interface problem, you can use one of two methods. The first method is to define an external procedure that the server-side module calls. The server program must define that procedure as an entry point into its request processor. The problem with this approach is the inflexibility of using predefined procedure names. As your programs evolve, the interface name can lose its meaning.

Another approach is to offer a registration service. As part of initialization, before the server is up and awaiting connections, the server program could register all of its request processor routines. This is the preferred way to overcome the upside-down interface problem. It ensures the longevity of the interfaces.
