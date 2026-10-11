# Understanding the Role of accept(2)

It might seem strange for accept(2) to return yet another socket. After all, wouldn't it be better to use the original socket? The answer lies in the nature of most server designs. A server, upon accepting one client connection, must be willing to accept additional connections from clients. Any individual socket, however, can only be connected to one client. Where would the www.woohoo.com server be if it could only service one client at one time?

Figure 8.1, which was presented earlier, has an oversimplification of server responsibilities. Figure 8.3 is an improvement, showing the steps that a simple server would use.

![](bbox=[0.22, 0.33, 0.82, 0.872])

**Figure 8.3**: *Here is an improved diagram explaining the connection steps for client and server (note the repetition of steps S4 to S6).*