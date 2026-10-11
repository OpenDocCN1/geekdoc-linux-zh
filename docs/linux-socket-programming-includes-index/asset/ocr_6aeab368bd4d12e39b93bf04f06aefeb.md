connections need no more than a reconnection. If, however, yours is a critical server, you have to authenticate. **Authentication** verifies the client has the right to connect. This can happen through a login prompt, a common form of security.

The other form establishes and verifies that the client is really who it claims to be (*certification*). The certification process requires a trusted third party-server (a *certifier*). When the server accepts a connection and begins the login process, the server asks the client for a certificate of authenticity. The server then forwards the certificate to the third party certifier. The certifier checks the certificate and responds with the authenticity.

You must consider these general issues and others you may have before implementation. If you consider security and session protocols after implementation, you create unpluggable holes in your design.

# ## Session Recovery Techniques

Part of the security system includes session recovery. Because you may have critical data, you must consider ways of securing the data. The previous section introduces a couple of ideas to solve this problem.

Part of the process of auto recovery is minimizing user interaction. You also need to consider the issues discussed previously. The previous section provides some hints as to methods to help you recover a session.

The first problem is simply the connection. Even though your server notices the connection loss first, it cannot initiate the connection if the protocol foundation is TCP. Instead, the client must connect to the server. If you want to use the TCP protocol, your client must be intelligent enough to detect a connection dropout and re-establish it.

**Back-Handshaking**

Getting the client to realize that the connection has dropped out can be more difficult because it takes time for network errors to arise. You could *back-handshake*— connect in both directions. Normally, the client connects to the server. In back-handshaking, the server connects back to the client. You can use the backwards channel to send procedural messages back (such as reconnect). You can use a reliable UDP instead of TCP for this back channel.

The connection process can include forcing the recovering client to reauthenticate or reverify automatically or re-log in. This is a necessary step to recover a secure session. If your user is still using the application when it re-establishes the session, you could recall the previous