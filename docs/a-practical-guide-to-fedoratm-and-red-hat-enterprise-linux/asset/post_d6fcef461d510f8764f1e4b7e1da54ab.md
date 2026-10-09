
## CONNECTING SEVERAL SERVERS TO A SINGLE INTERNET CONNECTION

DNAT (destination NAT) can set up rules that allow clients from the Internet to send packets to servers on the LAN. This example sets up an SMTP mail server on 192.168.1.33 and an HTTP (Web) server on 192.168.1.34. Both protocols use TCP. SMTP uses port 25 and HTTP uses port 80, so the rules match TCP packets with destination ports of 25 and 80. The example assumes the mail server does not make outgoing connections and uses another server on the LAN for DNS and mail relaying. Both commands put rules in the PREROUTING chain of the NAT table (`-A PREROUTING -t NAT`):

```bash
# iptables -t PREROUTING -t NAT -p tcp --dport 25 -j DNAT --to-destination 192.168.1.33:25
# iptables -t PREROUTING -t NAT -p tcp --dport 80 -j DNAT --to-destination 192.168.1.34:80
```

To match these rules, the packet must use the TCP protocol (`-p tcp`) and have a destination port of either 25 (first rule, `--dport 25`) or 80 (second rule, `--dport 80`).

The `--to-destination` is a target specific to the PREROUTING and OUTPUT chains of the NAT table; it alters the destination address and port of matched packets as specified. As with MASQUERADE and SNAT, subsequent packets in the same and related connections are altered the same way.

The fact that the servers cannot originate connections means that neither server can be exploited to participate in a *DDoS attack* (page 1246) on systems on the Internet, nor can they send private data from the local system back to a malicious user’s system.

## CHAPTER SUMMARY

A firewall, as implemented by **firewalld**, is designed to prevent unauthorized access to a system or network. Such a firewall can protect just the single system it runs on or can protect the system it runs on plus other systems on a LAN that connect to the Internet through the system running the firewall. The **firewalld** service is replacing the older **iptables** service. The **firewalld** daemon accepts changes to the firewall while it is running. The **firewalld** daemon (which runs in user space) works with **netfilter** (which runs in kernel space) to filter network packets. A firewalld firewall allows you to configure the runtime configuration and the permanent configuration.

The **firewalld** daemon has a D-Bus interface that allows it to communicate with processes, including allowing authenticated processes to reconfigure the firewall as they run. It also has a GUI (*firewall-config*) and a CLI (*firewall-cmd*). The **firewall-cmd** utility has direct commands that allow you to give *iptables* commands to **firewalld**. In an emergency you can put the firewall in panic mode, in which it drops all packets.

An **iptables** command sets up or maintains in the kernel rules that control the flow of network packets; rules are stored in chains. Each rule includes a criteria part and an action part, called a target. When the criteria part matches a network packet, the kernel applies the action from the rule to the packet.

Chains are collected in three tables: Filter, NAT, and Mangle. Filter (the default table) DROPs or ACCEPTs packets based on their content. NAT (the Network Address Translation table) translates the source or destination field in packet headers. Mangle is used exclusively to alter the TOS (type of service), TTL (time to live), and MARK fields in a packet. The connection tracking machine, which is handled by the conntrack module, defines rules that match criteria based on the state of the connection a packet is part of.

## EXERCISES

- 1. How would you put a **firewalld** firewall in panic mode from **firewall-config**? From **firewall-cmd**?
- 2. How can you tell whether **firewalld** is running?
- 3. Which **firewall-cmd** command would you use to cause the runtime configuration of the firewall to trust the FTP service? Which command would cause the permanent configuration to trust the FTP service?
- 4. Which **firewall-cmd** command would verify that the FTP service was trusted in the runtime configuration? In the permanent configuration?
- 5. How would you use **firewall-cmd** to open ports for SMTP packets (TCP and UDP port 25) in the permanent configuration? Verify that these ports are open.

## ADVANCED EXERCISES

- 6. Define an **iptables** rule that will reject incoming connections on the TELNET port.
- 7. Which **iptables** command would list all rules including line numbers that specify each rule's position in the chain?
- 8. Write an **iptables** (IPv4) rule that silently blocks incoming SMTP connections from 10.10.0.10.
- 9. Run the rule from exercise 8 using the direct option of **firewall-cmd**.

*This page intentionally left blank*

# 26

# APACHE (httpd): Setting Up a Web Server

## In This Chapter

- Running an Apache Web Server . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 935
- JumpStart: Getting Apache Up and Running . . . . . . . . . . . . . . . . . . . . . . 936
- Filesystem Layout . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 938
- Configuration Directives . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 939
- Contexts and Containers . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 945
- Advanced Configuration Directives . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 949
- Redirects . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 962
- Content Negotiation . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 962
- Type Maps . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 963
- MultiViews . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 963
- Virtual Hosts . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 965
- Troubleshooting . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 967

## Objectives

After reading this chapter you should be able to:

- Explain the purpose of Apache and describe the use of several available modules
- Configure an Apache server to listen on the network and provide simple content
- Customize names, addresses, ports, and the location of content, logs, and scripts of an Apache server
- Allow users to publish content from their home directories
- Configure virtual hosts to display different content
- Configure password-protected directory hierarchies, host-based access control, directory options, and SELinux Booleans to secure access to Web content

The World Wide Web (WWW or Web for short), is a collection of servers that hold material, called *content*, that (Web) browsers can display. Each of the servers on the Web is connected to the Internet, a network of networks (an *internetwork*). Much of the content on the Web is coded in HTML (Hypertext Markup Language, page 1254). *Hypertext*, the links you click on a Web page, allows browsers to display and react to links that point to other Web pages on the Internet.

Apache is the most popular Web server on the Internet. It is both robust and extensible. The ease with which you can install, configure, and run it in the Linux environment makes it an obvious choice for publishing content on the World Wide Web. The Apache server and related projects are developed and maintained by the Apache Software Foundation (ASF), a not-for-profit corporation formed in June 1999. The ASF grew out of the Apache Group, which was established in 1995 to develop the Apache server.

This chapter starts by providing introductory information about Apache. Following this information is the JumpStart section, which describes the minimal steps needed to get Apache up and running. Next is “Filesystem Layout,” which details where the various Apache files are located.

Configuration directives are a key part of Apache and are discussed starting on page 939. This section includes coverage of contexts and containers, two features/concepts that are critical to understanding Apache. The next section, which starts on page 962, covers advanced Apache configuration: redirects, content negotiation, directory indexing, virtual hosts, troubleshooting, and modules you can use with Apache, including CGI and SSL.

## INTRODUCTION

Apache is a server that responds to requests from Web browsers, or *clients*, such as Firefox, Netscape, lynx, elinks, and Internet Explorer. When you enter the address of a Web page (a *URL*, page 1279) in a Web browser’s location bar, the browser sends a request over the Internet to the (Apache) server at that address. In response, the server sends (serves) the requested content back to the browser. The browser then displays or plays the content, which might be a textual document, song, picture, video clip, or other information.

Aside from add-on modules that can interact with the content, Apache looks only at the type of data it is sending so that it can specify the correct *MIME* (page 1261) type; otherwise it remains oblivious to the content itself. Server administration and content creation are two different aspects of bringing up a Web site. This chapter concentrates on setting up and running an Apache server; it spends little time discussing content creation.

Apache, like the *Linux* kernel, uses external modules to increase load-time flexibility and to allow parts of its code to be recompiled without recompiling the whole program. Rather than being part of the Apache binary, modules are stored as separate files that can be loaded when Apache is started.
