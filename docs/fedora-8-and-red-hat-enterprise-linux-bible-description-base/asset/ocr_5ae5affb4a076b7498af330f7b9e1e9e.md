A small icon shaped like a yellow man appears in the system tray on your desktop when Pidgin is running. Click that icon to have your buddy list appear and disappear. Right-click that icon and a menu lets you choose to send a new message, join a chat, or work with Pidgin account and preference settings.

# ## Sharing Files with BitTorrent

BitTorrent is a tool for distributing software content to a large number of clients over a network. What makes BitTorrent so unique is that, as you download a file to your computer, someone else can be downloading the same file from your computer. In that way, the server originally offering the file doesn't get hammered and a potentially unlimited number of people can get the file quickly.

BitTorrent is an excellent tool for the free and open source software community. For example, when a new release of Fedora comes out (now including more than 8GB of software), using BitTorrent means you don't have to wait for days for traffic on the Red Hat servers to cool down. Likewise, someone who wants to share home videos with the world can do so without having an industrial-size server and bandwidth. Of course, there are also those who are concerned that BitTorrent makes it easy to share files people shouldn't share, such as commercial movies, music, and software.

Both a text-based and graphical (bittorrent-gui) BitTorrent client are available from the Fedora repository. You can get both clients by typing the following as root user from a Terminal window:

```
# yum install bittorrent-gui
```

To use BitTorrent, visit a Web site that offers software downloads and look for a link to a torrent file representing the software, video, or other type of file you want to download. Download the torrent file to your computer. Next open the BitTorrent Window (select Applications ➜ Internet ➜ BitTorrent File Transfer). Open the torrent file (look for a file with a .torrent extension) you downloaded by selecting File ➜ Open torrent file.

The slider on the BitTorrent window lets you control how much bandwidth you will allow for others to upload the files from you that you are downloading. The more you supply, the faster you will be allowed to download the file. You can continue to make the file available to others after you are finished downloading.

To create your own torrent file for a file or directory of files you want to share, select File ➜ Make new torrent. While you can always publish your own torrent on a public server, your firewall may limit your ability to publish your own torrent to the Internet. For more information on how to publish your own content with BitTorrent, refer to the BitTorrent Guide at http://www.bittorrent.com/guide.html.