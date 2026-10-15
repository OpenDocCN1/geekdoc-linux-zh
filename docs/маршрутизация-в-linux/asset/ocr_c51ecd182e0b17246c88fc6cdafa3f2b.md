# The Digital Subscriber Line Access Multiplexer (DSLAM)

The DSLAM multiplexes the signals from the various DSL subscribers onto the provider's network. Current generation of DSLAMs provide an Asynchronous Transfer Mode (ATM) interface to the service provider's network. Early implementations were typically frame relay interfaces (covered later). Some DSL proponents expect IP to become the interface of choice in next generation DSLAMs, but market reality and current deployments will likely encourage vendors to provide multiple interfaces and let the service provider choose.

# Data Networking with Routers

Until the push of broadband technology in the last several years, the router was the most common hardware used to connect remote sites requiring multiple user support. Routers are known for their Layer 3 routing capability and multiple physical interface support.

This book covers routing with Linux in detail. However, much of the following covers interfaces that can be purchased for both Linux and hardware-based routers.

One of the major advantages of hardware routers over host-based solutions, such as Linux, is their simplicity and dedicated operating system. With a generic operating system, one of the other services can affect the routing functionality. For example the kernel might mistakenly have an unneeded, buggy, IPX stack compiled with the kernel. In addition, there is also the tendency to activate additional services because "the box can do it."

In addition many hardware routers, like Linux routers, provide security functionality such as packet filtering, network address translation, and additional networking functions such as acting as a frame relay access device in a frame relay network. On the high end, core routers also can process many more packets than a PC motherboard...the router's back plane is optimized to route packets quickly.

In addition, hardware routers will typically support a wider range of network interfaces, as was covered earlier.

For these reasons, interaction with routers is likely in most environments...at a minimum the Internet access router provided by the ISP is likely to be a hardware router. Therefore we'll cover some of the more likely facilities used in enterprise networks.

# T1 and E1

As covered in the modem section, the T1 is the 1.54Mbps digital facility that is the standard for voice networks. Its proven technology confirmed its effectiveness in customer premises and has become the standard for narrowband digital communications only likely to be offset by the current broadband technologies. HDSL is the natural replacement and is being marketed as the T1 replacement for business connectivity in some markets.