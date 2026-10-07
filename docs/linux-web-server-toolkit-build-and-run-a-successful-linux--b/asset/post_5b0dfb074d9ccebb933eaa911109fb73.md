
make: sure the card is recognized by the kernel, set up a few configuration files, and test it. Of course, each of these steps assumes a lot of knowledge about your particular solution.

The recommended choice for Linux support of these technologies is the cards from Sangoma Technologies, Inc. (see http://www.sangoma.com). Providing a full product line of communications devices, these cards are fully compatible with Linux – their driver software comes with the Linux kernel. Sangoma has worked with Linux developers to make updates available and troubleshoot any problems detected using its cards on Linux systems. Models are available for both leased lines and frame relay networks.

The Web site mentioned in the preceding paragraph includes a complete user's manual, WAN Router for Linux Operating System. Sangoma cards for frame relay connections that include onboard CSU/DSU (so you don't have any other hardware to buy) cost less than $750.

This section has provided some concrete information about connecting your modem to the Internet as well as some details on using other connection options. In the next section, I'll fill you in a little more on routing, the process by which your information is passed around the Internet, and others' information reaches you.

## A Few Words About Routing

Routing packets on the Internet can be a lot more complicated than what is covered in this book. Many other issues come into play when you start working with larger networks, more traffic, and other complicating factors.

Your ISP should be able to help you with questions that arise. In general, however, if you just have a Web server and a few computers at your, your routing is very straightforward.

The Linux kernel provides complete routing capabilities for all incoming network traffic. You can use the route command to examine and change the routing tables that determine what the Linux kernel does with the network packets that it receives for other computers.

If you recompile the Linux kernel, you have options such as IP forwarding and IP firewalling that provide additional options. These options are described in the main pages and other system documentation. Using the Linux firewall features is also described in Chapter 18.

If you have very heavy server traffic or a large network of users in your organization accessing the Internet, the routing load on your Linux system might start to interfere with the efficient operation of your Web server. In this situation, you should consider adding a separate system as a router for your network.

Adding a router is a simple task. The router becomes the key machine between your internal network and the Internet, just as your Web server acts now. Your router can be another Linux machine dedicated to routing or a specialized router

## Chapter 7: Connecting to the Internet

from a company like Cisco Systems. These specialized routers provide very high-speed routing for busy networks but cost several thousand dollars. They are “black boxes” that must be administered via a custom terminal connection.

Beyond IP routing, which Linux is very good at, you can set up your Linux server as a Domain Name Server. The next section provides an overview of the task and points you to additional resources.

## Setting Up a Domain Name Server

Once you have a Web server connected, all the services you need to establish beyond your Web httpd server is the ability to use Domain Name Services to resolve domain names into IP addresses.

I mentioned earlier that you can use a hosts file to list important sites, such as your ISP’s address, and how you can list your ISP’s server as your name server. While those things are both good ideas, if you are providing a gateway to an entire network or want a little more autonomy from your ISP, you can set up a complete name server on your Linux system. The name server runs at the same time as your Web server.

## Understanding the Resolver

All the programs on your Linux system use a feature of the networking code called the Resolver to look up IP addresses when they are handed a domain name. The Resolver is what you configure when you entered your domain name and the IP address of your name server during installation. Those facts are stored in the file /etc/resol.conf.

Another file, /etc/hosts.conf, determines how the Resolver uses the /etc/hosts file and how it protects your programs against security problems. The /etc/hosts file indicates whether to use the name server (referred to bind) or the /etc/hosts file as a first place to look for name resolution. It also indicates whether to reverse loops to protect against spoofed (faked) domains.

The options in your /etc/hosts.conf and /etc/resol.conf files by the installation program are probably sufficient. These files are used mostly by client software such as a Web browser rather than the Web server. If you want to learn more about these files, you can use the command man hosts.conf or man resolv.conf.

In the following sample hosts.conf file, comment lines start with #. Several other options are available, but this example is what you’re most likely to see in:

```
# Lookup names via the Name Server first, then try the hosts file
order bind hosts
# Check for correct IP to name matches to avoid spoofing
nospoof on
```

## Using the Name Server

Setting up a name server that can be used by Resolvers on your system and other systems is a very complex task. In fact, it's much more complex than anything you'll read about when configuring your Web server. The problem is the arcane syntax of the configuration files. I'll provide some basic information and recommend that you read a lot of sample configuration files and the pages for the name server program, named (pronounced name-dee) and the named.boot file.

The named daemon starts by reading the file /etc/named/named.boot, which defines the domains that the name server should worry about responding to, where more configuration files are located, whether to cache resolution information, and other options.

Other configuration files (you can name whatever you like) contain lines called records that define each of the hosts that the name server knows about, with the correct IP address for each one. Records also define things like aliases and to forward mail that's sent to a particular address.

The process is straightforward. Problems with setting up a name server are usually caused by syntax errors in the records. You can use the dig or nslookup commands from any command line to review what the name server is doing, or run the named daemon with the -d option to have notices written in /var/log/messages file.

## Summary

This chapter showed you how to select a type of Internet service Provider, how to identify the right Internet Service Provider, and how to install your Linux system with the connectivity to the Internet that fits your needs.

In this chapter you've learned the following:

- You connect to the Internet using one of many technologies, including a standard modem, ISDN, frame relay, and leased lines. These can run at various speeds. The connection you choose depends on balancing your need for fast access with the cost of your connection.
- An Internet Service Provider (ISP) is the key link between you and the Internet. ISPs offer a variety of services, including Web hosting, consulting, script programming, and page design. As the Internet is seen as a money-making opportunity, people with a variety of skill levels set themselves up as ISPs. Evaluating potential ISPs carefully can save a great deal of time and money in the long run.
- Setting up your Linux server to connect to the Internet (your ISP) using a modem and PPP is simple using a few commands outlined in this chapter. The connection can even be automated. Other connections, such as frame relay or ISDN, may require some additional configuration help from your ISP or a consultant.
- Linux makes a great IP router and Domain Name Server. Setting up a basic router of Name Server is a relatively simple process, but debugging any problems can be challenging.

In the next chapter I'll discuss running your Web site from day to day, and you'll learn how to bring people to your Web site and then keep them coming back. You'll read about many great methods of advertising your site and even several that you should never use.
