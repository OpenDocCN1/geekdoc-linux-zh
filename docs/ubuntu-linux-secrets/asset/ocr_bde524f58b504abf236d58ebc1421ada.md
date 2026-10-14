happen. It helps if you have a download manager that allows you to interrupt and restart the download process.

# Interrupting and Restarting the Download

When you're downloading a large ISO image file, things can (and often do) go wrong with your Internet connection before the entire file makes its way to your PC. Some browsers allow you to recover from an interrupted download, while others require that you start all over again.

The Firefox browser uses a download manager that's a great tool for downloading large files. The Firefox download manager keeps track of the file download and allows you to stop and restart the download as often as you want (as long as you keep the same browser window open). It also allows you to resume a previous download that failed, starting from the point of failure. This is a great feature if you're on an Internet connection that is subject to failure. Figure 2-2 shows the Firefox download manager window in action.

![](bbox=[0.18, 0.49, 0.65, 0.75])

Figure 2-2: The Firefox web browser download manager.

The download manager provides controls for pausing the download so you can resume it later. Once the download is complete, the download manager keeps a record of the download for future reference.

# Using BitTorrent to Download

Peer-to-peer (P2P) network sharing has become a popular way to distribute large files on the Internet. Instead of hosting the file as a single download on a single FTP server, a P2P system has clients register on the P2P server, which then splits the file into many small pieces for download.

As different clients retrieve the different pieces of the file, they advertise which pieces they have and offer them to other clients for downloading. Before long, an individual client can retrieve pieces of the download directly from multiple clients instead of having to go to the main server. As the client program retrieves the individual pieces, it recreates the original file. When it's retrieved all of the pieces, you've got your copy of the original file.

Although P2P has gotten a bad rap lately because some users post material that violates copyright laws, it's still a valid way to distribute large files, as long as they're legal. The Ubuntu project fully supports using P2P to distribute the various Ubuntu LiveCD versions. It's perfectly legal to use P2P to download the Ubuntu ISO image file.