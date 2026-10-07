
# Chapter 5 • The Hacking Top 10

number of ICMP requests to or from a single host. Using Figure 5.27 as example, a single ICMP packet from forensic1 to forensic3 is not suspicious; however, 102 packets in less than 30 seconds may raise a red flag.

Remember, this is just one example. Hping2 can also use TCP or UDP (as seen in my example with the signature.sig file) to send data, which is what makes it so dangerous. Bring up anything that looks suspicious with the customer and have them make the determination of whether or not the traffic was normal or requires a second look.

Don't take my word for it! Download hping2¹⁵ and Wireshark¹ in a laboratory environment. Test the utility out, see what it can do, and make note of the signatures it leaves. Your time in the lab may be the difference between cracking the case and the intruder getting off scot-free.

# Ettercap

Unlike many other security tools that have been misused by nefarious intent, Ettercap was pretty much designed to be a hacktool,¹⁷ and came in #11 on the top 100 network security tools survey. In 2004, it was named #9 of the top 75 security tools on the Nmap hackers mailing list.¹⁸'s current version, NG-0.7.3, was written to be more modular, enabling the user community to assist in adding new features and submitting patches. By default, Etter installs into the /usr/sbin directory, and has a block size of 362112. It was designed to be a sniffer, and specializes in Man-in-the-Middle (MITM) attacks. It boasts being able to sniff live connections, content filtering on the fly, and many other tricks of the trade.

If you are working a case and happen to come across Ettercap, you can pretty much assume something not great is being planned or is already happening. Unfortunately, applying the application installed is all you are going to get in terms of “evidence.” Since it can sniff traffic in effect promiscuous or non-promiscuous modes, you may or not be able to tell if it’s doing anything. Apart from being a very capable and configurable sniffer, the self-proclaimed “most relevant” features of Ettercap are SSH support, Secure Sockets Layer (SSL) support, ARP injection, packet filtering/dropping, traffic sniffing via tunnels remote mangling, password collection, OS fingerprinting, and connection termination. As you can see, this is very versatile, and in the hands of a skilled user, very dangerous.

- 15 http://www.hping.org/download.html
- 16 http://www.wireshark.org/
- 17 http://ettercap.sourceforge.org/index.php
- 18 http://it.slashdot.org/article.pl?id=04/11/09/1350205

![](img/fd8e85097b37559dbc07dc22fd8cb1fe_151_0.png)

I installed Ettercap on my Ubuntu 7.10 Gutsy host, Forensic1, launched it, and started sniffing my local network. Figure 5.29 shows the connections on my local subnet.

# Figure 5.29 Sniffing with Ettercap

![](img/fd8e85097b37559dbc07dc22fd8cb1fe_152_0.png)

By double-clicking on any one of these connections, you can view more detail about the packets. In my example, I selected a connection from 192.168.10.118 to 205.188.13.16 on port 5190. Incidentally, that IP address resolves to America Online, Inc, so we are looking at AOL instant message connections on port 5190.

# Figure 5.30 AOL IM Traffic

![](img/fd8e85097b37559dbc07dc22fd8cb1fe_153_0.png)

Good thing for me that I used Pidgin¹⁹ with the OTR plug-in,²⁰ or my traffic would be completely unencrypted! All you would be able to decipher was that I was having instant message conversations with a few unknown individuals.

In addition to viewing the host-to-port connections, you can also view the collected passive profiles. This view simply shows an IP address and the hostname it resolves to, as seen in Figure 5.31.

- ¹⁹ www.pidgin.im/
- ²⁰ www.cypherpunks.ca/otr/

# Figure 5.31 IP Address and Resolved Hostname

![](img/fd8e85097b37559dbc07dc22fd8cb1fe_154_0.png)

From this example, I will drill down to IP address 66.35.250.203, hostname www.sourceforge.net. The profile details including the distance (number of hops), fingerprint, OS, port, and HTTP version are displayed. (See Figure 5.32).

# Figure 5.32 Profile Details

![](img/fd8e85097b37559dbc07dc22fd8cb1fe_155_0.png)

Note: With Ettercap, I started sniffing, and we were able to see what the intruders were and are able to see. In fact, you may want to discuss putting your own system on their wire and running Ettercap to see what is taking place. In fact, chances are you belong to an organization which uses either Telnet or FTP.

# Figure 5.33 Unencrypted Traffic

![](img/fd8e85097b37559dbc07dc22fd8cb1fe_156_0.png)

While Ettercap will sniff SSH2, Figure 5.34 shows what we were.

# Figure 5.34 Encrypted Traffic

![](img/fd8e85097b37559dbc07dc22fd8cb1fe_157_0.png)

A MITM attack can only be successful when the attacker can impersonate each endpoint to the satisfaction of the other. Most cryptographic protocols include some form of endpoint authentication, specifically to prevent MITM attacks. According to wikipedia,¹ a MITM attack “… is a form of active eavesdropping in which the attacker makes independent connections with the victims making them believe they are talking directly to each other, when in fact the entire conversation is controlled by the attacker.”

- ¹ http://en.wikipedia.org/wiki/Man-in-middle_attack

# Figure 5.35 “mitm” Dropdown

![](img/fd8e85097b37559dbc07dc22fd8cb1fe_158_0.png)
