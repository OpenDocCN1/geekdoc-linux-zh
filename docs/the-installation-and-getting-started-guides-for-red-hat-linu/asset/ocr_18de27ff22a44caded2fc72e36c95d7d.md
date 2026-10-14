# The Installation Guide for Red Hat Linux 6.0

|  |  |  |
|---|---|---|
| HP LAN Ethernet | hp.o | hp_io=port,IRQ |
|  |  | hp_io=io_port,irq=IRQ |
| 100VG-AnyLan Network Adapters | hp100.o | hp100_io=io_port,name |
| HP J2585B, J2585A, J2970, J2973, J2573 |  | hp100 hp100_port=io_port hp100_name=name |
| Compex ReadyLink ENET 100-VG4, |  |  |
| FreedomLine 100/VG |  |  |
| IBM Token Ring 16/4 | ibmtr.o | ibmtr_io=io_port,IRQ,mem |
|  |  | ibmtr_io=io_port,irq=IRQ mem=mem |
| AMD LANCE/PCnet | lance.o | lance_io=io_port,IRQ,dma |
| Allied Telesis AT1500, HP J2405A, |  |  |
| NE2100, NE2500 |  | lance_io=io_port,1_io_port,n_irq=IRQ,1_IRQ,2 |
|  |  | dma=dma,1_dma,n |
| Mylex LNE390 EISA cards (LNE390A,LNE390B) | lne390.o | lne390_io=io_port,IRQ,mem |
|  |  | lne390_io=io_port,irq=IRQ mem=mem |
|  | ltpco.o | ltpco_io=port,IRQ |
|  |  | ltpco_io=io_port,irq=IRQ |
| NE1000 / NE2000 (non-pci) | ne.o | ne_io=io_port,IRQ |
|  |  | ne_io=io_port,irq=IRQ |
| PCI NE2000 cards | ne2k-pci.o |  |
| RealTEK RTL-8029, Winbond 89C940, |  |  |
| Compex RL2000, KTI ET32P2, NetVin, |  |  |
| NV5000SC, Via 82C926, SureCom NE34, |  |  |
| Novell NE3210 EISA Network Adapter | ne3210.o | ne3210_io=io_port,IRQ,mem |
|  |  | ne3210_io=io_port,irq=IRQ mem=mem |
| MiCom-Interlan NI5010 ethercard | ni5010.o | ni5010_io=io_port,IRQ |
|  |  | ni5010_io=io_port,irq=IRQ |
| NI5210 card (82586 Ethernet chip) | ni52.o | ni52_io=io_port,IRQ |
|  |  | ni52_io=io_port,irq=IRQ |
| NI6510, ni6510 EtherBlaster | ni65.o | ni65_io=port,IRQ,dma |
|  |  | ni65_io=io_port,irq=IRQ dma=dma |
| AMD PCnet32 and AMD PCnetPCI | pcnet32.o |  |
| RedCreek Communications PCI | rpcpci.o |  |
| ReaTek cards using RTL8129 | rtl8139.o |  |
| or RTL8139 Fast Ethernet chipsets |  |  |