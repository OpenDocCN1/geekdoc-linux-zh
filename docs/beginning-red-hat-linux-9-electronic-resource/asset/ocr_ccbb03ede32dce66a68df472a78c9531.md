+   - The stability and reliability of the operating system is also influential, because an unstable or unreliable system brings maintenance costs. Linux is a good choice for network applications because it makes the grade in these areas. Moreover, Linux is ready for high-availability environments (see http://www.ibiiblio.org/pub/Linux/ALPHA/linux-ha).
+   - Other factors influencing TCO include the scalability, flexibility, and security of the system:
+     - By choosing a Linux operating system and open source networking applications, you have access to the source code of both the system and the application. This puts you in a position to adapt the applications to achieve whatever aims you need.
+     - We've already seen evidence, earlier in this chapter, that Linux is capable of being deployed in both small- and large-scale networks.
+     - Red Hat Linux installs by default with a minimum of good-practice security, and (as we'll see in Chapter 12) be further enhanced with a combination of open source security tools and good practice.

Linux is also great for services that can be replicated (for example, DNS). You can configure such machines cheaply, and replicate them. Then, if one machine fails, it doesn't matter; it should be possible to replace it cheaply. In the meantime, the replicate servers keep on working to provide the service.

By contrast, Linux is not a common choice for basic infrastructure, such as routers, hubs, and switches. While Linux is capable in this area, it's desirable only when the low cost of cheap (or cast off) PCs is the major selection criteria. In a more business critical role, where reliability will count for more than minimum purchase price, dedicated hardware is still the most popular choice.

You can find more information about TCO comparison between Red Hat Linux and other Unix flavors at http://www.redhat.com/whitepapers/services/tco.pdf.

# # Assumptions for Network Setup

In the demonstrations in this chapter, we've used a network setup that may not be the same as your own environment. You can choose your own server, connectivity devices (switch, hub, and direct cable connection), IP address scheme, and hostname to set up networking in a way that suits your own requirements. In this section, we'll note the network settings that we've used. In order to facilitate, we'll begin with an explanation of the terms that we'll use.

The network topology refers to the shape or layout of the network. It defines how different systems in a network are connected and communicate with each other. The ideal topology of a network depends on the size of the network, the requirements of its users, and the policies of the company or organization.

The following diagram shows an ideal network topology: