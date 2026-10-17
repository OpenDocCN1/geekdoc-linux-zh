
| D-Link (`www.dlink.com`) | |

# 附录 C CORE LINUX 硬件兼容性

| 制造商 | 硬件 |
|---|---|
| Fujitsu (`www.fujitsu.com`) | `D-Link DE6200` 适配器<br>`FMV-181, 182, 183, 184`<br>`EtherTeam 16/32 EISA` |
| Generic | `Cogent EM1110 NE1000, NE2000` (注意克隆版) |
| Hewlett-Packard (`www.hp.com`) | `PCLAN` (`27245` 和 `27xxx` 系列) `PCLAN Plus` (`27247B, 27252A`) `10/100VG PCLAN` |
| Intel (`www.intel.com`) | `EtherExpress` `EtherExpress Pro /10, EtherExpress Pro /100` |
| LSI Logic/SEEQ (`www.lsilogic.com`) | `SEEQ 8005 Apricot Xen-II /82596` |
| Mitsubishi (`www.mitsubishi.co.uk/computers/`) | `EISA L390A/B DM9102 PCI 以太网适配器` |
| Mylex (`www.mylex.com`) | `NE/2` (`ne2000 MCA`) `NE2000 MCA` |
| Not specific | `PCI Racal-Interlan (Micom)` `NI5010, NI5210, NI6510, EISA ES3210` |
| Not specific | `Realtek 8192/8139` |
| Not specific | `SIS 900/7016 PCI 以太网适配器` |
| Not specific | `SkNet MCA` |
| Not specific | `Ti Thunder Zenith ZNote (内置)` |
| Novell (`www.novell.com`) | `Novell/Eagle/Microdyne ME3210 EISA` |
| Standard Micro Corporation (`www.smc.com`) | `EtherPower II Ultra / EtherEZ (ISA)` |
| Via Technologies (Cyrix) (`www.cyrix.com`) | `Rhine` |
| Western Digital Corporation (`www.wdc.com`) | `Western Digital/SMC 9194` `Western Digital/SMC Ultra` `Western Digital/SMC Ultra 32 EISA` `Western Digital/SMC MCA` `Western Digital/SMC WD80x3` |

# 令牌环

Corel Linux 支持任何不使用 DMA 的 IBM 令牌环卡。

# 制造商

# 硬件

`IBM (www.ibm.com)`

`Madge Networks (www.madge.com/Madge.asp)`

`IBM Tropic 芯片组卡` `Madge TokenRing OCI 16/4 Mk2`

# PCMCIA

以下是关于 PCMCIA 设备兼容的一些说明：

- `SCSI` 要小心。许多厂商，特别是 CD-ROM 厂商，似乎会不同程度上切换控制器芯片。通常，它们会使用不同的产品代码，但例如，旧的（支持的）`New Media Bus Toaster` 卡与当前的基于 `Symbios` 卡难以区分，后者使用单独发布的 `sym5c500_cs` 驱动程序。

- `调制解器` 几乎所有现代调制解器、串口卡和数字蜂窝调制解器都支持。唯一的例外是 `Compaq 192`、`New Media WinSurfer`、`Motorola Montana`、`Megahertz XJ/CC256`、`3Com 3XCM356/3CCM356` 和 `3XCM656/3CCM656`、`Billionton 56K HSP`，以及需要特殊 `Windows` 驱动程序的所谓“`Winmodems`”。模拟标准 `UART` 的 `ISDN` 调制解器也受支持。

- `内存卡` 所有 `SRAM` 卡工作良好。不支持的闪存卡可以读取但不可写入。

- `CD-ROM` Corel Linux 不支持 PCMCIA CD-ROM 安装。安装后，PCMCIA CD-ROM 应该按预期工作。

- `ATA/IDE` 卡驱动器 大多数卡运行良好，包括外部 IDE 设备的适配器。系统支持闪存 ATA 设备和旋转介质卡，包括智能媒体闪存和紧凑卡。非常老的 `Western Digital 40MB` 驱动不支持，因为它们不符合 PCMCIA 规范。

以下是部分支持的 PCMCIA 卡。其余支持的 PCMCIA 卡按驱动列出。

# 制造商

# 硬件

`Aironet (www.aironet.com)`

`Cirrus (www.cirrus.com)`

`PC 4500, PC 4800` (`airo-cs` 驱动)

`PD67xx`

# 附录 C 核心 Linux 硬件兼容性

| 制造商 | 硬件 |
|---|---|
| Databook (`www.fortezza.com/db.soft.html`) | `DB8608x` |
| Digital Mobile Media | `SCSI II 适配器` |
| Intel (`www.intel.com`) | `82092AA 182365SSL` (使用 `i82365.o` 模块) |
| I-O Data Device Inc. (`www.iodata.com`) | `CDG-PX44/PCSC CD-ROM` `PCSC-II, PCSC-II-L` |
| Logitech (`www.logitech.com`) | `LPM-SCSI2 LCD-601 CD-ROM` |
| Melco | `IFC-SC2, IFC-DC` |
| New Media Corporation (`www.newmediacorp.com`) | `EthernetLAN, New Media LiveWire` (`nmclan_cs` 驱动) |
| O2Micro (`www.o2micro.com`) | `OZ67x` |
| Omega Micro (`www.fsbond.com/omegamicro/omegamic.htm`) | `82Cx` |
| Pioneer (`www.pioneer.co.jp/index-e.html`) | `PCP-PR1W, PCP-PR2W CD-ROM` |
| Ricoh (`www.ricoh-usa.com`) | `RF5Cx, RL5cx` |
| Taxan (`www.taxan.co.uk`) | `ICD-400PN` |
| Texas Instruments (`www.ti.com`) | `PCIx` |
| Toshiba (`www.toshiba.com`) | `ToPICx` |
| Vadem (`www.vadem.com`) | `VG4x` |
| Via Technologies (Cyrix) (`www.cyrix.com`) | `VT83C69` |
| VLSI Technologies (`www.vlsi.com`) | `VCF94365` |

# 带有 3c574_cs, 3c575_cs 和 3c589_cs 驱动的 PCMCIA 卡

| 制造商 | 硬件 |
|---|---|
| `3c574_cs` 驱动 | `3C574TX` |
| `3Com Corporation` (`www.3com.com`) | `3CCFE54BT 3CXFE574BT` `Megahertz 3CCFEM5566B` |
| `3c575_cs` 驱动<br>`3Com Corporation` (`www.3com.com`) | `3C575TX`<br>`3CCFE575BT`<br>`3CCFE575CT`<br>`3CXFE575CT`<br>`3CCFEM656B` (仅限以太网) |
| `3c589_cs` 驱动<br>`3Com Corporation` (`www.3com.com`) | `Megahertz 3CCEM556`<br>`Megahertz 3CCEM556B`<br>`Megahertz 3CXEM556`<br>`3C562/B/C/D`<br>`3C563B/C/D`<br>`3C589`<br>`3C589/B/C/D`<br>`3CCE589E`<br>`3CXE589D`<br>`3CXE589EC` |

- `Farallon` (`www.farallon.com`) - `EtherWave`

- `Motorola` (`www.motorola.com`) - `Motorola Marquis`

# 带有 aha152x_cs 和 apa1480_cb 驱动的 PCMCIA 卡

| 制造商 | 硬件 |
| --- | --- |
| `aha152x_cs` 驱动<br>`Adaptec` (`www.adaptec.com`) | `APA-1450A`<br>`APA-1460`<br>`APA-1460A/B/C/D` `SlimSCSI` |
