different types of networks. However, virtually no one goes by this definition anymore, so we are not going to, either. Instead, we will use the commonly accepted definition throughout this chapter, and the terms default router and gateway will be used interchangeably.

One of the most common uses of a gateway is to allow multiple hosts to share a single Internet connection.

# # What Is NAT?

NAT, which stands for Network Address Translation, is a way for multiple hosts to connect to the Internet using a single IP address. The magic involved in how this works is beyond the scope of this book, but basically NAT works by having a NAT gateway attached to the network in question. When the internal hosts want to send or receive Internet content, their request goes through the NAT gateway. The NAT gateway “hides” the internal IP address and sends all requests from the hosts connected to it out on the Internet with a single IP address (which is the IP address owned by the NAT gateway). Responses that are sent back are sent to that single IP address (which is owned by the NAT gateway). The NAT gateway then routes the data to the proper internal host, which does not need to have a registered IP address. There are two primary advantages of this method:

+   • It conserves IP addresses. The IP address pool is a limited resource, and there is no reason to waste IP addresses where they are not needed. NAT prevents you from having to register an IP address for each one of your systems. The only system that needs a public and registered IP address is the NAT system. The rest of them can all have private, internal IP addresses.

+   • If you are a home or small office user, it allows you to share a single Internet connection with multiple computers, and you won’t have to purchase additional accounts from your ISP. You can also share a single modem and a single phone line, preventing you from having to install additional phone lines if more than one computer will use the Internet at the same time.

To illustrate some of the ways you can configure various types of routing services on FreeBSD, this chapter presents a few sample scenarios. We begin by looking at sharing a single modem and Internet connection at home or in a small office.

# # Configuring a NAT Gateway in FreeBSD

In this scenario, you will generally have a single Internet connection, which may or may not be over a modem. You have several systems that need to access the Internet. Figure 27.3 shows an example.