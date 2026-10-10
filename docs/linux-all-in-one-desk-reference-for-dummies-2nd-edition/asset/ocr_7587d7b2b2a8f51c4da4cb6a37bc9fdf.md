WEP has its weaknesses, but it's better than nothing. You can use it in smaller wireless LANs where sharing the same key among all wireless stations is not an onerous task.

![](bbox=[0.11, 0.2, 0.2, 0.28])

Work is underway to provide better security than WEP for wireless networks. In 2003, the Wi-Fi Alliance published a specification called **Wi-Fi Protected Access (WPA)** that replaced the existing WEP standard and improved security by making some changes. For example, unlike WEP, which uses fixed keys, the WPA standard uses **Temporal Key Integrity Protocol (TKIP)**, which generates new keys for every 10K of data transmitted over the network. This makes WPA more difficult to break. In 2004, the Wi-Fi Alliance introduced a follow-on to WPA called the **Wi-Fi Protected Access 2 (WPA2** $\longrightarrow$ the second generation of WPA security). WPA2 is based on the final **IEEE 802.11i** standard, which uses public key encryption with digital certificates and an authentication, authorization, and accounting **RADIUS** (**Remote Authentication Dial-In User Service**) server to provide better security for wireless Ethernet networks. WPA2 uses the **Advanced Encryption Standard (AES)** for data encryption.

# # Setting Up the Wireless Hardware

To set up the wireless connection, you need a wireless access point and a wireless network card in each PC. You can also set up an ad hoc wireless network among two or more PCs with wireless network cards, but that is a standalone wireless LAN among those PCs only. In this section, I focus on the scenario in which you want to set up a wireless connection to an established LAN that has a wired Internet connection through a cable modem or DSL.

In addition to the wireless access point, you also need a cable modem or DSL connection to the Internet, along with a **NAT** router and hub, as described in the previous chapters of this minibook. Figure 3-1 shows a typical setup for wireless Internet access through an existing cable modem or DSL connection.

As Figure 3-1 shows, the LAN has both wired and wireless PCs. In this example, either a cable or DSL modem connects the LAN to the Internet through a NAT router and hub. Laptops with wireless network cards connect to the LAN through a wireless access point attached to one of the RJ-45 ports on the hub. To connect desktop PCs to this wireless network, you can use a USB wireless network card (which connects to a USB port).

![](bbox=[0.12, 0.8, 0.22, 0.88])

If you have not yet purchased a NAT router and hub for your cable or DSL connection, consider buying a router and hub that has a built-in wireless access point.