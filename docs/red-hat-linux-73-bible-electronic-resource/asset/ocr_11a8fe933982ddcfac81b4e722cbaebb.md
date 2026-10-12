+   * offer compatibility with earlier WaveLAN/IEEE products.
+   * can communicate with other 802.11b wireless LAN equipment that has been Wi-Fi-certified by WECA.
+   * enable you to select transmission rates (11, 5.5, 2, or 1-Mbps), select channels (in the 2.4 GHz range), and use power-management features.

Because antennas are built into Orinoco PC cards, you may not need an additional antenna for indoor office environments. As with any wireless card, the distances you can achieve between your wireless nodes depend on transmission rate (lower speeds go farther), receiver sensitivity, and the amount and type of obstacles. At the maximum transmission rate (11 Mbps), the Orinoco card gives you an estimated range of between 80 feet (25 meters) in a closed area and 525 feet (160 meters) in an open area with no additional antenna.

# ## Selecting adapter cards

If the computers on your wireless network are all laptops with PCMCIA slots, you only need to plug in your wireless cards to get started. However, if you are using a desktop computer with only ISA and PCI slots, you will also need an adapter card.

Before you purchase a wireless LAN card for your desktop computer, make sure that you can get a compatible adapter card. Agere Systems offers both ISA and PCI Orinoco adapter cards. If you have an ISA slot available, you should get an ISA adapter. In fact, Agere Systems strongly recommends the ISA adapter if you have a choice between ISA and PCI. The ISA card supports the following I/O addresses: 3E2-3E1 (default) and 3E2-3E3.

The PCI adapter works on computers that have the following features:

+   * PCI 2.2 (or higher) BIOS support
+   * PC99 compliance
+   * PCI slots only

The PCI adapter will not work on some older computers that don't meet the BIOS specifications. To use the PCI adapter in Linux, you may have to perform additional configuration in the operating system.

> **NOTE:** Although using the Orinoco ISA and PCI adapters with a standard Type II PC is not specifically supported, many Type II PC cards (besides your wireless cards) will work in those adapters.

# ## Selecting antennas

If you are setting up your wireless LAN among several computers in close proximity to each other, you may not need an additional antenna. To deal with obstructions and longer distances, however, you can add indoor or outdoor antennas to your wireless hardware.