# Appendix A. General Parameters and Modules

267

| Hardware | Module | Parameters |
| --- | --- | --- |
| 3Com 3c501 | 3c501.o | 3c501=io_port, IRQ |
| 3Com 3c503 and 3c503/16 | 3c503.o | 3c503=io_port, IRQ OR 3c503 io=io_port_1,io_port_n irq=IRQ_1,IRQ_n |
| 3Com EtherLink Plus (3c505) | 3c505.o | 3c505=io_port, IRQ OR 3c505 io=io_port_1,io_port_n irq=IRQ_1,IRQ_2 |
| 3Com EtherLink 16 | 3c507.o | 3c507=io_port, IRQ OR 3c507 io=io_port_irq=IRQ |
| 3Com EtherLink III | 3c509.o | 3c509=io_port, IRQ |
| 3Com ISA EtherLink XL "Corkscrew" | 3c515.o | |
| 3Com EtherLink PCI III/XL Vertex (3c590, 3c592, 3c595, 3c597) Boomerang (3c900, 3c905, 3c595) | 3c59x.o | full_duplex= j is on |
| RTL8139, SMC EZ Card Fast Ethernet | 8139too.o | |
| RealTek cards using RTL8129 or RTL8139 Fast Ethernet chipsets | 8139too.o | |
| Apricot 82596 | 82596.o | |
| Ansel Communications Model 3200 | ac3200.o | ac3200=io_port, IRQ OR ac3200 io=io_port_1,io_port_n irq=IRQ_1,IRQ_n |
| Alteon AceNIC Gigabit Aironet Arlan 655 | acenic.o | |
| Allied Telesis AT1700 | at1700.o | at1700=io_port, IRQ OR at1700 io=io_port irq=IRQ |
| Broadcom BCM5700 10/100/1000 ethernet adapter | bcm5700.o | |
| Crystal SemiconductorCS89[02]0 | cs89x0.o | |