Before Agere Systems was spun off as a separate company, Orinoco cards were referred to as WaveLAN cards and were produced by Lucent Technologies (as well as AT&T and NCR).

Other wireless cards supported in Red Hat Linux are listed in the PCMCIA Card Configuration Database file (/etc/pcmcia/config). Table 15-2 shows the wireless-network adapters listed in this file, along with the module required by each.

> **NOTE:** Just because you don't see your wireless card listed in Table 15-2 doesn't mean that it won't work. The same technology is often referred to by different names. Rather than try to keep track of all the various acquisitions and name-changes in the wireless industry, I refer you to the Linux Wireless LAN HOWTO (http://www.hpl.hp.com/personal/Jean_Tourrilhes/Linux). The Drivers section provides more insight into which drivers work with which cards.

# Table 15-2: Supported Wireless Network Adapters and Modules

| Wireless Network Adapter | Module |
| :--- | :--- |
| 350 Series Wireless LAN Adapter (Cisco Systems) | airo_cs |
| Aironet PC4500 (Cisco Systems) | airo_cs |
| Aironet PC4800 (Cisco Systems) | airo_cs |
| AT&T WaveLAN Adapter | wavelan_cs |
| Cabletron RoamAbout 802.11 DS | wlan_cs |
| Compaq WL100 11 Mbps Wireless Adapter | orinoco_cs |
| Digital RoamAbout/DS | wavelan_cs |
| ELSA AirLancer MC-11 | wlan_cs |
| Lucent Technologies WaveLAN Adapter | wavelan_cs |
| Intersil PRISM2 11 Mbps Wireless Adapter | wlan_cs |
| Lucent Technologies WaveLAN/IEEE Adapter | wlan_cs |
| MELCO WLI-PCM-L11 | wlan_cs |
| NCR WaveLAN Adapter | wavelan_cs |
| NCR WaveLAN/IEEE Adapter | wlan_cs |
| Orinoco PC Cards (Agere Systems) | orinoco_cs |
| RayLink PC Card WLAN Adapter | ray_cs |
| Xircom CreditCard Netwave | netwave_cs |

The Orinoco PC cards I purchased use the wlan_cs module. The cards come in two types: Gold Label, which offers 128-bit WEP RC4 encryption, and Silver Label, which offers only 64-bit WEP RC4 encryption. The two cards differ in cost by about $10. Both cards: