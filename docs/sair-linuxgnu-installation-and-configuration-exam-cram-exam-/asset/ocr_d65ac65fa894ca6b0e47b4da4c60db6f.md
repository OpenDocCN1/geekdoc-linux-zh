![](bbox=[0.06, 0.07, 0.93, 0.57])

Figure 5.1 Network configuration example based on Caldera Linux setup.

+   - **IP address**—If you have a static IP address, you also need to know the network mask. If your computer will get its IP address from a Dynamic Host Configuration Protocol (DHCP) server, just choose the appropriate option. A DHCP server temporarily assigns IP addresses to different computers on a network.
+   
+   - **Network mask**—If you specified an IP address, you need a network mask. A network mask, such as 255.255.255.0, limits the range of possible IP addresses on your local network. Network masks are sometimes called subnet masks.
+   
+   - **Nameserver**—A nameserver includes a database of names, like mommabeans.com, and the corresponding IP address of each, such as 192.168.10. You need the IP address for your nameserver and any secondary nameservers for your network. Nameservers are also known as Domain Name Servers (DNS) or as the Berkeley Internet Name Daemon (BIND) servers.
+   
+   - **Gateway**—If your network is connected to any other network, you need the IP address of the computer that serves as the junction between the networks. In the example shown in Figure 5.1, the address is 192.168.10.1
+   
+   - **Hostname**—You need a name for your computer, and it needs to be different from any other computer on your network. In the example shown in Figure 5.1, the hostname is linux.