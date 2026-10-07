# Options and Peripherals 169

and various physical connections. Cable options are available for configuring the system for the particular network in which the pseries is attached. These multiprotocol adapters are part of the AIX Realtime Interface Coprocessors (ARTIC) family of adapters designed to remove the burden of communications traffic from the pseries by handling the detailed processing associated with communications links and nonstandard device interfaces.

The IBM AIX960Hx 4-Port Multiprotocol PCI Adapter (#2947) provides four ports for EIA-232, EIA-530, RS-449, X.21, or V.35. Each port can support speeds up to 2 Mbps. Using the appropriate software support provided with AIX, this adapter provides SDLC, bisync, or X.25 packet-switched communications capability. The adapter requires one full-length 32-bit PCI slot.

The 2-port Multiprotocol PCI Adapter (#2962) provides high-speed connections between standalone systems on a WAN, connected via external communications equipment such as Service Units (CSUs), Data Service Units (DSUs), and synchronous mediums. Using the appropriate cable, the 2-Port Multiprotocol PCI Adapter connects to X.25 packet-switched networks compatible with X.21 DCE (Distributed Computing Environment) Cable (X.21, #2954), with V.24 DCE (2-Port Cable, V.24/EIA-232, #2951), with V.35 DCE (2-Port Cable, V.35, and V.36 DCE (2-Port Cable, V.36/EIA-449, #2953).

# Other Communications Options

In this section, we will cover several communications options for pSeries systems that don't fit neatly into the other categories.

# S/390 ESCON Channel PCI Adapter

The S/390 ESCON Channel PCI Adapter (#2751) allows a pSeries system to be attached to IBM's larger System/390 (such as an ES/9000) computer systems via an Enterprise Systems CONection (ESCON) channel. These channels are fiber-optic links introduced with the System/390 architecture. When a pSeries system is attached to a System/390 computer via an ESCON channel, information can be exchanged between the two systems at up to 17 Mbps. This communications link can allow a pSeries system to provide a gateway between the computers in