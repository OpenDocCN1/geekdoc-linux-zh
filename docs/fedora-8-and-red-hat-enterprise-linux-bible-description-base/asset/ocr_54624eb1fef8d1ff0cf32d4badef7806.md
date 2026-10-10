# ## Understanding How the Internet Is Structured

In order to operate, the Internet relies on maintaining a unique set of names and numbers. The names are domain names and hostnames, which enable the computers connected to the Internet to be identified in a hierarchy. The numbers are Internet Protocol (IP) addresses and port numbers, which enable computers to be grouped together into interconnected sets of subnetworks, yet remain uniquely addressable by the Internet.

An Internet service provider (ISP) will give you the information you need to set up a connection to the Internet. You plug that information into the programs used to create that connection, such as scripts to create a PPP connection over telephone lines. See the section “Using Dial-up Connections to the Internet” later in this chapter for descriptions of the information needed from your ISP and the procedures for configuring PPP to connect to the Internet. With a broadband connection (and the default DHCP configuration), you might just be able to plug in your Ethernet card and go.

The following list describes the basic Internet structure in more detail:

+   - **IP addresses** — These are the numbers that uniquely define each computer known to the Internet. Internet authorities assign pools of IP addresses (along with network masks, or netmasks) so that network administrators can assign addresses to each individual computer that they control. An alternative to assigned addresses is to use a reserved set of private IP addresses, so multiple computers in your home or business can share a single public IP address.

> **CROSS-REFERENCE:** See Chapter 15 for a further description of IP addresses.

+   - **Port numbers** — Port numbers provide access points to particular services. Port numbers are like channels on a television. While all ports are inherently the same, many ports are associated with a particular service. A server computer will listen on the network for packets that are addressed to its IP address, along with one or more port numbers. For example, a Web server listens to port 80 to respond to requests for HTTP content. A Web browser will know, by default, to make its request for HTTP service (in other words, a Web page) to port 80 on the server.

> **NOTE:** In reality, you can assign any service to any port you choose. In fact, system administrators sometimes assign services to unusual ports for the express purpose of keeping most outsiders from finding them. If you decide to use a non-standard port for a service, you should try to avoid port numbers that are already assigned for common services, since those ports might end up being scanned by an intruder anyway. A client of your service would have to know to request that port specifically. For example, `http://www.example.com:4863` would request content from port 4863 on the host `www.example.com`.

+   - **Domain names** — On the Internet, computer names are organized in a hierarchy of domain names and host names. If you want to have and maintain your own Internet