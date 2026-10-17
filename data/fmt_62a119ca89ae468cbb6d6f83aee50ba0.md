
# Red Hat Linux 6.0 安装指南

| 设备 | 模块 | 参数 |
|---|---|---|
| EtherWORKS DE425 TP/COAX EISA<br>DE434 TP PCI,<br>DE435/450 TP/COAX/AUI PCI<br>DE500 10/100 PCI<br>Kingston, LinkSys, SMC8432, SMC9332, Zynex31[45], 和 Zynex346 10/100 卡<br>带 DC21040 (无 SROM)、DC21041[A]、DC21140[A]、DC21142、DC21143 芯片组 | `de4x5.o` | `de4x5=io,port`<br>`de4x5 io=io_port`<br>`de4x5 args=ethX[tdx] autosense=MEDIA_STRING` |
| D-Link DE-600 以太网口袋适配器 | `de600.o` |  |
| D-Link DE-620 以太网口袋适配器 | `de620.o` | `de620 io=io_port irq=IRQ bnc=1 utp=1` |
| DIGITAL DEPCA & EtherWORKS<br>DEPCA, DE100, DE101,<br>DE200 Turbo, DE201 Turbo<br>DE202 Turbo TP/BNC, DE210, DE422 EISA | `depca.o` | `depca io=io_port,IRQ`<br>`depca io=io_port irq=IRQ` |
| Digi Intl. RightSwitch SE-X EISA 和 PCI | `dgrs.o` |  |
| Cabletron E2100 系列以太网卡 | `e2100.o` | `e2100 io=io_port,IRQ`<br>`e2100 io=io_port irq=IRQ` |
| Intel i82595 ISA<br>EtherExpressPro10/10+ 驱动 | `eepro.o` | `eepro io=io_port,IRQ,mem`<br>`eepro io=io_port irq=IRQ mem=mem` |
| Intel i82557/i82558 PCI<br>EtherExpressPro100 驱动 | `eepro100.o` |  |
| Intel EtherExpress 16 (82586) | `eexpress.o` | `eexpress io=io_port,IRQ`<br>`eexpress io=io_port irq=IRQ` |
| SMC EtherPower II 9432 PCI (83c170/175 EPIC 系列) | `epic100.o` |  |
| Racal-Interlan ES3210 EISA 网络适配器 | `es3210.o` | `es3210 io=io_port,IRQ,mem`<br>`es3210 io=io_port irq=IRQ mem=mem` |
| ICL EtherTeam 16/32 | `eth16i.o` | `eth16i io=io_port,mediatype`<br>`eth16i ioaddr=io_port mediatype=type` |
| EtherWORKS3 (DE203, DE204 和 DE205) | `ewrk3.o` | `ewrk3 io=io_port,IRQ`<br>`ewrk3 io=io_port irq=IRQ` |
| Fujitsu FMV-181/182/183/184 | `fmv18x.o` | `fmv18x io=io_port,IRQ`<br>`fmv18x io=io_port irq=IRQ` |
| Comtrol Hostess SV11 的模块化驱动 | `hostess_sv11.o` | `hostess_sv11 io=io_port,IRQ,DMABIT`<br>`hostess_sv11 io=io_port irq=IRQ dma=DMABIT` |
| HP PCLAN/plus | `hp-plus.o` | `hp-plus io=io_port,IRQ`<br>`hp-plus io=io_port irq=IRQ` |

## Red Hat Linux 6.0 安装指南

| 设备 | 模块 | 参数 |
|---|---|---|
| HP LAN 以太网 | `hp.o` | `hp_io=port,IRQ` |
|  |  | `hp_io=io_port,irq=IRQ` |
| 100VG-AnyLan 网络适配器 | `hp100.o` | `hp100_io=io_port,name` |
| HP J2585B, J2585A, J2970, J2973, J2573 |  | `hp100 hp100_port=io_port hp100_name=name` |
| Compex ReadyLink ENET 100-VG4, FreedomLine 100/VG |  |  |
| IBM Token Ring 16/4 | `ibmtr.o` | `ibmtr_io=io_port,IRQ,mem` |
|  |  | `ibmtr_io=io_port,irq=IRQ mem=mem` |
| AMD LANCE/PCnet | `lance.o` | `lance_io=io_port,IRQ,dma` |
| Allied Telesis AT1500, HP J2405A, NE2100, NE2500 |  | `lance_io=io_port,1_io_port,n_irq=IRQ,1_IRQ,2 dma=dma,1_dma,n` |
| Mylex LNE390 EISA 卡（LNE390A,LNE390B） | `lne390.o` | `lne390_io=io_port,IRQ,mem` |
|  |  | `lne390_io=io_port,irq=IRQ mem=mem` |
|  | `ltpco.o` | `ltpco_io=port,IRQ` |
|  |  | `ltpco_io=io_port,irq=IRQ` |
| NE1000 / NE2000（非 pci） | `ne.o` | `ne_io=io_port,IRQ` |
|  |  | `ne_io=io_port,irq=IRQ` |
| PCI NE2000 卡 | `ne2k-pci.o` |  |
| RealTEK RTL-8029, Winbond 89C940, Compex RL2000, KTI ET32P2, NetVin, NV5000SC, Via 82C926, SureCom NE34, Novell NE3210 EISA 网络适配器 | `ne3210.o` | `ne3210_io=io_port,IRQ,mem` |
|  |  | `ne3210_io=io_port,irq=IRQ mem=mem` |
| MiCom-Interlan NI5010 以太网卡 | `ni5010.o` | `ni5010_io=io_port,IRQ` |
|  |  | `ni5010_io=io_port,irq=IRQ` |
| NI5210 卡（82586 以太网芯片） | `ni52.o` | `ni52_io=io_port,IRQ` |
|  |  | `ni52_io=io_port,irq=IRQ` |
| NI6510, ni6510 EtherBlaster | `ni65.o` | `ni65_io=port,IRQ,dma` |
|  |  | `ni65_io=io_port,irq=IRQ dma=dma` |
| AMD PCnet32 和 AMD PCnetPCI | `pcnet32.o` |  |
| RedCreek Communications PCI | `rpcpci.o` |  |
| 使用 RTL8129 或 RTL8139 快速以太网芯片组的 RealTek 卡 | `rtl8139.o` |  |

## 附录 D：通用参数和模块

| 设备 | 模块 | 参数 |
|---|---|---|
| Sangoma S502/S508 多协议 FR | `sdla.o` |  |
| Sangoma S502A, ES502A, S502E, S503, S507, S508, S509 | `sdladrv.o` |  |
| SysKonnect Token Ring ISA/PCI 适配器、TR4/16(+) ISA 或 PCI、TR4/16 PCI 以及较旧的 SK NET TR4/16 ISA 卡 | `sktr.o` | `sktr=io_port,IRQ,mem`<br>`sktr io=io_port irq=IRQ mem=mem` |
| SMC Ultra 和 SMC EtherEZ ISA 以太网卡（8K, 83C790） | `smc-ultra.o` | `smc-ultra=io_port,IRQ`<br>`smc-ultra io=io_port irq=IRQ` |
| SMC Ultra32 EISA 以太网卡（32K） | `smc-ultra32.o` |  |
| SMC 9000 系列以太网卡 | `smc9194.o` | `smc9194=io_port,IRQ`<br>`smc9194 io=io_port irq=IRQ ifport=[0,1,2]` |
