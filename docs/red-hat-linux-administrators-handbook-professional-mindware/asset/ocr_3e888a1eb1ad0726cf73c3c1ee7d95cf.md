Because of this, you need to shut the windows and lock the doors. Some guidelines for basic firewall security:

+   * **Turn off any unneeded services.** To go one step further, consider disabling sendmail, finger, netstat, systat, bootp, and FTP

+   * **Limit the number of people who have shell access to the firewall.** If you have only one or two user accounts, miscreants have to get very lucky to find one of them.

+   * **Don't use the same password on the firewall as you do elsewhere.** Sometimes, people fall into the trap of using the same password for many different computers. Don't do that here! Otherwise, your network may topple like a line of dominos.

+   * **Make physical security a huge consideration.** Whereas you may find it acceptable to have your desktop machine sitting in an open office or cubicle, you should keep tighter tabs on the physical access people have to your firewall.

Firewalls come in all varieties. Some are software applications, while others are sold as hardware. Many cost in the tens of thousands of dollars, while others are free. Firewalls can usually be classified in one of two categories: packet-filtering firewalls or application-level firewalls.

# # Packet filters

Packet filters do nothing more than take each packet, test it against a set of rules, and either allow or deny the packet to reach the other network. Packet filters are fast, simple, and effective ways of deciding which traffic passes and which does not. Packet filters exist at the network level and do not concern themselves with the data contained within the packets.

Typically, a packet filter has the capability to examine the source IP address, destination IP address, source port number, destination port number, and protocol type. It can also distinguish among the separate network interfaces on your computer. This way, someone forging one of your IP addresses from the outside world can be blocked. Table 16-1 shows the strengths and weaknesses of packet filters.