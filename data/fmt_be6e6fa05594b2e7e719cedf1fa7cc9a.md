
- 3Com 3C501, 3C503, 3C505, 3C507, 3C509/3C509B (ISA)/3C579 (EISA)

- AMD LANCE (7C960)/PCnet-ISA/PCI (AT1500, HP J2405a, NE1500/NE2100)

- AT&T WaveLAN; Allied Telesis AT1700

- Ansel Communications AC3200 EISA

- Cabletron E21xx

- DEC DE425 (EISA) / DE434/DE435 (PCI)

- DEC DEPCA 和 EtherWORKS

- HP PCLAN (2725 and 27xx 系列)

- HP PCLAN PLUS (27247B and 27252A)

- HP 10/100VG PCLAN (ISA/EISA/PCI)

- Intel EtherExpress; Intel EtherExpress Pro

- NE2000/NE1000 (然而并非所有克隆都是)

- New Media Ethernet

- Racal-Interlan NI5210 (8256 以太网芯片)

- Racal-Interlan NI6510 (atm99 芯片）（如果你的电脑内存超过 16MB，此板将无法工作）

- PureData DUC8028; SEEK 8005; SMC Ultra; Schneider & Koch G16

- Western Digital WD80x3;

- Zenith Z-Note ThinkPad 300 内置适配器。

此外，表 1.3 列出了从互联网下载并安装补丁后，Linux 将识别的多端口控制器。

| 控制器 | 互联网地址 |
| --- | --- |
| Comtl RocketPort (8/16/32 端口) | `ftp://tux-11.mit.edu/pub/linux/comtrl/` |
| DigiBord PC/Xe (ISA) 和 PC/XI (EISA) | `ftp://fpt.digib.com/drivers/linux/` |
| Moxa C218 (8 口) / C320 (8/16/24/32 可扩展) | `ftp://fpt.moxa.com.twl/drivers/c-218-320/linux/` |
| Specialix SIOXO (模块化, 4 到 32 口) | `ftp://sunsite.unc.edu/pub/Linux/kernel/patches/serial/sdrv0_5.tar` |

## 调制解调器

同样，如果调制解调器在 DOS 下可以工作，它在 Linux 下也应该工作——无论是内部还是外接。当你安装 Linux 时，你需要指定调制解调器的位置（串口 1、2、3 或 4）。PCMCIA 调制解调器也是如此。

你需要传真软件来利用传真调制解调器的功能。某些调制解调器需要特殊的程序：Digicom Connection 96+/14.4+ 需要一个 DSP 代码下载程序（可以在 `http://sunsite.unc.edu/pub/linux/system/Serial/smdl-linux.1.02.tar.gz` 找到），ZyXEL U-1496 系列需要 ZyXEL 1.4，一个调制解modem/传真/语音控制程序（可以在 `http://sunsite.unc.edu/pub/Linux/system/ZyXEL-1.4.tar.gz` 找到）。

### ISDN 卡

ISDN 卡属于直接连接到设备或标准调制解调器或网卡的替代品。如果你正在使用 ISDN 卡仿真调制解调器或网卡，你应该没有问题。然而，如果你正在使用 ISDN 连接互联网，你需要安装一些补丁。表 1.4 列出了 Linux 将识别的 ISDN 设备，随后是相应补丁的互联网地址。

### 表 1.4 ISDN 设备及其对应的补丁

如果你想获得更多关于使用 Linux 和 ISDN 设备的信息，请将你的 Web 浏览器指向 `http://www.ix.de/ix/linux/linux-isdn.html`。

### ATM 网络适配器

已经对 Efficient Networks ENI155P-MF 155 Mbps ATM 适配器进行了一些工作。你可以从 `http://lrc.epfl.ch/linux-atm/` 获取驱动程序和过程描述。

### 帧中继卡

针对 Sangoma S502 56K 帧中继卡的驱动程序已经完成了一些工作。你可以从 `ftp://ftp.sovereign.org/pub/wan/fr/` 获取副本。

### 其他设备

如今，很难买到一台没有配备一系列附加组件（如声卡和网卡）的 PC。在这一节中，我们将列举这些最受欢迎的附加组件和其他杂项组件。

### 声卡

Linux 支持多种声卡，包括：6850 UART MIDI (OPL2)；Audio Excel DSP16；Aztec Sound Galaxy NX Pro；基于 Crystal CS4232（即插即用）的卡；ECHO-POS 卡 (Orchid Wave32, Cardinal DSP16)；Ensoniq SoundScape；Gravis Ultrasound；Gravis Ultrasound 16 位采样子板；Gravis Ultrasound MAX；Logitech SoundMan Games (SBPro, 44kHz)

## 26 第1章：Linux 与 PC 硬件

GeniScan GS4500 携持式扫描仪 (`ftp://tsx-11.mit.edu/pub/linux/ALPHA/scanner/gs4500-1.3.tar.gz`), HP ScanJet 和 ScanJet Plus (`ftp://ftp-ctrl-c.liue.edu/unix/linux//`), HP ScanJet II 系列 SCSI (`ftp://sunsite.unc.edu/pub/linux/apps/graphics/scanners/hpscanpbm-0.3a.tar.gz`), HP ScanJet 家族（包括 ScanJet 3c） (`http://www.tummy.com/xvscan/`), Logitech 32/256扫描仪 (`ftp://tsx-11.mit.edu/pub/linux/ALPHA/scanner/logiscan-0.0.2.tar.gz`), Mustek M105 手持式扫描仪 GI1904 接口 (`ftp://tsx-11.mit.edu/pub/linux/ALPHA/scanner/driver-0.1.tar.gz`), Mustek Paragon 6000CX (`ftp://sunsite.unc.edu/pub/linux/apps/graphics/scanners/muscan-1.1.5.taz`), Nikon Coolscan CSCI 35mm 胶片扫描仪 (`ftp://sunsite.unc.edu/pub/linux/apps/graphics/scanners`)。

### 视频采集卡
