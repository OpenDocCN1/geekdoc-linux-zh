There is, however, an attack called “IP Spoofing” where a person on the outside sends in packets with doctored source and destination addresses so that it appears that the packet came from inside the network. They can’t connect to any machines on the inside (because no packets will come back to them), but they can send packets in that could cause trouble with buggy software. For example, if could send in a whole bunch of SYN packets (called a SYN Flooding attack) making a machine think that someone is trying to set up a whole bunch of connections. This can crippe a machine by using all its resources. Luckily, there are ways to protect against these kinds of attacks. For example, you could add a rule to the input chain that makes sure that no packets coming in off the interface connected to the Internet claim to have IP addresses from the private network. For example, if you are using the network address 192.168.1.0 for your private network and are connecting to the Internet through the ppp0 interface, the following rule would protect your from an IP spoofing attack:

```
# i chains -A input -i ppp0 -s 192.168.1.0/24 -j DENY
```

There are drawbacks to IP masquerading, however. Because no host from the outside can connect to a host on the inside (the other direction is okay, of course), certain protocols don’t work very well. For example, there are two types of FTP: passive and active. With active FTP, the client makes a connection to the server to exchange commands and responses, but the server makes a connection back to the client machine to send the files. With IP masquerading in use, the FTP server won’t be able to make a connection with the client machine, unless the user is FTPing from the firewall. Active FTP is the default for most FTP clients (for example, when you run ftp from the command line). With passive FTP, however, the client is always the one making the connections, so passive FTP works without any hitches. Most Internet browsers use passive FTP.

People are actively working at trying to fix the problems with IP masquerading, however. For example, there are several kernel modules that you can load that help deal with certain problematic protocols. You can find them in the directory /lib/modules/2.2.5/ipv4. They are all the modules with “masq” in their name somewhere. The name of the module generally offers a key to what the module was designed to do. For example, ip_masq_irc is for helping masquerade the Internet Relay Chat protocol.

Setting up your firewall to use IP masquerading is really easy. After you have configured your kernel correctly (see the first part of this chapter—that would be the only hard part), you set up rules in the forward chain that have MASQ set as their target for all the packets that you want to masquerade. In my case, it’s very simple. Any packets that are from one of the local networks and not destined for a local network are masqueraded.

```
# i chains -A forward -s 192.168.0.0/16 -d ! 192.168.0.0/16 -j MASQ
```

You can be more selective, of course, and only masquerade certain types of packets.