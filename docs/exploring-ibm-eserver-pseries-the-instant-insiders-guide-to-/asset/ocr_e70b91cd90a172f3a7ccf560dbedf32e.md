# pSeries Communications 253

![](bbox=[0.195, 0.098, 0.805, 0.318])

**Figure 4.5.** The basic structure of an Ethernet local area network.

supported over an Ethernet LAN. There are many Ethernet attachment options available for pSeries systems. In Chapter 2, eight Ethernet adapters are described (see Figure 2.13) in addition to the integrated Ethernet ports for pSeries systems.

With the availability of gigabit Ethernet adapters for fiber-optic connection and 100/100/1000 Mbps Ethernet adapters for UTP (copper) links, Ethernet is the primary technology for high-speed links among servers. Integrated 100/100/1000 Mbps Ethernet controllers, as available on the p65, will probably become standard in future pSeries designs, and there are dual-port Ethernet adapters that operate at gigabit speeds. The Ethernet options for pSeries servers enable many high-speed Ethernet connections with minimal use of I/O slots. To build complex, long-distance networks, these adapters must be integrated with networking products like hubs, switches, and routers. These are available from third-party suppliers such as Cisco Systems, whom IBM has recently announced an alliance to integrate IBM's system products and services with Cisco's leadership networking products for the Internet.

Figure 4.6 shows one possible wiring arrangement on a company's premises. This diagram could represent, for example, the intranet connections either the company or the supplier building of Figure 4.4. In Figure 4.6, various employees' PC workstations are connected to Ethernet hubs located in a wiring closet or communications room. We have shown some hubs supporting 10 Mbps on the input side and others supporting 100 Mbps input. It is possible, of course, for each PC