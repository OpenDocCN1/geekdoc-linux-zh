# Chapter 15

# Setting Up an Internet
Connection

This chapter demonstrates how to connect CentOS to any TCP/IP-based network, such as the Internet, a private LAN, or a company WAN. The differences in how you connect have more to do with the network medium you use (i.e., telephone lines, LAN router, etc.) than they do with whether you are connecting to the public Internet or a company’s private network.

Connections to the Internet described in this chapter include a simple dial-up connection from your own Linux system. The most popular protocol for making dial-up connections to the Internet is the Point-to-Point Protocol (PPP). It also builds on the procedures in Chapter 14 for creating your own local area network (LAN) by teaching you how to connect your LAN to the Internet.

This chapter first provides an overview of the structure of the Internet, including descriptions of domains, routing, and proxy services. It then discusses how to connect your Linux system to the Internet using PPP dial-up connections. For those who want to connect a LAN to the Internet, it describes how to use Linux as a router and set it up to do IP masquerading to protect your private LAN addresses. Finally, it describes how to configure Linux as a proxy server, including how to configure client applications such as Firefox.

# IN THIS CHAPTER

+     
+     * Understanding how the Internet is structured
+     * Using dial-up connections to the Internet
+     * Connecting your LAN to the Internet
+     * Setting up Linux as a router
+     * Configuring a virtual private network
+     * Setting up Linux as a proxy server
+     * Setting up proxy clients

# Understanding How the Internet
Is Structured

In order to operate, the Internet relies on maintaining a unique set of names and numbers. The names are domain names and hostnames, which enable the computers connected to the Internet to be identified