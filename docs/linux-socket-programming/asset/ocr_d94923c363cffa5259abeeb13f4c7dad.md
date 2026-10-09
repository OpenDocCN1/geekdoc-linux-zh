# **Supplying Middleware Methods**

You can write a set of service calls that interface with a server. The service calls provide a passive (or active) interface between the network, hiding the implementation of the network connection. More often than not, the interface, or *middleware*, is passive, doing no computation—only copying and translating information from one place to another.

Middleware is an important process for modern products. Most applications interface with it from various levels and requirements. Making your middleware components very robust is critical.

The first step in creating good, solid middleware service calls is to define the interface for longevity. You cannot expect to write an interface for others to use that you intend to revise within six months. The short-term interface for a foundational technology like networking is likely to be unpopular.

You can create long-lasting interfaces—critical for all serious projects—by identifying the *brainchild* (a set of goals, intents, philosophies, and theories) for the services. After you have solidified your brainchild, you can work on the network stubs.

# **Stubbing Network Calls**

If you are writing a passive interface, the interface between your client program and the network support functions only needs to be a set of simple procedure calls. These procedure calls implement different parts of the brainchild. The procedures can also be routines that do more than repackage the parameters.

The getphino() and *getuserinfo*() examples, discussed earlier, are examples of interfaces that do nothing more than retrieve data. These calls could easily be part of a security desk brainchild; when the security officer needs to identify someone by face and credentials, he or she uses a tool that retrieves and displays that information.

The network stubs identify what the caller expects and what the server needs to fulfill the request. The interface must be simple as well; the more information your user-developer has to provide, the more difficult it becomes to use.

# **Adding the Service Call Implementation**

After your client-side service call accepts the request, the call has to package up data and ship it to the server. The server, in turn, implements the server-side service calls that accept and unpack the data and request. This is the heart of middleware.

# **Defining Client-Side Services**

Client-side services often are based on on-demand processing; the network interaction is only active during the request. The *service requestor*'s basic needs are destination, request, and data. Most requests are transactional, so the middleware does not have to support any more than packaging and shipping the information. The service call module is inactive between requests. UDP fits this case well because a single message passes between client and server.

You may find occasions that require an open connection—a conversation instead of a simple request. TCP fits better in this circumstance. In fact, the client-side services'role changes slightly because the channel has to be held open, and you may have the potential of holding more than one