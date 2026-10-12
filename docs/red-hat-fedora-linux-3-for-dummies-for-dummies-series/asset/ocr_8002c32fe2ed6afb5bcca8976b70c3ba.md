# Configuring your external Internet connection

The forwarding we describe in the preceding section takes care of routing the packets to and from the Internet via your Internet gateway. Follow these steps to configure the Internet gateway:

+   1. Install an Ethernet or Wi-Fi NIC on your Fedora Core Internet gateway.
+   
+      You use this NIC to connect your Internet gateway to your private network. We identify this device as the internal NIC ( eth0 ).

+   2. Install an Ethernet NIC on your Fedora Core Internet gateway; skip this step and the next one if you're using a telephone modem for your Internet connection.
+   
+      You use this NIC to connect to your DSL or cable modem. We identify this device as the external NIC ( eth1 ).

+   3. Connect the external NIC to the DSL or cable modem with a Cat-5 cable.

+   4. Configure your Internet gateway to allow packet forwarding. (Refer to the section “Forwarding network traffic through your gateway,” earlier in this chapter.)

+   5. Assign an IP address to each NIC. For example, assign the address $192.168.1.254$ to your internal NIC ( eth0 ) and $192.168.32.254$ to the external NIC ( eth1 ).
+   
+      Note that when you're using a telephone or cable modem, this action is done automatically for you. Modems connect directly to your gateway and not through an Ethernet NIC; some DSL modems can also plug directly into your computer and don't require an Ethernet connection. For this book, we assume that you're connecting via an Ethernet NIC. Check your protocols. Telephone modems use the Point-to-Point Protocol (PPP), whereas cable and some DSL modems use DHCP (Dynamic Host Configuration Protocol), which assigns an IP address to their respective interfaces.

+   6. Assign a default route that points to the Internet connection device. The PPP and DHCP protocols do this step automatically.

![](bbox=[0.05, 0.7, 0.14, 0.78])

# Configuring your internal private network connection

Follow these steps to configure computers or network devices on your private network to connect to the Internet through the gateway:

+   1. Configure your computer with its network parameters.
+   
+      In other words, assign an IP address and a netmask (and, optionally, but recommended, a host and network name) to each computer when you're using an Ethernet-based LAN. On a wireless network, you have to assign the IP address, netmask, common network name, and encryption key.