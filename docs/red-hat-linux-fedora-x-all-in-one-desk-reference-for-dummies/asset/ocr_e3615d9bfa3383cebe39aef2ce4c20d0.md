# Joining the BitTorrent 101

If you don't find the correct BitTorrent RPM file at torrent.dulug.duke.edu/btrprms/, you can always download the files from the official BitTorrent home page at bitconjur.org/BitTorrent/. For example, to download and install BitTorrent 3.3, open a terminal and type the following commands:

```
wget http://bitconjur.org/BitTorrent/BitTorrent-3.3.tar.gz
tar -xzf BitTorrent-3.3.tar.gz
```

In this case, the BitTorrent software is installed in the BitTorrent-3.3 subdirectory of the current directory and you have to run the BitTorrent client from that subdirectory.

# Open incoming TCP ports used by BitTorrent

Typically, your system runs a firewall that restricts access to many of the ports. BitTorrent, however, requires that you open up the TCP ports 6881 through 6999 so that BitTorrent clients can contact your system and request updates. To open TCP ports 6881 through 6999, type the following command in a terminal window:

```
iptables -I RH-Firewall-1-INPUT --protocol tcp --dport 6881:6899 -i eth0 -j ACCEPT
```

This command assumes that your system connects to the Internet through its Ethernet interface and interface is eth0 (the first Ethernet card). Change eth0 to the name of the external network interface of your system. For example, if it's the second Ethernet card, the interface is eth1. For a dial-up connection, the interface is ppp0.

# Start BitTorrent transfers

To download BitTorrent, you have to run the BitTorrent client. Use a URL to download the torrent, which refers to the collection of files that you want to download. The URL also identifies the tracker — the server that hooks your system's BitTorrent client with others that can provide parts of the files you want. In turn, the tracker also lets others clients requesting the torrent from your system.

Follow these steps to download one of the Fedora Core torrents:

+   1 Visit the Fedora Core tracker at torrent.dulug.duke.

You find a list of different torrent files listed at this site. Locate the file that you want. For example, if you are planning to burn Fedora Core CDs, you want the torrent for the Fedora Core binary OS images.