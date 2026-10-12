+   - **Save on modems** — Instead of each computer having its own modem, you can have one high-speed modem (such as a DSL modem) that routes all messages to the Internet.

+   - **Save on telephone lines** — Instead of using a telephone line for each person who wants to get to the Internet, you can use one line to your ISP. (In the case of DSL, the telephone company will even let you use the same telephone line for both analog voice and high-speed digital data.)

+   - **Central maintenance** — If information related to your Internet connection changes (such as your dial-out number or name server addresses), you can administer those changes in one location instead of having to change it on every computer.

+   - **Central security** — You can better control the Internet traffic that comes in and goes out of your network.

The procedures in this section assume that you have already set up a LAN, as described in Chapter 15. It is also assumed that you have an outgoing connection from your Red Hat Linux system to the Internet that all traffic between the computers on your LAN and the Internet can pass through. That outgoing connection may be dial-up or may come through another LAN card connected (to a DSL modem) or other LAN. This section describes two ways to set up the Red Hat Linux computer so clients on the LAN can access the Internet:

+   - **As a router** — By configuring Red Hat Linux as a router, it can route IP packets from clients on the LAN to the Internet through the dial-up connection.

+   - **As a proxy server** — You can configure Red Hat Linux as a proxy server. In this way, client computers on your LAN can access the Internet as though the connection were coming from the Linux computer.

# ## Setting up Red Hat Linux as a Router

There are several different ways to set up routing from your LAN to the Internet. You can have a dedicated router or you can have a computer already connected to your LAN that will act as a router. This section describes how to use your Red Hat Linux computer as a router.

A computer may have several network interfaces, such as a loopback, an Ethernet LAN, a direct line to another computer, or a dial-up interface. For a client computer to use a router to reach the Internet, it may have private IP addresses assigned to computers on the LAN, while the connection to a routing computer would act as the gateway to all other addresses.

Here’s an example of Red Hat Linux being used as a router between a LAN and the Internet:

+   - The Red Hat Linux system has at least two network interfaces: one to the office LAN and one to the Internet. The interface to the Internet may be a dial-up PPP connection or a higher-speed DSL or cable modem connection.