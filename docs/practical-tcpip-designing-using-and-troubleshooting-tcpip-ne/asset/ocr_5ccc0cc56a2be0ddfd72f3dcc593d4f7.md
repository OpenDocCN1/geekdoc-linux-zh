# ### 14.4 The different versions of HTTP

For basic troubleshooting of an HTTP problem, the conversation we illustrated in the previous module is often all you need. What we were using is the very early version of HTTP – version 0.9 from 1991. The next version was HTTP/1.0 (May 1996), which formalized and enhanced the protocol. HTTP/1.1 (January 1997) developed it even further, and resolved some problems with how the HTTP/1.0 was being interpreted and implemented. (To indicate how the complexity has increased, it's interesting to compare the size of the specifications of the various versions. The spec for 0.9 is two pages long in its original format (see Notes). RFC-1945, specifying HTTP/1.0, has 60 pages, and RFC-2616, specifying HTTP/1.1, has 176 pages.)

Fortunately, the only differences that we need to consider here are:

+   - in HTTP/0.9 the server has no way to tell the client the type of data that are being returned. The client just receives a lump of data and has to guess what format they're in and how best to handle them – by looking at the content or the name of the page. Most transfers on the Web are pages containing HTML so in practice this system worked quite well, but for more sophisticated data types – word processor files, different image types, etc. – it is inadequate. HTTP/1.0 overcomes this problem by using exactly the same mechanism that e-mail does – MIME. In HTTP/1.0 and 1.1, the server sends the client details of the format and type of the data, before sending the actual data (Module 14.8)

+   - in HTTP/0.9 the server has no way to tell the client if there is a problem with the page that the client requested (e.g. if it doesn't exist). The only thing the server can do is return an HTML page containing a human-readable error message (Figure 14.5). HTTP/1.0 and 1.1 overcome this by sending a status response to each request (Module 14.6).

+   - HTTP/1.1 allows a single instance of a Web server to handle multiple site names (e.g. **www.alice.com**, **www.bob.com**, **www.carol.com**, **www.dave.com** on a single IP address. Earlier HTTP versions had to use a separate IP address for each site name (Module 14.6)

+   - HTTP/0.9 and 1.0 initiate a new TCP connection for every download. For example, if a page contains five GIF images, six TCP connections are used – one for the page itself and five for the images. HTTP/1.1 uses *persistent connections* to allow multiple downloads over a single TCP connection in a single session (Module 14.9).

In the next module we look at HTTP/1.0 and HTTP/1.1. We'll see how clients use headers to give more information about the data requested and servers use headers to inform the client about what data will be sent back.