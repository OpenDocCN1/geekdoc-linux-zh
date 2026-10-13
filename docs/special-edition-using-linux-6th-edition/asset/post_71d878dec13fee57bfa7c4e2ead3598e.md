
## ABOUT NETWORKING

Probably one of the most exciting moments for new Linux users is when their first network is successfully implemented. Linux, as illustrated elsewhere in this book, works great as a desktop system, but to limit it to desktop use is like purchasing a Ferrari just to drive back and forth to the grocery store. Linux is a fantastic operating system for networking; you are cheating yourself if you do not at least try networking with it—even between only two machines—just to see what it is like.

One of the fastest growing uses of Linux seems to be in home networking. It is common to find more than one computer in a home, so this is somewhat understandable. The classic SneakerNet, in which data was transferred by copying it to a disk and carrying the disk to another machine, is no longer acceptable to most people with multiple computers, and it is a waste of resources. Resources such as printers, disk drives, and even Internet access can be shared across a network, and the cost of setting it all up is rather low. (An average low-end Ethernet card for a PC can cost around $25, and the cabling that connects the machines is even less expensive—you will learn about hardware shortly.)

However, the principles and concepts of setting up a small network are not unique to home use; you can take these instructions into your office and use them to set up a network server there. Furthermore, with the way that Linux is licensed, you can take your CD-ROM in and use it to set up all the other machines on the network as well without incurring any extra costs or per-seat restrictions. It is a win-win situation for everyone involved.

> **Note:** If you purchase the boxed Caldera or Red Hat Linux versions, they include some commercial software that is licensed for use on only one system; you must purchase a separate license for each system you want to use the software on for these commercial programs.

### HARDWARE

Network hardware covers quite a range of possible network connections. Some items cover networking over frame relay through the same cable that gives you television services, digital subscriber lines (DSL), or even satellite dishes. Router boxes and firewall boxes. Today, embedded Web server machines exist, some of which even run Linux. Watchdog boxes monitor your network and make sure that the server is rebooted if it appears to have crashed. Computer serial devices set up dial-in connections through the use of modems. As many different types of networking hardware devices exist as there are types of networks, and the list continues to grow.

Despite the many different types of hardware that are available for networks, for the sake of simplicity only the three most basic, most essential kinds are discussed here: network cards, cabling, and hubs.

### NETWORK CARDS

Naturally, each computer that is going to be networked must have its own network card. Of the many different kinds of network cards, the ones most commonly used are of the Ethernet variety. The quality of these cards run the gamut from $25 NE2000 clones all the way up to major name-brand offerings that can transfer data one hundred times as fast as the low-end clones, and then some. Find out what others who have networks either at home or at work recommend.

Unless you are doing serious data transfers over your network, you will be just fine with the low-end NE2000 clones. These come in a few different varieties, the most common being 10Base-T, 10Base-2, and 10Base-T/2. As indicated by the classification of the card, it is capable of transferring ten megabits of information at any given time. The T, 2, and T/2 at the end of the classification indicate the cabling that is required by the card.

### CABLING

Computers with network cards are pretty much useless unless they are connected with network cables. 10Base-T cards use what is known as Cat 5 (category 5) twisted-pair cabling. This kind of cabling has what look like telephone plugs at each end; because it does not normally permit direct card-to-card connections between computers, it is typically used in conjunction with a hub (hubs are discussed a bit later). A special kind of twisted pair cable called a reverse pair or cross-connect cable permits direct connections, though, and is commonly used to connect one hub to another or one computer directly to another computer. The use of a hub is much more common. Networks that use these cards tend to be arranged in a star topology around a central location at which the hub resides (see Figure 30.1).

**Figure 30.1**  
A 10Base-T network scheme.

![](img/c741b1b6b6eccaba2ad43454c979a7f8_584_0.png)

10Base-2 cards use coaxial cables similar to those used with cable TV. Instead of having what look like phone plugs at the ends, these cables have what are called terminators—little metal devices that terminate the line by looping the wiring back into the cable. The cables themselves are connected to the network cards with small tees. Networks that use these types of cables tend to be strung together in one long line, with each computer joining the connection at the tee in the back of the network card (see Figure 30.2).

![](img/c741b1b6b6eccaba2ad43454c979a7f8_585_0.png)

The drawback to using this kind of cabling with 10Base-2 cards is that for each cable coming into the computer's room from the previous system, another cable must go out of the room for the next system. The benefit to using twisted-pair cabling with 10Base-T cards is that only one cable is needed to connect the computer in the room.

What about 10Base-T/2 cards? They simply have jacks on the back that can handle both types of cables and generally autosense which one is to be used.

### HUBS

Hubs are small boxes that can accommodate a number of different network cable connections, but they are primarily used to connect computers containing 10Base-T cards. Among their benefits, they can act as the central connection point for all systems on a network, or they can help to split the network connections into more easily manageable chunks. For instance, if multiple rooms have multiple computers in each, it makes more sense to take one cable into each room and give each its own hub than it does to have multiple cables coming out of each room going to a central hub.

Hubs can also act as traffic cops by helping monitor network traffic for packet collisions.

A typical 4- or 8-port hub can cost anywhere from $40 to more than $100, depending on the brand and the features. Again, unless you are planning on passing around bandwidth-intensive network traffic, stay inexpensive. Buying features can be fun, but if you never really use the features you are wasting your money.

> **Caution**
>
> Hardware is available for 100MB and 1000MB networking if you are interested. Be careful about mixing bandwidths if you are using a hub, though; if you have 10Base-T or 10Base-2 (or 10Base-T/2) cards, do not purchase a 100Mb hub to connect them. Mixing bandwidths in this manner does not work without special, expensive switching hubs. If you plan on eventually moving to a 1000 network, it might be cheaper in the long run for you to simply go 100MB right from the start.

### ASSUMPTIONS

The following sample network consists of five computers: four PCs running various operating systems (including Windows NT and Linux) and one Mac. All are connected using 10Base-T/2 Ethernet cards through a small 10Base-T hub with twisted-pair cabling (see Table 30.1).

**Table 30.1 — Assumptions for Your Sample Network**

| Computer Name | IP Address | Type | O/S Used |
|---|---|---|---|
| rumble.fish.net | 192.168.1.1 | PC | Linux |
| geoffie.fish.net | 192.168.1.2 | PC | Windows 95 |
| go.fish.net | 192.168.1.3 | PC | Windows NT |
| silver.fish.net | 192.168.1.4 | Apple | System 7.5 |
| tuna.fish.net | 192.168.1.5 | PC | Linux |

*fish.net is being used as an example only. If your network is going to be connected to the Internet, please register your own domain and do not use fish.net. Of course, if fish.net is not taken...*

All systems are connected using TCP/IP, plus various other protocols that allow the connection of networked drives. For the sake of brevity, only the TCP/IP setup is addressed here. Also for the sake of brevity, it is assumed that the names of the Linux systems were assigned when the systems were installed. For the Windows and Mac systems, the assumption is made that they already have names as well.

Each system has the equivalent of a hosts file that contains all the preceding addresses plus the localhost address. A DNS server can work on this network as well, providing not only local resolution, but also Internet resolution and saving you the trouble of putting hosts files in each system. You could also assign a static IP to rumble.fish.net, configure a DHCP server on it, and let the other systems get their IP address through DHCP. Each additional step will require more initial effort on your part, but for larger networks, it is definitely worth the trouble.

The format of the hosts file is consistent across the various platforms. Each one will resemble Listing 30.1.
