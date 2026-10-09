# General Rules About Defining Protocols

When communicating with other computers, your programs need to agree on a procedure of interaction. Two very important actions are "Who talks first?" and "When are we done?" This agreement defines a transaction-protocol.

The client and server use these procedures to ensure that they don't transmit at the same time or blindly wait for each other to transmit first. As you build servers, consider the questions in the following subsections.

# Which Program Talks First?

Most servers talk first. But, high security systems sometimes wait for the client to send the first message. The process you use can have the client identify itself (more than the standard host ID and port). At the same time, you may want a more user-friendly system that provides some identification and protocol listing upon connection.

Another consideration is unneeded interaction. If the server talks first, it usually says the same thing each time it gets a connection. Does the client need to know that? Does the added interaction slow the communication channels a little?

# Which Program Drives the Conversation?

Often, clients drive the interaction with the server. The client connects to the server and sends requests. The server, in turn, processes the requests and issues a reply.

But, you may have to switch roles sometimes. For example, a client requests some database information from your server. After transmitting the data, a different client updates a few fields that the first client requested. If the first client works exclusively from the first data set, it could make the wrong decisions.

In that type of situation, the server should send the unsolicited updates to the client, and the client needs to accept them. Consider how the client interacts with the server and peers interact with each other and notice exceptions and define ways to address them.

# What Level of Certification Do You Need?

To write a highly secure system, it's essential to know to whom the server is talking. In turn, the server must know or certify the user, or minimally the machine.

The certification process can include usernames and passwords. It can also use a trusted certificate issuer for the users'machines. *Chapter 16, "Adding Security to Network Programs and SSL,"* discusses the Secure Socket Layer (SSL) and presents a couple possible solutions to this problem.

On the other hand, you may not need certification, but want some kind of logging instead. How often does a demographic hit your server? Do you need to beef up certain server pieces to meet user needs? How can you unobtrusively get to know your customer?

Each of these questions are important to consider as you program your server. The Web has several examples of how to get demographics and user needs/trends. This information can also offer information about software defects and even system crackers. A simple way is to ask. Some browsers and Web servers use much more elaborate methods.