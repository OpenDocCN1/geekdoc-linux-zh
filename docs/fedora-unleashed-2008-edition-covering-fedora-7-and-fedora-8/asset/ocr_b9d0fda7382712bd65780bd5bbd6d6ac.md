# ## CHAPTER 14
## Networking

# IN THIS CHAPTER

+   > - Using Network Configuration Tools
+   > - Laying the Foundation: The localhost Interface
+   > - Networking with TCP/IP
+   > - Advanced Wireless Networking
+   > - Dynamic Host Configuration Protocol
+   > - Beyond the Network and Onto the Internet
+   > - Configuring Dialup Internet Access
+   > - Troubleshooting Connection Problems
+   > - Reference

One of the benefits of open source technology in general and Linux in particular is that it is now mature enough to be used effortlessly across several different networking environments as well as the Internet. With strong support for the standard Internet protocol TCP/IP, Linux can also talk to all the UNIX flavors, as well as Mac OS X, Windows (with the help of Samba), NetWare (IPX), and even older protocols such as DECnet and Banyan Vines. Many organizations use Linux as an Internet gateway, allowing many different clients to access the Internet through Linux, as well as communicate via email and instant messaging. This chapter covers network and Internet connectivity because most networks invariably end up connected to the Internet by one means or another. You will learn about how to get the basics right, including configuration and management of network interface cards (NICs) and other network services with Fedora. You will also find out how to manage network services from the command line—again an important lesson in case you are ever confined to a command prompt. We also look at connectivity options, both for inbound and outbound network traffic and the importance of PPP (Point-to-Point Protocol). Also included is an overview of graphical management clients for Fedora, which are becoming more and more popular.

# ### Using Network Configuration Tools

If you add or replace networking hardware after your initial installation, you must configure the new hardware. You can use either the command line or the graphical configuration tools to do so. To configure a network client host using the command line, you can use a combination of