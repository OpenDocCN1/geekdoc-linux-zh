A connection is an individual, separate TCP data channel between two applications. As we said, two applications can have more than one connection between them, and we gave the example of a Web browser with multiple connections to a server. Even though the connections are from the same client, they must be kept completely separate. For example, if one is downloading an image file a.gif and the other is downloading a Web page index.htm, the connections aren't kept separate, you'd get a jumble of data on each connection, which would be useless. Figure 10.7 illustrates schematically how the separate connections in Figure 10.6 are handled.

You can think of connections like phone conversations between two offices. You can have lots of different phone conversations between the same two offices, but if you have crossed wires and the conversations get mixed up, the system doesn't work - you can't communicate properly.

![](bbox=[0.06, 0.29, 0.94, 0.85])

Figure 10.7 How port numbers let TCP separate out multiple inputs

In the next module we show how the netstat program lists the connections that are in use and how you can see which ports are used.