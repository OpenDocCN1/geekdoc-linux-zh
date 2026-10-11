
# What? More Devices?

We've covered a lot of ground here, but we are by no means finished. Those things we attach to our PCs aren't much good if we don't put them in context with the tools and applications we use them with. Those tools tend to require a somewhat more in-depth examination. For instance, burning CDs isn't just about creating collections of your favorite songs. People use them for back-ups, as well, or to make collections of digital photos for sharing with the family. I'll tell you all about CD burning in Chapter 18. Most CD and DVD burners are automatically recognized under Linux.

The same is true of scanners. These gizmos are incredibly handy devices for the home or office. Aside from converting nondigital pictures to place on your Web site, you can use your scanner as a photocopier and as a way to send faxes when the pages require your signature (you can fax from a word processor, after all). For the most part, your scanning application autodetects your scanner and configures it for you (see Figure 6-13). You'll find XSane under your Graphics submenu.

![](img/0e9cf4c65a042f4a9bea644dc50153a7_154_0.png)

**Figure 6–13** XSane, the image scanning application included with Ubuntu, autodetects and automatically configures many popular scanners.

By the way, XSane is also a great program for sending images in an email, faxing documents, or making photocopies.

To help you in choosing a scanner that is well supported under Linux, check out the SANE (Scanner Access Now Easy) page of supported devices:

http://www.sane-project.org/sane-supported-devices.html

There's also a scanner search engine on that page to make locating your devices that much easier.

# Resources

- Linux Hardware Compatibility HOWTO
  http://www.tldp.org/HOWTO/Hardware-HOWTO/index.html
- Hardware Catalog at Red Hat
  http://bugzilla.redhat.com/hwcert
- Linmodems.org (Winmodems under Linux)
  http://www.linmodem.org
- LinuxPrinting.org (Linux Printer Database)
  http://www.linuxprinting.org
- Linux USB Device Overview
  http://www.qbik.ch/usb/devices/
- SANE Project, Supported Devices
  http://www.sane-project.org/sane-supported-devices.html
- Ubuntu Hardware Support Wiki
  https://wiki.ubuntu.com/HardwareSupport

# Chapter 7

# Connecting to the Internet

I'm going to start this chapter with a little Networking 101. It will be fun—really. For those of you who already know everything about *TCP/IP* and how IP networks operate, you can skip ahead a few paragraphs.

Communication over the Internet takes place using something called the *TCP/IP* protocol suite. *TCP/IP* actually stands for *Transmission Control Protocol/Internet Protocol*, and it is the basic underlying means by which all this magic communication takes place. Everything you do on the Net, whether it is surfing your favorite sites, sending and receiving emails, chatting via some instant messaging client, or listening to an audio broadcast—all these things ride on *TCP/IP*'s virtual back.

*TCP/IP* is often referred to as a *protocol/suite*, a collection of protocols that speak the same language. Essentially, this comes down to the transmission and reception of IP packets. Those packets have to get from place to place, and that means they need to know how to get there. IP packets do this in exactly the same way that you get from your house to someone else's house. They have a home address from which they go to a remote address.

Each and every computer connected to the Internet has a unique address called an *IP address*, four sets of numbers separated by dots (for example, 192.168.22.55). Some systems that are always online (banks, Web sites, companies, and so on) have a *static* address. Dial-up connections for home users tend to be shared — when you aren't connected, someone else may be using the same address — which is referred to as a *dynamic* IP address.

You may be wondering how a symbolic Web site address such as www.marcelagane.com translates to the dotted foursome I mentioned previously, and that would be an excellent question.

Think of the real world again. We don't think of our friends as 136 Mulberry Tree Lane or 1575 Natika Court; we think of them by their names. To find out where our friends live, we check the phone book (or ask them). The same holds true in the digital world, but that phone book is called a *domain name server* (DNS). When I type a symbolic (that is, human readable) address into my Web browser, it contacts a DNS (assigned by my Internet service provider (ISP)) and asks for the IP address. With that IP address, my packets almost know how to get to their destinations.

Almost?

To reach an address in the real world, you get out of your driveway and enter some road to which all other roads are connected. If you drive long enough, presumably you get to Rome (having often been told that *all roads lead to Rome*). Before you can get to Rome, we enter from your default route, namely, the street in front of your house. The same principle exists in the virtual world. For your IP packages (an email to your mother, for instance) to get to its destination, it must take a particular route, called a *default route*. This will be the IP address of a device that knows all the other routes. Your ISP provides that route.

That concludes Networking 101. Not particularly complicated, is it?

# Before You Begin

Connecting to the Internet is one of those things you set up once, then forget about. Still, you need to get some information from your ISP up front. The basics are as follows:

- Your username and password
- The phone number your modem will be dialing to connect (if using a dial-up modem connection)
- The IP address of the DNS (name servers, described earlier)
- The IP or symbolic address of your SMTP and POP3 email hosts
- The IP or symbolic address of your news server (optional)

All of this information likely came with your contract when you first signed up with your ISP. Armed with this information, you are ready to begin.

# Getting on the Net

As I write this, there are three very popular methods of connecting to the Internet, notwithstanding your own connection at the office. These are cable modem, DSL service from the phone company, or good old-fashioned dial-up modem. The first two are usually referred to as high-speed or broadband connections, and dial-up access is usually made fun of because it feels very slow when compared to the higher speed methods.

With all the press and hype about high-speed service, you would think that this is all people run. Think again. As I write this, the vast majority of people in North America, and indeed the world, is still connecting through a dial-up connection. Make no mistake—as Mark Twain might have remarked, the rumors of dial-up access’s demise are greatly exaggerated. You may be among the majority who are still using dial-up; I’ll cover that in detail.

If you are ready, let’s begin.

# Connecting to the Net with a Modem

Most ISPs provide dial-up access through the Point-to-Point Protocol, or PPP. To set up a network connection or pretty much any type, just run the Network Settings program. Click System on the top panel, then Administration, and finally, Networking. You can also use your <Alt+F2> Run Application shortcut and type in network-admin in the dialog box. If you are starting to like the feel of the command line, enter network-admin & in a terminal window. Since this is an administration function, you’ll be asked for your password (see Figure 7-1).

![](img/0e9cf4c65a042f4a9bea644dc50153a7_160_0.png)

**Figure 7–1** Administrative functions like this require that you enter your password.

> **Tip** You may have noticed in the preceding paragraph that I added an ampersand (`&`) to the end of the network-admin command. When you start a command from a shell prompt, it normally runs in the foreground. This means you can’t start another process at the shell until the current one finishes (you could, of course, open up another shell). The ampersand tells the shell to put the process in the background so that you can run other commands.

When the Network Settings tool comes up for the first time, it lists, at minimum, a modem connection that is currently not configured (see Figure 7–2). Even if you don’t have a modem built in to your machine, an option for configuring one is still available. In your list of connections, you may also see an Ethernet connection. Most modern machines usually have an Ethernet card built in, so this is likely. We’ll use my test machine as an example, which, as you can see, has both a network card and a dial-up modem attached.

Before you jump in and configure your modem connection, look at the drop-down box labeled Location near the top of this window. The idea here is that you can have multiple dial-up (or network) accounts. Most people probably use just one, but you can also use it to set up multiple profiles of the same account. If you happen to be a road warrior or globe trotter with a notebook, you can create location profiles for the various cities you visit.
