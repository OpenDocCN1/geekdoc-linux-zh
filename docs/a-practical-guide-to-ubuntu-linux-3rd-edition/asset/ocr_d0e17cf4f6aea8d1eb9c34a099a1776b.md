Use the `dpkg --contents` command to list the files contained in a package that is on the system but not installed. The following command lists the files in the **dump deb** file in the **archives** directory:

```
$ dpkg --contents /var/cache/apt/archives/dump_0.4b42-1_i386.deb
```

# # BITTORRENT

The easiest way to download a BitTorrent file is to click the *torrent* file object in a Web browser or in the Nautilus File Browser. This section describes how BitTorrent works and explains how to download a BitTorrent file from the command line.

The BitTorrent protocol implements a hybrid *client*/*server* and *P2P* (page 1163) file transfer mechanism. BitTorrent efficiently distributes large amounts of static data, such as the Ubuntu installation ISO images. It can replace protocols such as anonymous FTP, where client authentication is not required. Each BitTorrent *client* that downloads a file provides additional bandwidth for uploading the file, thereby reducing the load on the initial source. In general, BitTorrent downloads proceed faster than FTP downloads. Unlike protocols such as FTP, BitTorrent groups multiple files into a single package: a BitTorrent file.

*Tracker, peer, seed, and swarm*: BitTorrent, like other P2P systems, does not use a dedicated server. Instead, the functions of a server are performed by the *tracker*, *peers*, and *seeds*. The *tracker* is a server that allows clients to communicate with each other. Each *client*\u2014called a *peer* when it has downloaded part of the BitTorrent file and a *seed* once it has downloaded the entire BitTorrent file\u2014acts as an additional source for the BitTorrent file. Peers and seeds are collectively called a *swarm*. As with a P2P network, a member of a swarm uploads to other clients the sections of the BitTorrent file it has already downloaded. There is nothing special about a *seed*: It can be removed at any time once the torrent is available for download from other *seeds*.

*The torrent*: The first step in downloading a BitTorrent file is to locate or acquire the *torrent*, a file with the filename extension of *.torrent*. A torrent contains pertinent information (metadata) about the BitTorrent file to be downloaded, such as its size and the location of the *tracker*. You can obtain a torrent by accessing its URI, or you can acquire it via the Web, an email attachment, or other means. The BitTorrent client can then connect to the *tracker* to learn the locations of other members of the *swarm* that it can download the BitTorrent file from.

*Manners*: Once you have downloaded a BitTorrent file (the local system has become a *seed*), it is good manners to allow the local BitTorrent client to continue to run so peers (clients that have not downloaded the entire BitTorrent file) can upload *at least* as much information as you have downloaded.