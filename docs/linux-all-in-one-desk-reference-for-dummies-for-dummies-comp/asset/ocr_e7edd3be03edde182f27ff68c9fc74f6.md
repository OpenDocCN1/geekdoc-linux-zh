# # Chapter 1: Managing Internet Services

# ## In This Chapter

+   - Understanding Internet services
+   - Controlling servers through inetd or xinetd
+   - Using chkconfig or update-rc.d to manage servers
+   - Using GUI utilities to configure services to start at boot time

The Internet is a world of clients and servers. Clients make requests to servers, and servers respond to the requests. For example, your Web browser is a client that downloads information from Web servers and displays it to you. Of course, the clients and servers are computer programs that run on a wide variety of computers. A Linux system is an ideal system to run a wide variety of servers — from a Web server to a Windows file and print server. In this chapter, I provide an overview of a typical Internet service, its client/server architecture, and how to manage the servers in Linux. You can use the information in this chapter to manage any server running on your Linux system.

# ## Understanding Internet Services

Internet services are network applications designed to deliver information from one system to another. By design, each Internet service is implemented in two parts — a server that provides information and one or more clients that request information.

Such a client/server architecture is the most common way to build distributed information systems. The clients and servers are computer programs that run on these computers and communicate through the network. The neat part is that you can run a client at your desktop computer and access information from a server running on a computer anywhere in the world (as long as it’s on the Internet).