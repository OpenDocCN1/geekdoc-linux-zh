But, you may have to switch roles sometimes. For example, a client requests some database information from your server. After transmitting the data, a different client updates a few fields that the first client requested. If the first client works exclusively from the first data set, it could make the wrong decisions.

In that type of situation, the server should send the unsolicited updates to the client, and the client needs to accept them. Consider how the client interacts with the server and peers interact with each other and notice exceptions and define ways to address them.

# ## What Level of Certification Do You Need?

To write a highly secure system, it’s essential to know to whom the server is talking. In turn, the server must know or certify the user, or minimally the machine.

The certification process can include usernames and passwords. It can also use a trusted certificate issuer for the users’ machines. Chapter 16, “Adding Security to Network Programs and SSL,” discusses the Secure Socket Layer (SSL), and presents a couple possible solutions to this problem.

On the other hand, you may not need certification, but want some kind of logging instead. How often does a demographic hit your server? Do you need to beep up certain server pieces to meet user needs? How can you unobtrusively get to know your customer?

Each of these questions are important to consider as you program your server. The Web has several examples of how to get demographics and user needs/trends. This information can also offer information about software defects and even system crackers. A simple way is to ask. Some browsers and Web servers use much more elaborate methods.

# ## What Type of Data Do You Use?

Most servers you interact with use ASCII for correspondence, while most Web pages are text/HTML. It’s a good idea to consider the questions “Is that the most efficient data form to use?” and “Does the client support compressed data?” As you look at your server and your customer’s clients, consider how to decrease the delays on the server, network, and client.

Compressing data can have some real benefits. Compressed ASCII can yield between 50% and 80% reduction in data size. Even compressed data can be ASCII without too much inflation, so the network won’t lose any binary high bits. The following subsections provide more detail on how to handle data.

# ## How Do You Handle Binary Data?

Binary data—especially compressed—is more efficient than ASCII. Problem: some networks only support 7-bit bytes. This is a real problem for 8-bit binary data. These networks are