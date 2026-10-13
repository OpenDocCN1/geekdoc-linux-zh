
![](img/b7e91b81e0d84c8a5261ee14a48991b2_142_0.png)

**Figure 8-3:** Connect your LAN to the Internet through a NAT router with a built-in Ethernet hub.

When you connect a LAN to the Internet, the NAT router acts as a gateway for your LAN. The NAT router also dynamically provides IP addresses to the PCs in your LAN. Therefore, on each PC, you have to set up the networking options to obtain the IP address dynamically.

![](img/b7e91b81e0d84c8a5261ee14a48991b2_142_1.png)

Your LAN can mix and match all kinds of computers — some may be running Linux and some may be running Microsoft Windows or any other operating system that supports TCP/IP. When configuring the network settings, remember to select the option that enables Linux to automatically obtain IP address settings and DNS information with DHCP.

## Extending Your LAN with a Wireless Network

If you have a laptop computer that you want to connect to your LAN — or if you don’t want to run a nest of wires to connect a PC to the LAN — you have the option of using a wireless Ethernet network. In a typical scenario, you have a cable modem or DSL connection to the Internet, and you want to connect one or more laptops with wireless network cards to access the Internet through the cable or DSL modem. In the following sections, I explain wireless networking and how to set it up on your network.

### Understanding Wireless Ethernet Networking

You’ve probably heard about Wi-Fi. Wi-Fi stands for *Wireless Fidelity* network — a short-range wireless network similar to the wired Ethernet networks. A number of standards from an organization known as IEEE (the Institute of Electrical and Electronics Engineers) defines the technical details of how Wi-Fi networks work. Manufacturers use these standards to build the components that you can buy to set up a wireless network, also known as WLAN for short.

Until mid-2003, there were two popular IEEE standards — 802.11a and 802.11b — for wireless Ethernet networks. These two standards were finalized in 1999. A third standard — 802.11g — was finalized by the IEEE in the summer of 2003. All these standards specify how the wireless Ethernet network works over the radio waves. You don’t have to fret over the details of these standards to set up a wireless network, but knowing some pertinent details is good so that you can buy the right kind of equipment for your wireless network.

The three wireless Ethernet standards have the following key characteristics:

- **802.11b:** Operates in the 2.4 GHz radio band (2.4 GHz to 2.4835 GHz) in up to three nonoverlapping frequency bands or channels. Supports a maximum bit rate of 11 Mbps per channel. One disadvantage of 802.11b is that the 2.4 GHz frequency band is crowded — many devices such as microwave ovens, cordless phones, medical and scientific equipment, as well as Bluetooth devices — all work within the 2.4 GHz frequency band. Nevertheless, 802.11b is very popular in corporate and home networks.
- **802.11a:** Operates in the 5 GHz radio band (5.725 GHz to 5.850 GHz) in up to eight nonoverlapping channels. Supports a maximum bit rate of 54 Mbps per channel. The 5 GHz band is not as crowded as the 2.4 GHz band, but the 5 GHz band is not approved for use in Europe. Products conforming to the 802.11a standard are available on the market, and wireless access points are designed to handle both 802.11a and 802.11b connections.
- **802.11g:** Supports up to 54 Mbps data rate in the 2.4 GHz band. (The same band that 802.11b uses.) 802.11g achieves the higher bit rate by using a technology called *OFDM* (Orthogonal frequency-division multiplexing), which is also used by 802.11a. Although 802.11g was only recently finalized, equipment that complies with it is already on the market. That’s because 802.11g has generated excitement by working in the same band as 802.11b but promising much higher data rates and by being backward-compatible with 802.11b devices. Vendors currently offer access points that can support both the 802.11b and 802.11g connection standards.

![](img/b7e91b81e0d84c8a5261ee14a48991b2_144_0.png)

There is a third standard — 802.11n — under development that would support 100-Mbps data rates in either the 2.4 GHz or the 5 GHz band, depending on which of the two proposals garner the required membership approval. Two equally matched groups of companies — known by the titles TGn Sync (Task Group n Synchronization) and WWiSE (Worldwide Spectrum Efficiency) — have each authored proposals for the 802.11n standard. TGn Sync proposes to use the 5 GHz band, the same one used by 802.11a, whereas WWiSE’s proposal is for the 2.4 GHz that’s used by 802.11b and g. Both groups agree that some form of multiple input multiple output (MIMO), pronounced “my-mo,” antenna technology would be needed to achieve the 100-Mbps data rate. (Some MIMO access points are already becoming available on the market.) At the May 2006 balloting, the TGn Sync proposal obtained the majority votes, but it did not receive the 75 percent votes required to be the basis for the first draft. You can read the latest news about the IEEE 802.11n project at grouper.ieee.org/groups/802/11/Reports/tgn_update.htm.

![](img/b7e91b81e0d84c8a5261ee14a48991b2_144_1.png)

If you are buying a new wireless access point, get an 802.11g one. An 802.11g access point can also communicate with older (and slower) 802.11b devices. You can also consider a MIMO access point that supports multiple 802.11 standards and implements techniques for getting higher throughputs and better range.

The maximum data throughput that a user actually sees is much less because all users of that radio channel share the capacity of the channel. Also, the data transfer rate decreases as the distance between the user’s PC and the wireless access point increases.

![](img/b7e91b81e0d84c8a5261ee14a48991b2_144_2.png)

To find out more about wireless Ethernet, visit www.wi-fi.org, the home page of the Wi-Fi Alliance — a nonprofit international association formed in 1999 to certify interoperability of wireless LAN products based on IEEE 802.11 standards.

### Understanding Infrastructure and Ad Hoc Modes

The 802.11 standard defines two modes of operation for wireless Ethernet networks: infrastructure and ad hoc. *Ad hoc mode* is simply two or more wireless Ethernet cards communicating with each other without an access point.

*Infrastructure mode* refers to the approach in which all the wireless Ethernet cards communicate with each other and with the wired LAN through an access point. For the discussions in this chapter, I assume that you set your wireless Ethernet card to infrastructure mode. In the configuration files, this mode is referred to as *managed mode*.

### Understanding Wired Equivalent Privacy (WEP)

The 802.11 standard includes Wired Equivalent Privacy (WEP) for protecting wireless communications from eavesdropping. WEP relies on a 40-bit or 104-bit secret key that is shared between a *mobile station* (such as a laptop with a wireless Ethernet card) and an *access point* (also called a base station). The secret key is used to encrypt data packets before they are transmitted, and an integrity check is performed to ensure that packets are not modified in transit. The 802.11 standard does not explain how the shared key is established. In practice, most wireless LANs use a single key that is shared between all mobile stations and access points. Such an approach, however, does not scale up very well to an environment such as a college campus because the keys are shared with all users — and you know how it is if you share a “secret” with hundreds of people. That’s why WEP is typically not used on large wireless networks such as the ones at universities. In such wireless networks, you have to use other security approaches such as SSH (Secure Shell) to log in to remote systems. WEP, however, is good to use on your home wireless network.

WEP has its weaknesses, but it’s better than nothing. You can use it in smaller wireless LANs where sharing the same key among all wireless stations is not an onerous task.

![](img/b7e91b81e0d84c8a5261ee14a48991b2_145_0.png)

Work is underway to provide better security than WEP for wireless networks. A standard called 802.11i is in the works that provides better security through public-key encryption. While the 802.11i standard is in progress, the Wi-Fi Alliance — a multivendor consortium that supports Wi-Fi — has developed an interim specification called *Wi-Fi Protected Access* (WPA) that’s a precursor to 802.11i. WPA replaces the existing WEP standard and improves security by making some changes. For example, unlike WEP (which uses fixed keys), the WPA standard uses something called the Temporal Key-Integrity Protocol (TKIP), which generates new keys for every 10K of data transmitted over the network. TKIP makes WPA more difficult to break. In 2004, the Wi-Fi Alliance introduced a follow-on to WPA called the *Wi-Fi Protected Access 2* (WPA2) — the second generation of WPA security. WPA2 is based on the final IEEE 802.11i standard, which uses public key encryption with digital certificates and an authentication, authorization, and accounting RADIUS (Remote Authentication Dial-In User Service) server to provide better security for wireless Ethernet networks. WPA2 uses the Advanced Encryption Standard (AES) for data encryption.
