# The basics

# Networking models

In this article, we cover a lot of ground, from physical media to packets to MAC addresses and routed IP networks. If it seems difficult to understand how this all fits together, imagine how difficult it is to make the systems that enable all this to work. It's very complicated, and there are many components that all have to work together if your network connection is going to work the way it should.

To make networking software and hardware that works together easier to create, some clever people came together and created the Open Systems Interconnection model. The OSI specifies seven layers, each of which describes a set of related functions that are critical if the network is to work as expected. Each separate layer depends on the one below it to provide certain services, but it doesn't need to know how any of the other layers are implemented, just how to interact with the lower layers. This means they can be created and tested separately, and you can have many different implementations of the different functions (for example, fibre optic or Ethernet for the physical layer), without having to rewrite any other components.

In this article, we've covered the first three layers of the OSI model:

+   > **The physical layer** This specifies how electrical signals can be transmitted across particular physical media.
+   > **The data link layer** This specifies how hosts

are physically identified on the network – that is, with MAC addresses.

**The network layer** Specifies how packets are routed between networks and how logical addresses are assigned.

The remaining four layers concern managing reliable connections between machines, and the presentation and utilisation of transmitted data at the application level. Networking topics that you might be familiar with that fall into these layers include: the TCP and UDP protocols in layer 4; file encoding such as UTF, ASCII, JPG and so on that are all found in layer 6; and things such as the HTTP (web), FTP (file transfer) and SMTP (mail transfer) protocols, which are all network applications in layer 7.

network. To see these packets, install the tcpdump package using whichever package manager your Linux distribution provides. Once it's installed, launch a terminal and first find out which device is currently providing your network connection. Assuming you've got only one active network connection on your computer, you can find this out by typing: `ip a | grep "state UP"`

The `ip` command is used for showing information about your network connections – we'll cover this in more detail a little later – while the grep command filters the result to see only those network connections which are 'up' or active. The bit of information you're interested in is near the beginning of the line, and probably reads eth0, wlan0 or em1, depending on your configuration.

With this information, you can now run tcpdump to watch a network conversation take place. As root, run:

`tcpdump -i wlan0`

where wlan0 is the device you discovered above. Then, open a web browser and visit a site. When you switch back to the terminal, you'll see the screen filling up with lines of text. Each line represents a packet that was sent between your computer and the web server in order to load the page, and each provides bits of information about it, including the time it was sent or received, which computers (or hosts) it was sent from and to, and much more.

By passing the -w switch and a filename, you can save this output and the contents of the packets (not just the header information shown in the terminal) for later analysis by a graphical tool, such as Wireshark (see p102).

This can be a very useful tool for diagnosing network problems. For instance, if you can't get DHCP working properly, running a packet dump on the DHCP server will enable you to see whether it's receiving requests for

addresses, whether it's responding, or whether packets are being blocked by a firewall, which will enable you to identify where the problem lies.

# MAC addresses

Now you know how many computers can share a single physical network, you might be wondering how computers can identify each other on the network – that is, how can you send information only to Bob's computer, not Alice's?

In fact, the answer is that when computers are connected by the same bit of physical medium – for example, a copper cable – they see every packet sent to every other computer.

> Nmap is a command line tool for scanning your network. Here, we've used Zenmap to interpret the results of a scan to display the topology of the network.

![](bbox=[0.35, 0.68, 0.92, 0.92])