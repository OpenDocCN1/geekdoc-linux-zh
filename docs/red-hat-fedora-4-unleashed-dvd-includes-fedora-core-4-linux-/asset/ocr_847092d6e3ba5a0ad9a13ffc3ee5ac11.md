Start system-config-securitylevel1 from the System Settings menu's Security level menu item. You are prompted for the root password and the client's window then appears. Figure 33.2 shows firewalling enabled for the eth0 Ethernet device, allowing incoming secure shell and HTTP requests.

![](bbox=[0.3, 0.18, 0.7, 0.45])

**FIGURE 33.2** Fedora's system-config-securitylevel1 client can also be used to quickly generate and implement standard or simple custom firewall rules for Linux.

# ### Fedora and Firewalling

Fedora also supports the older—but still popular—ipchains packet-filtering software, which can be used to construct effective firewalling rules on Linux firewalls, gateways, servers, and workstations. Linux also supports the more capable iptables, or NetFilter system, which offers additional controls and logging facilities used to build filtering *rule sets* or filtering instructions.

Unfortunately, Fedora does not include any command-line or graphical interface utilities you can use to build, save, and test complex iptables rulesets, usually implemented as shell scripts. You need to do this if you want to control outgoing as well as incoming packets. However, you can write your own using a text editor such as vi. Many experienced Linux users hand-tune rulesets for specific application in advanced network situations, such as development of routing rules.

For a good overview and all the details about using iptables for a variety of gateway and firewall systems, read Robert L. Ziegler's excellent book, *Linux Firewalls, Second Edition*, available from New Riders. You can also browse to his site at http://www.linux-firewall-tools.com/linux/firewall/index.html, which offers a graphical, web-based firewall design and construction tool you can use to quickly build a custom ipchains-based ruleset file.

You can use Fedora to create a custom firewall, perhaps supporting IP masquerading (also known as *NAT*) by using either ipchains or iptables. You'll find two sample scripts under the /usr/share/doc/rp-pppoe/configs directory; these are used when connecting to the Internet using a digital subscriber line (DSL).