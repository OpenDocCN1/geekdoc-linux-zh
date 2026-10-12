Cisco ADSL routers, that can exclusively perform routing between your LAN and the Internet or network service provider.

> TIP: Unlike regular dial-up modems, xDSL modems have several different standards that are not all compatible. Before purchasing a xDSL modem, check with your ISP. If your ISP supports xDSL, it can tell you the exact models of xDSL modems you can use to get xDSL service.

# Proxies

Instead of having direct access to the Internet (as you do with routing), you can have indirect access via the computers on your LAN by setting up a *proxy server*. With a proxy server, you don’t have to configure and secure every computer on the LAN for Internet access. When, for example, a client computer tries to access the Internet from a Web browser, the request goes to the proxy server. The proxy server then makes that request to the Internet. Using a proxy server, Internet access is fairly easy to set up and quite secure to use. Red Hat Linux can be configured as a proxy server (as described later in this chapter).

# Using Dial-up Connections to the Internet

Many individuals and even some small businesses that need to connect to the Internet still do so using modems and telephone lines. Your modem connects to a serial port (COM1, COM2, and so on) on your computer and then into a telephone wall jack. Then your computer dials a modem in your Internet service provider or business that has a connection to the Internet.

The two most common protocols for making dial-up connections to the Internet (or other TCP/IP network) are Point-to-Point Protocol (PPP) and Serial Line Internet Protocol (SLIP). Of the two, PPP is more popular and more reliable. SLIP, however, has been around longer. This section describes how to use PPP protocol to connect to the Internet.

# Getting information

To establish a PPP connection, you need to get some information from the administrator of the network that you are connecting to. This is either your Internet service provider (ISP) when you sign up for Internet service or the person who walks around carrying cables, a cellular phone, and a beeper where you work (when a network goes down, these people are in demand!). Here is the kind of information you need to set up your PPP connection:

+   - **PPP or SLIP** — Does the ISP require SLIP or PPP protocols to connect to it? In this book, I describe how to configure PPP.

+   - **Telephone number** — This telephone number gives you access to the modem (or pool of modems) at the ISP. If it is a national ISP, make sure that you get a local telephone number (otherwise, you will rack up long distance fees on top of your ISP fees).

+   - **Account name and password** — This information is used to verify that you have an Internet account with the ISP. This is referred to as an *account name* when you connect