
specific sequence of steps, or specific input to give to a network program, so that the program becomes confused and tries to use computer memory inappropriately: The buffer, or memory space, reserved for a part of the program overflows. The result can be corruption of system data, a crashed server, or even direct root access, any of which may be the goal of the attacker.

- **Denial-of-service (DoS)** attacks try to overwhelm a server so that valid users cannot access it. This is often done by attacking numerous insecure systems and using all of them at the same time to send requests to a server. This is called a **distributed DoS (DDoS)** attack. Services such as DNS and the Web are among those vulnerable to this type of attack. Because a server is designed to accept any incoming connection, this type of attack can be very hard to anticipate and prevent, though features in modern routers and in newer protocols make prevention easier.

- **Port scanning** is a technique used by both attackers and system administrators checking the security of their network. Networked applications in Linux typically (but not always) communicate with other systems by using ports. A **port** is a number, like an address, associated with an application running on a computer. Many port numbers are predefined for standard services; others are used on an as-needed basis. A port-scanning program sends packets to a server to gain information about the server based on its response. Port scanning normally involves sending packets to many ports or sending malformed packets to gain knowledge that the host is not intentionally sharing.

> If you are a network administrator with responsibility for the security of a particular network, feel free to use port scanning and packet-sniffing tools to learn about your network's weaknesses and improve your security. For any other networks, ask before you act or you risk causing yourself and the other network administrator many problems.

- **Packet sniffing** (also called **network traffic analysis**) is another technique used by both attackers and skilled network administrators studying the network. Sniffing lets you see the headers and data contained within every packet on a network, not just those that are addressed to your own host.

## Security Tools

The most widely used port-scanning utility is **nmap**, the network mapper. **nmap** is a powerful command-line utility that can use a variety of different scanning methods. **nmap** is installed by default on Red Hat Linux and Fedora.

The home page for the **nmap** utility is www.insecure.org/nmap, where you can also find a number of very interesting security-related articles. One of the most valuable is the list of 75 most used security utilities, from a survey of hundreds of network administrators. You can find this list at www.insecure.org/tools.html. A simple example of using nmap to scan a host is shown here:

```
# nmap -sS www.myplace.net
```

Although nmap is not difficult to use, the nmapfe utility provides a nice graphical interface that is useful both when you are learning to use the utility and when you expect to collect a lot of data that is more easily viewed in a graphical environment. Figure 15-9 shows this utility, which is part of the Nmap Front End package, located on Fedora CD 3 (this package is not installed by default).

![](img/43f64015de86d989e30eff5bb284fb96_722_0.png)

### Figure 15-9 The nmapfe port-scanning utility

The IPTraf program is a popular tool for viewing network activity on a LAN. It doesn't display the data within packets, but instead displays individual network connections, with protocol and other data listed for each one. It also displays statistics by protocol, by interface, by host name, or IP address. You can set up filters to track only certain protocols, certain host names, or certain IP addresses. The home page of IPTraf is http://cebu.mozcom.com/~riker/iptraf/, but it is included on CD 3 of Fedora (it is not installed by default). Start it with the command iptraf. Figure 15-10 shows a configuration menu within IPTraf.

The tcpdump command-line utility provides functionality similar to the IPTraf program, but it also includes more detailed information about packets on your network. This utility is installed by default on Red Hat Linux and Fedora using the categories recommended in Chapter 8, "Installing Linux." Using tcpdump, you can examine the headers for each packet and save that information to a file for later analysis. You can also save the data within packets to a file, having tcpdump act as a network sniffer.

![](img/43f64015de86d989e30eff5bb284fb96_723_0.png)

### Figure 15-10 The IPTraf network traffic analysis program

One of the best packet-sniffing tools is Ethereal, a graphical network traffic analysis tool. Though it's not installed by default on Red Hat Linux or Fedora, you can add it to your system by installing the following two packages from Fedora CD 3: ethereal and ethereal-gnome.

The first of these packages includes documentation; the second includes the actual Ethereal program and setup instructions for the GNOME graphical desktop. If you're running other versions of Linux, packaged binaries are also likely to be available for your system. Visit the Ethereal home page at www.ethereal.com or your favorite Linux download site (such as rpmfind.net or freshmeat.net). To start the program, execute the ethereal command from any graphical command-line window. Figure 15-11 shows the Ethereal window.

![](img/43f64015de86d989e30eff5bb284fb96_723_1.png)

The Ethereal packages also include a text-mode version called tethereal.

A special type of security software is called an intrusion detection system (IDS). An IDS watches the network for activity that may indicate that an attacker is looking for a way to enter your server. For example, when a person uses the nmap program to perform a port scan of your server, an intrusion detection program sees that certain network activity is coming from a port scanner, which indicates the presence of an attacker.

A freely available IDS is the Linux Intrusion Detection System (LIDS). LIDS is a challenge to use, but provides a level of protection that's hard to match with most other tools. LIDS adds a module to the Linux kernel that blocks access to resources for all users—including root—except as configured by LIDS. You can download LIDS from www.lids.org. Specific features of LIDS include:

![](img/43f64015de86d989e30eff5bb284fb96_724_0.png)

### Figure 15-11 The Ethereal network traffic analysis program

- Port scanner detection within the kernel
- Ability to hide files completely or make them read-only, even to root
- Ability to hide processes completely or block which other processes can send signals to them (effectively blocking the use of the kill command to stop or restart an application)
- Access Control Lists (ACLs) (data structures that define who can access individual directories and programs)
- Time-based restrictions stating a task can only be performed or a file accessed during specific times during the day (this is similar to features offered by such services as Pluggable Authentication Modules, but LIDS performs this directly in the Linux kernel)

After you have started using security tools, you can test the security of your servers by performing a security audit, a review or test of how secure your system really is and what needs to be done to improve its security. Such an audit can take many forms. For example, if you work in an organization that has a well-defined security policy, one type of security audit would consist of a careful review of that policy to see where the systems, system administrators, management team, or end-users fall short in implementing that policy. Software can also be used to perform an automated attack on your servers using known weaknesses and typical attacker techniques.

The Security Administrator's Integrated Network Tool (SAINT) is a utility that uses a Web browser interface to manage an "attack" on your network and report to you the vulnerabilities it finds. It is similar to using a port scanner to locate potentially open network
