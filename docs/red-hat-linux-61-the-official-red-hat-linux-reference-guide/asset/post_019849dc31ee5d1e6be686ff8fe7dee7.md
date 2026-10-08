
# Hardware

## Appendix A. General Parameters and Modules

| Hardware | Module | Parameters |
|---|---|--|
| Qlogic 2x00 | gla2x00.o | |
| Qlogic Fast SCSI FASXXX ISA/VLB/PCMCIA | qlogicfas.o | |
| Qlogic ISP21100 SCSI-FCP | qlogicfc.o | |
| Qlogic ISP10200 Intelligent SCSI cards IQ-PCI, IQ-PCI10, IQ-PCI-D | qlogicisp.o | |
| Qlogic ISP10200 SCSI SBUS | qlogicpti.o | |
| Future Domain TMC-88S, TMC-950 Seagate ST-01/02, Future Domain TMC-8xx | seagate.o | controller_type=2 base_address=base_addr irq=IRQ |
| Cards with the sym53c416 chipset | sym53c416.o | sym53c416 io=PORTBASE, [IRQ] OR sym53c416 io=PORTBASE irq=IRQ |
| Trantor T128/T12F/T223 SCSI Host Adapter | t128.o | |
| Tekram DC-390(T) PCI | tmcsim.o | |
| UltraStor 14F/34F (not 24F) | ul14-34f.o | |
| UltraStor 14E, 24F, and 34F WD7000 Series | wd7000.o | |

Table A-3. SCSI Parameters

Here are some examples of these modules in use:

| Configuration | Example |
|---|---|---|
| Adaptec AHA1522 at port 330, IRQ 11, SCSI ID 7 | aha152x=0x330,11,7 |
| Adaptec AHA1542 at port 330 | bases=0x330 |
| Future Domain TMC-800 at CA000, IRQ 10 | controller_type=2 base_address=0xca00 irq=10 |

Table A-4. SCSI Parameters Configuration Examples

### A.4. Ethernet Parameters

> Important
> Most modern Ethernet-based network interface cards (NICs), do not require module parameters to alter settings. Instead, they can be configured using ethtool or mii-tool. Only these tools fail to work should module parameters be adjusted.

For information about using these tools, consult the man pages for ethtool and mii-tool.

| Hardware | Module | Parameters |
| --- | --- | --- |
| 3Com 3c501 | 3c501.o | 3c501=io_port, IRQ |
| 3Com 3c503 and 3c503/16 | 3c503.o | 3c503=io_port, IRQ OR 3c503 io=io_port_1,io_port_n irq=IRQ_1,IRQ_n |
| 3Com EtherLink Plus (3c505) | 3c505.o | 3c505=io_port, IRQ OR 3c505 io=io_port_1,io_port_n irq=IRQ_1,IRQ_2 |
| 3Com EtherLink 16 | 3c507.o | 3c507=io_port, IRQ OR 3c507 io=io_port_irq=IRQ |
| 3Com EtherLink III | 3c509.o | 3c509=io_port, IRQ |
| 3Com ISA EtherLink XL "Corkscrew" | 3c515.o | |
| 3Com EtherLink PCI III/XL Vertex (3c590, 3c592, 3c595, 3c597) Boomerang (3c900, 3c905, 3c595) | 3c59x.o | full_duplex=j is on |
| RTL8139, SMC EZ Card Fast Ethernet | 8139too.o | |
| RealTek cards using RTL8129 or RTL8139 Fast Ethernet chipsets | 8139too.o | |
| Apricot 82596 | 82596.o | |
| Ansel Communications Model 3200 | ac3200.o | ac3200=io_port, IRQ OR ac3200 io=io_port_1,io_port_n irq=IRQ_1,IRQ_n |
| Alteon AceNIC Gigabit Aironet Arlan 655 | acenic.o | |
| Allied Telesis AT1700 | at1700.o | at1700=io_port, IRQ OR at1700 io=io_port irq=IRQ |
| Broadcom BCM5700 10/100/1000 ethernet adapter | bcm5700.o | |
| Crystal Semiconductor CS89[02]0 | cs89x0.o | |
| Hardware | Module | Parameters |
| --- | --- | --- |
| EtherWORKS DE425 TP/COAX EISA, DE434 TP PCI, DE435/450 TP/COAX/UI PCI DE500 10/100 PCI Kingston, LinkSys, SMC8432, SMC9332, Znyx31[45], and Znyx36 10/100 cards with DC21040 (no SROM), DC21041[A], DC21140[A], DC21142, DC21143 chipsets | de4x5.0 | de4x5=io_port OR de4x5=io_port de4x5='ethX[fdx] autosense=MEDIA_STRING' |
| D-Link DE-600 Ethernet Pocket Adapter | de600.0 | |
| D-Link DE-620 Ethernet Pocket Adapter | de620.0 | |
| DIGITAL DEPCA & EtherWORKS DE100, DE201 Turbo, DE202 TP/BNC, DE210, DE422 | depca.0 | depca=io_port.IRQ OR depca io=io_port irq=IRQ |
| Intl. RightSwitch-X EISA and PCI | dgrs.0 | |
| Davicom DM9102(A)/DM9132/DM9801 Fast Ethernet | dmfe.0 | |
| Intel Express/100 | e100.0 | e100_speed_duplex=X 0=autodetect and duplex 1=100Mbps, half duplex 2=100Mbps, full duplex 3=100Mbps, half duplex 4=100Mbps, full duplex |
| Intel EtherExpress/1000 Gigabit | e1000.0 | |
| Cabletron E2100 | e2100.o | e2100=io_port, IRQ, mem OR e2100 io=io_port mem |
| Intel EtherExpress Pro10 | eepro.o | eepro=io_port,IRQ OR eepro io=io_port irq=IRQ |
| Intel EtherExpress i8257/i8258 | eepro100.o | |

| Hardware | Module | Parameters |
| --- | --- | --- |
| Intel EtherExpress 16 (i8256) | eexpress.o | eexpress=io_port,IRQ OR eexpress io=io_port,irq=0x10 10base T half duplex 0x20 10base T full duplex 0x100 10base T full duplex |
| SMC EtherPower II 9432 (83c170/175) | epic100.o | |
| Racal-Inter ES3210 | es3210.o | es3210.o |
| ICL Ether-Team 16i/32 | eth16i.o | eth16i=io_port,IRQ OR eth16 io=io_port |
| EtherWorks 3 (DE203, DE204 and DE205) | ewrk3.o | ewrk=io_port,IRQ OR ewrk io=io_port,irq |
| Packet Enginet-II | hamachi.o | |
| HP PLAN/plus | hp-plus.o | hp-plus=io_port,IRQ OR hp-plus io=io_port irq=IRQ |
| HP LAN | hp.o | hp=io_port,IRQ OR hp=io_port irq=IRQ |
| Network Adapters HP2585, J2585, J2970, J2973 | hp100.o | hp100=io_port.name OR hp100_port=io_port hp100_name |
| Freedom/100/VG | lance.0 | |
| DEC 10 PCI(DE450) EtherWorks 100/10 PCI(DE550-XA) DEC EtherWorks 10 PCI(DE450) Zyx 312 etheray QSILVER'S | | io=io_port |
| Allied Telesis LA100PCI-T Danpex EN-9400, Cogent EM110 | |
| VIA Rhine PCI Fast Ethernet cards with either the VIA VT86c100A Rhine-II PCI or 3043 Rhine-I D-Link DFE-930-TX PCI 10/100 | via-rhine.o | |
| AT&T GIS (nee NCR) WaveLan ISA Card | wavelen.o | wavel={IRQ,0],io_port, NWID |

| Hardware | Module | Parameters |
|---|---|--|
| WD8003 and WD8013-compatible Ethernet cards | wd.o | wd=io_port,IRQ,mem,mem_end OR wd=io_port irq=IRQ mem=mem mem_end=end |
| Compex RL1000ATX-PCI | winbind.o | |
| Packet Engines Yellowfin | yellowfin.o | |

Table A-5. Ethernet Module Parameters

Here are some examples of these modules in use:

| Configuration | Example |
|---|---|---|
| NE2000 ISA card at IO address 300 and IRQ 11 | ne=0x300,11 ether=0x300,11,eth0 |
| Wavelan card at IO 390, autprobe for IRQ, and use the NWID to 0x4321 | wavelan=0x390,0x4321 ether=0x390,0x4321,eth0

Table A-6. Ethernet Parameter Configuration Examples

| Hardware | Module | Parameters |
|---|---|--|
| MiCom-Interlan NI5010 | ni5010.o | |
| NI5210 card (i8256 Ethernet card) | ni52. | ni52=io_port,IRQ OR ni52_io_port irq=IRQ |
| NI6510 Ethernet | ni650.o | |
| IBM Olympic-based PCI token ring | olympic.o | |
| AMD PCnet32 and AMD PCnetPCI | pcnet32.o | |
| SIS 900/701G PCI Fast Ethernet | sis900.o | |
| SysKconnect SK-98XX Gigabit | sk98lin.o | |
| SMC Ultra and SMC EtherEz EISA earthcard (8K, 83c790) | smc-ultra.o | smc-ultra=io_port,IRQ OR smc-ultra io=io_port irq=IRQ |
| SMC Ultra32 EISA Ethernet card (32K) | smc-ultra32.o | |
| Sun BigMac Ethernet | sunbmac.o | |
| Sundance ST201 Alta | sundance.o | |
| Sun Happy Meal Ethernet | sunhme.o | |
| Sun Quad Ethernet | sunqe.o | |
| ThunderLAN | tlan.o | |
| Digital 21x44 Tulip Ethernet cards SMC EtherPower 10 PCI(84327/8432BT) SMC EtherPower 10/100 PCI(9332DST) DEC EtherWorks 100/10 PCI(DE550-XA) DEC EtherWorks 10 PCI(DE450) DEC QSILVER'S, Znyx 312 etheray Allied Telesis LA100PCI-T Danpex EN-9400, Cogent EM110 | | io=io_port |
| Novell NE3210 EISA | ne3210.o | |

### A.4.1. Using Multiple Ethernet Cards

You can use multiple Ethernet cards in one machine. If each card uses a different driver (for example, a 3c509 and a DE425, add alias (and possibly options) lines for each card to /etc/modules.conf. Refer to the chapter titled Kernel Modules in the Red Linux Customization Guide for more information.

If two Ethernet cards use the same driver (such as two 3c509 cards or a 3c595 and a 3c905), either give the two card addresses on the driver's options line (for ISA cards) or simply add one alias line for each card (for PCI cards).

For additional information about more than one Ethernet card, see the Linux Ethernet-HOWTO at http://www.redhat.com/mirrors/LDP/HOWTO/Ethernet-HOWTO.html.
