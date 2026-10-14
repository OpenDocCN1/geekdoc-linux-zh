
Here is the syntax to use:

```
# sshfs user@remote_address:/path/to/music/ /mnt/test/
```

Next, you press Enter and then type in your password just like using SSH or SCP. After this is done, your remote music (MP3s, Ogg files, etc.) is accessible at /mnt/test/path/to/music/. All you need to do is add this path to your Edna config file and (re)start Edna. Bam! Done. Now, you have access to your tunes despite the man trying to keep you down ;-). Perhaps the greatest benefit of using SSHFS and Edna is that you can share your remote music with others on your network as well.

Here is the entry, keeping consistent with the previous example entries:

```
dir4 = /mnt/test/path/to/music/ = Remote Tunes
```

If Edna is already running, you need to restart it for it to pick up the remote file. Let's send a HUP signal to the python process to accomplish the restart:

```
sudo killall -HUP python
```

Now, you should be able to access your remote files on the computer running DSL via localhost access at http://127.0.0.1:8080/Remote%20Tunes/. Other people on your local network should also be able to access your tunes via your local IP. If you don't know what it is, you can look at the Torsmo display at the upper right of your desktop or open a Terminal window and type /sbin/ifconfig and look for the four part number that comes after inet addr: on the device that is not the "local loopback" or "lo" listing.

For example, if your address turns out to be 192.168.1.200, people in your local area network could access your remote tunes by pointing their browser to http://192.168.1.200:8080/Remote%20Tunes/.

## SUMMARY

This should be enough to get you going with a basic Edna setup. As you can see, there are many ways to use Edna to enjoy your music or any other type of audio files. One last tip: If you include an image in a directory with your music, Edna displays that image while you access it. This could be a way to add some personality to your music server.

## Using Skype VoIP Service
in DSL

By adding Skype software to Damn Small Linux (DSL), you can make calls from your computer to a person at another computer (for free) or to any telephone in the world (for a bit of money). You can also use text chat to communicate with other Skype users.

Besides being offered for Linux, Skype software is available for Windows, Mac OS X, and Pocket PCs. So, if you can get a group of family, friends, or associates to sign up for Skype accounts, you can make calls, send files, and participate in chats among those people, even if they are not all using the same type of computer.

Because Skype software has been packaged for Damn Small Linux, you can easily install Skype using the MyDSL feature. You can then apply all the advantages of using DSL to your Skype application, so you can have your own calling tools that run on a low-end PC or from a custom, portable USB stick or CD.

This chapter describes how to use the Skype software package that is available for DSL to place calls to people over the Internet. It also describes how to extend your use of Skype to include other free and inexpensive services. Although this chapter describes how to set up Skype from any recent version of DSL you might have, refer to Appendix A for information on the DSL software included on the CD that comes with this book.

### NOTE

Although this chapter describes some of the free Skype services available using software created for Linux, it also touches on some of the for-pay services available from Skype. The authors of this book have no affiliation with Skype and our coverage of their products doesn't represent an endorsement of Skype. If you are interested in those services, you should research their suitability for yourself.

## INTRODUCTION TO SKYPE AND VOIP

To encourage people to purchase its voice over Internet protocol (VoIP) Internet telephone products, Skype Limited (www.skype.com) offers a variety of free Internet communications services to people who sign up for a free user account. By downloading and installing Skype software, setting up a user account, and doing some simple configuration, you can be making calls to others over the Internet within just a few minutes.

Skype describes its Internet-based telephony service as a decentralized peer-to-peer network. The concept of peer-to-peer (P2P) networked applications was popularized by file-sharing applications, such as KaZaA (www.kazaa.com), where clients can offer and share files (containing documents, music, video, or other content) directly to other clients. In its P2P VoIP offering, Skype emphasizes the decentralized aspect of how it implements its communications services.

By decentralizing the processing and networking power needed to run the Skype service, the Skype network can grow without adding more centralized servers. In other words, each client using Skype shares its processing power and network bandwidth to increase the general pool of resources available to all Skype users. So, in theory, adding more Skype users shouldn't require more servers, bandwidth, and other computing resources to maintain the same performance level for all users.

Traditionally, standard telephone service has been far superior to VoIP in quality and reliability. The following is a list of common shortcomings of VoIP services and how Skype is designed to deal with them:

- **Poor call completion**—Firewalls (which often block most incoming service requests) and network address translation (which can hide many private IP addresses behind a single public IP address) prevented many VoIP calls from getting through. To more effectively route calls, Skype uses Skype clients with public IP addresses to act as proxies to route calls to clients that are behind firewalls.
- **Poor call quality**—Inefficient routing of calls often resulted in poor quality of transmission on VoIP networks. Skype uses multiple connection paths so that the best possible route for data can be chosen as it is needed.
- **Difficult configuration**—Instead of just contacting a phone company and plugging in a phone, many VoIP services require complex firewall configuration and manual identification of servers. A simplified user interface that requires no special incoming firewall configuration makes Skype easy to set up for most users. (See Skype and Firewalls: www.skype.com/help/guides/firewall.html.)
