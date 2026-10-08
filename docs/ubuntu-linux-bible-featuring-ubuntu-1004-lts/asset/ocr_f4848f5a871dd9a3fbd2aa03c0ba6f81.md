# Chapter 26: File Transfer and Sharing

interested in a specific torrent—once peers are communicating with each other, the tracker is no longer necessary. As you'd expect, initiating a torrent, at least one peer must provide a complete set of the files in the torrent, which is known as seeding in BitTorrent vernacular.

One interesting optimization in BitTorrent is that peers retrieve and share the files in a random sequence of chunks. This means that, while many peers may be in the process of downloading the collection of files that make up a torrent, it's normal to expect that no two of them are sharing the same portions of those files. This makes torrents quite durable—even if the tracker and the host that is seeding a torrent go away, it's quite possible that all the peers together have a complete set of files in the torrent—they all just have to trade missing chunks with each other. This is known as a distributed copy in BitTorrent terms.

BitTorrent is a great piece of software, an impressive protocol, an excellent software distribution mechanism, and a good example of how P2P file sharing can guarantee the free sharing of any kind over the NET. It is also free.

# Tip

If you have problems getting BitTorrent client to work, make sure that any firewall that you are running does not block TCP ports 6881-6999, which are the ports that are used by the current version of BitTorrent. If you are experiencing performance problems and are behind a configurable gateway or router, you may want to forward those ports from your external Internet interface directly to the host on which you are running your BitTorrent client. Michael Ingram has a great article on slowing downloads problems and configuring specific routers and gateways at www.slicky.com/news.php?story=493. A general discussion of port forwarding on a variety of routers is available at www.portforward.com/routers.htm.



Because Transmission is installed as part of a basic Ubuntu distribution, you don't have to do anything special to access or configure it. To start Transmission, select the Applications Internet Transmission BitTorrent menu. This will display an initial dialog that explains the implications of using a file-sharing client like Transmission. Click “I Accept” to indicate that you understand this. The dialog shown in Figure 26-12 displays.

# FIGURE 26-12

The initial Transmission dialog

![](bbox=[0.039, 0.755, 0.541, 0.943])