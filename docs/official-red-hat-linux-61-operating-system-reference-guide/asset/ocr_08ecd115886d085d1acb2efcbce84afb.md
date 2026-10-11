# A.4 Ethernet parameters

Table A-5 Ethernet Module Parameters

| Hardware | Module | Parameters | 
|---|---|---|
| 3Com 3c501 | 3c501.o | 3c501=io_port,IRQ |
| 3Com 3c503 and 3c503/16 | 3c503.o | 3c503=io_port,IRQ 3c503 io=io_port_1,io_port_n irq=IRQ_1,IRQ_n |
| 3Com EtherLink Plus (3c505) | 3c505.o | 3c505=io_port,IRQ,DMA 3c505 io=io_port_1,io_port_n irq=IRQ_1,IRQ_2 dma=dma_1,dma_n |
| 3Com EtherLink 16 | 3c507.o | 3c507=io_port,IRQ 3c507 io=io_port irq=IRQ |
| 3Com EtherLink III | 3c509.o | 3c509=IRQ |
| 3Com ISA EtherLink XL "Corkscrew" | 3c515.o |  |
| 3Com EtherLink PCI III/XL Vortex (3c590, 3c592, 3c595, 3c597) Boomerang (3c900, 3c905, 3c595) | 3c59x.o |  |
| Apricot 680x0 VME, 82596 chipset | 82596.o | 82596=IRQ 82596 irq=IRQ |
| Ansel Communications AC3200 EISA | ac3200.o | ac3200=io_port,IRQ ac3200 io=io_port_1,io_port_n irq=IRQ_1,IRQ_n |