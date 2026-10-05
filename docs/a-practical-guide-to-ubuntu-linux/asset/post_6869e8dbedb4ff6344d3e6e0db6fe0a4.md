
# CONNECTING SEVERAL SERVERS TO A SINGLE Internet CONNECTION

DNAT (destination NAT) can set up rules that allow clients from the Internet to send packets to servers on the LAN. This example sets up an SMTP mail server on 192.168.1.33 and an Apache (Web) server on 192.168.1.34. Both protocols use TCP; SMTP uses port 25 and Apache uses port 80, so the rules match TCP packets with destination ports of 25 and 80. The example assumes that the mail server does not make outgoing connections and uses another server for DNS and mail relay. By putting commands in the PREROUTING chain of NAT (-A PREROUTING -t NAT):

```
$ sudo iptables -A PREROUTING -t NAT -p tcp --dport 25 --to-192.168.0.33:25 -j DNAT
$ sudo iptables -A PREROUTING -t NAT -p tcp --dport 80 --to-192.168.0.34:80 -j DNAT
```

To match these rules, the packet must use the TCP protocol and have a destination port of either 25 (first, --dport 25) or 80 (second, --dport 80).

The --to is a target in the PREROUTING and OUTPUT chains of the NAT table; it alters the destination address and port of matched packets as specified. With MASQUERADE and SNAT, subsequent packets in the same and related chains are altered by the same.

The fact that the servers cannot originate connections means neither server can be exploited to participate in a DDoS attack (page 1144) on systems on the Internet, nor can they send private data from the local system back to a malicious user's system.

# CHAPTER SUMMARY

A firewall, as iptables, gufw, or firestarter, is designed to prevent unauthorized access to a system or network. The firestarter and gufw utilities are sophisticated, graphical tools for building and maintaining a firewall. Each can protect the system it runs on or protect the system it runs on plus systems on a LAN that connects to the Internet through the system firestarter or gufw.

An iptables command sets or maintains in the kernel rules that control the flow of network packets; rules are stored in chains. Each rule includes a criteria part and an action part, called a target. The criteria part matches a network packet, the kernel applies the action from the rule to the packet.

Chains are collected in three tables: Filter, NAT, and Mangle. Filter (the default table) DROPS or ACCEPTs packets based on their content. NAT (the Network Address Translation table) translates the source or destination field of packets. Mangle is used exclusively to alter the TOS (type of service), TTL (time to live), and MARK fields in a packet. The connection tracking machine, which is handled by the conntrack module, defines rules that match criteria based on the state of the connection packet is part of.

# EXERCISES

- 1. How would you remove all iptables rules and chains?
2. What is firestarter? How is it related to iptables?
3. What is the easiest way to set up a rule using firestarter?
4. How would you list all current iptables rules?
5. How is configuring iptables different from configuring most Linux services?
6. Define an iptables rule that will reject incoming connections on the TEL-NET port.
7. What does NAT stand for? What does the NAT table do?

# ADVANCED EXERCISES

- 8. What does the conntrack module do?
9. What do rule match criteria do? What are they used for?
10. What do packet match criteria do? What are they used for?
11. Which utilities copy packet filtering rules to and from the kernel? How do they work?
12. Define a rule that will silently block incoming SMTP connections from spmr.com.

# 26

# APACHE: SETTING UP A WEB SERVER

# IN THIS CHAPTER

- JumpStart: Getting Apache Up and Running ................ 903
- Configuring Apache ................................. 905
- Configuration Directives ................ 909
- Contexts and Containers ....................... 915
- The Ubuntu apache2.conf File ................ 932
- Redirects ............................................ 935
- Content Negotiation ........................... 935
- Type Maps .......................................... 935
- MultiViews ........................................ 936
- Virtual Hosts .......................................... 937
- Troubleshooting ................................ 940

The World Wide Web (WWW or Web for short), is a collection of servers that hold that material, called content, that Web browsers (or just browsers) can display. Each of the servers on the Web is connected to the Internet, a network of networks (internet-work). Much of the content on the Web is coded in HTML (Hypertext Markup Language, page 1152). Hypertext, the links you click on a Web page, allows browsers to display and react to other Web pages on the Internet.

Apache is the most popular server on the Internet. It is both robust and extensible. The ease with which you can install, configure, and run in the Linux environment makes it an obvious choice for publishing content on the World Wide Web. The Apache server and related projects are developed and maintained by the Apache Software Foundation (ASF), a not-for-profit corporation formed in June 1999. The ASF grew out of the Apache Group, which was established in 1995 to develop the Apache server.

This chapter starts by providing introductory information about Apache. Following this information is the JumpStart section, which describes the minimal steps needed to get Apache up and running. Next is “Filesystem Layout,” which tells you where the Apache files are located.

Configuration directives (referred to simply as directives) are a key part of Apache and are discussed starting on page 909. This section includes coverage of contexts and containers, two features/concepts that are critical to understanding. The next section, which starts on 932, explains the main Apache configuration file, apache2.conf, as distributed by Ubuntu. The final pages of the chapter cover virtual hosts, troubleshooting, and modules you can use with Apache.

# INTRODUCTION

Apache is a server that responds to requests from Web browsers, or clients, such as Firefox, Netscape, lynx, and Internet Explorer. When you enter the address of a Web page (a URI, page 1179) in a browser's location bar, the browser sends a request over the Internet to the server at that address. In response, the server sends the requested content back to the browser. The browser displays or plays the content, which might be a song, picture, video clip, or other information.

- Content Aside from add-on modules that can interact with the content, Apache looks only at the type of data it is sending so that it specify the correct MIME (page 1160); otherwise it remains oblivious to the content itself. Server administration and content creation are two different aspects of bringing up a Web site. This chapter concentrates on setting up and running an Apache server; it like the Linux kernel, uses external modules to increase load-time flexibility and allows parts of its code to be recompiled without recompiling the whole program. Rather than being part of the Apache binary, modules are stored as separate files that can be loaded when Apache is started.
- Modules The Debian/Ubuntu Apache team provides one of the easiest-to-use Apache uses external modules, called dynamic shared objects (DSOs), for basic and advanced functions; there is not much to Apache without these modules. Apache also uses modules to extend its functionality. For example, modules can process scripts in Perl, PHP, Python, and other languages; use several different methods to authenticate users; facilitate publishing content; and process contextual content, such as audio. The list of modules written by the ASF and third-party developers is constantly growing. For more information refer to “Modules” on page 941.
- Setup Most packages that provide a Web interface and that depend on Apache run as installed; typically you do not need to modify the configuration files.
