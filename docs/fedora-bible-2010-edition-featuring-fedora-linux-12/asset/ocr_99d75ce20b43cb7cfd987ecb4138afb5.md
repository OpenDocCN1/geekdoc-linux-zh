wireless card. A project called Madwifi (http://madwifi-project.org/) has additional Linux wireless drivers, created specifically for wireless LAN cards that use chipsets from Atheros (www.atheros.com). Select Compatibility List from the Madwifi Wiki (http://madwifi-project.org/wiki/Compatibility) to see supported wireless cards.

+   * **Windows driver** — In cases where no native Linux driver is available, it’s sometimes possible to use an open source driver called ndiswrapper along with the Windows driver to use a wireless card in Linux. To see which cards are supported by ndiswrapper, refer to the list of ndiswrapper-supported cards. Go to the NDISwrapper project page (http://ndiswrapper.sourceforge.net/). Note that some aspects of this project have become quite controversial. You may need to look in the Internet Archive to find information. Go to web.archive.org and search for NDISwrapper to see the old list of supported cards.

Table 14-1 shows a list of network cards that have Linux-specific open source drivers included with Fedora.

> **NOTE:** It’s possible that even if your wireless card isn’t listed in Table 14-1 that it might still work with drivers included with Fedora. Some wireless cards that include the same chipset (and therefore work with the same driver) may be referred to by different names. Rather than try to keep track of all the various acquisitions and name changes in the wireless industry, I refer you to the Linux Wireless LAN HOWTO (www.hpl.hp.com/personal/Jean_Tourrilhes/Linux). The Drivers section provides more insight into which drivers work with which cards.

Table 14-1: Supported Wireless Network Adapters and Modules

| Wireless Network Adapter | Module |
| :--- | :--- |
| 350 Series Wireless LAN Adapter (Ciscko Systems) | airo_cs.ko |
| ADMtec ADM8211 wireless | adm8211.ko |
| Aironet PC4500 (Ciscko Systems) | airo_cs.ko |
| Aironet PC4800 (Ciscko Systems) | airo_cs.ko |
| 8388 USB WLAN Driver | Usb8xxx.ko |
| ADMtec ADM8211 | adm8211.ko |
| Atheros 802.11 and 802.11n wireless | ath5k.ko, ath9k.ko |
| Atmel AT76C50X wireless | atmel_cs.ko |
| Atmel AT76x wireless (USB version) | at76c50x-usb.ko |
| Atmel AT76C50X wireless (PCI version) | atmel_pci.ko |
| Compaq WL100 11 Mbps Wireless Adapter | orinoco_cs.ko |
| Intel PRO/Wireless 2100 Network Connection mini PCI | ipw2100.ko |