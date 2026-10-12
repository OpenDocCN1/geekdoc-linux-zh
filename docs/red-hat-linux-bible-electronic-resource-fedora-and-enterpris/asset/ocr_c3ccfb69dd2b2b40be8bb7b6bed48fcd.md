> **CROSS-REFERENCE:** Refer to Chapter 15 for descriptions of IP addresses, netmasks, and other information you need to set up your LAN and to Chapter 16 for information related to domain names.

With the "Edit Interface eth0" window displayed, add the following:

+   * **Configure using DHCP** — If your IP address is assigned automatically from a DHCP server, a checkmark should appear here. With DHCP checked, you don't have to set other values on this page. Remove the checkmark to set your own IP address.
+   * **IP Address** — If you set your own IP address, this is the four-part, dot-separated number that represents your computer to the network. How IP addresses are formed and how you choose them is more than can be said in a few sentences (see Chapter 15 for a more complete description). An example of a private IP address is 192.168.0.1.
+   * **Netmask** — The netmask is used to determine what part of an IP address represents the network and what part represents a particular host computer. An example of a netmask for a Class C network is 255.255.255.0.
+   * **Activate on boot** — Besides this information, you should indicate whether you want the network to start at boot time (you probably do if you have a LAN).
+   
+   Click **OK**. Then add the following information on the main screen:
+   
+   * **Set the hostname** — This is the name identifying your computer within your domain. For example, if your computer were named "baskets" in the hands on history.com domain, your full hostname may be baskets.handsonhistory.com. You can either set the domain name yourself (manually) or have it assigned automatically, if that information is being assigned by a DHCP server (automatically via DHCP).
+   * **Gateway** — This is the IP number of the computer that acts as a gateway to networks outside your LAN. This typically represents a host computer or router that routes packets between your LAN and the Internet.
+   * **Primary DNS** — This is the IP address of the host that translates computer names you request into IP addresses. It is referred to as a Domain Name System (DNS) server. You may also have Secondary and Tertiary name servers in case the first one can't be reached. (Most ISPs will give you two DNS server addresses.)

> **CROSS-REFERENCE:** To configure your LAN after installation, see Chapter 15.

+   16. **Choose a firewall configuration.** The use of a firewall has significant impact on the security of your computer. If you are connected to the Internet or to another public network, a firewall can limit the ways an intruder may break into your Linux system. Here are your choices for configuring a firewall during installation:
+   * **High** — Select this security level if you are connecting your Linux system to the Internet for Web browsing and file downloading (FTP) but don't plan to offer your system as a server to the Internet. Only explicitly defined connections are accepted.