

## ATA/IDE CD-ROM 适配器

你至少应使用内核 1.3.72。

- Argosy EIDE CD-ROM (ide_cs)
- Caravelle CD-36N (ide_cs)
- CNF CARDport CD-ROM (ide_cs)
- Creative Technology CD-ROM (ide_cs)
- Digital Mobile Media CD-ROM (ide_cs)
- EXP CD940 CD-ROM (ide_cs)（部分可用，部分不可用）
- EXP Traveler 620 CD-ROM (ide_cs)
- H45 Technologies Quick 2x CD-ROM (ide_cs)
- H45 Technologies QuickCD 16X (ide_cs)
- IBM Max 20X CD-ROM (ide_cs)
- IO DATA CDP-TX4/PCIDE、CDP-TX6/PCIDE、CDV-HDN6/PCIDE (ide_cs)
- IO DATA CDP-TX10/PCIDE、CDP-FX24/CBIDE、MOP-230/PCIDE (ide_cs)
- IO DATA HDP-1G/PCIDE、HDP-1.6G/PCIDE (ide_cs)
- Microtech International MicroCD (ide_cs)
- Microtech Mii Zip 100 (ide_cs)
- NOVAC NV-CD410 (ide_cs)
- Sony PCGA-CD5 CD-ROM (ide_cs)
- TEAC IDE Card/II (ide_cs)

## 多功能卡

你至少应使用内核 1.3.73。

- 3Com 3c562、3c562B/C/D、3c563B/C/D (3c589_cs)
- 3Com Megahertz 3CCEM556、3CXEM556、3CCEM556B (3c589_cs)
- 3Com Megahertz 3CCFEM556 (3c574_cs)
- 3Com 3CCFEM556B (3c575_cb，仅以太网！！)
- Accton UE2218 (pcnet_cs)
- ActionTec ComNet 33.6 (pcnet_cs)
- AnyCom 快速以太网 + 56K 组合卡 (pcnet_cs)
- 华硕组合卡 (pcnet_cs)
- Billionton LMSL7-10B (pcnet_cs)
- Compaq Microcom CPQ550 调制解调器 + 10/100 LAN (xirc2ps_cs)
- Dayna Communicard (pcnet_cs)
- D-Link DME336T、DMF560TX (pcnet_cs)
- Gateway Telepath Combo (smc91c92_cs)
- Grey Cell GCS3400 (pcnet_cs)
- GVC LAN 调制解调器 (pcnet_cs)
- IBM Home and Away、Home and Away 28.8 (pcnet_cs)
- IO DATA PCMCIA-336T (pcnet_cs)
- Intel EtherExpress PRO/100 LAN/调制解调器 (xirc2ps_cs)
- Linksys LANmodem 28.8 (PCMLM28)、33.6 (PCMLM336) (pcnet_cs)
- Linksys EtherFast LANmodem 56K (PCMLM56) (pcnet_cs)
- Megahertz/U.S. Robotics EM1144、EM3288、EM3336 (smc91c92_cs)
- Motorola Mariner (smc91c92_cs)
- Motorola Marquis (3c589_cs)
- Ositech Jack of Diamonds、Jack of Hearts (smc91c92_cs)
- Ositech Jack of Spades CardBus (epic_cb，实验性，需要内核 2.2.x 或更高版本)
- PREMAX LAN 调制解调器 (pcnet_cs)
- Psion V.34 Gold Card (pcnet_cs)
- Psion Gold Card Netglobal 56K+10Mb (pcnet_cs)
- Rover ComboCard 33.6 (pcnet_cs)
- TDK 3000/3400/5670 (pcnet_cs)
- Telecom Device SuperSocket LM336 (pcnet_cs)
- Xircom CreditCard CEM28、CEM33、CEM56 (xirc2ps_cs)
- Xircom RealPort REM10BT、REM56G-100 (xirc2ps_cs)
- Xircom RBEM56G-100BTX、CEM56G-100BTX (tulip_cb，实验性，需要内核 2.2.x 或更高版本)

## ATA/IDE 卡式驱动器

这些卡式驱动器从内核 1.3.72 开始受到支持。Flash-ATA 卡和旋转介质卡均受支持。非常老式的 Western Digital 40MB 驱动器不受支持，因为它们不符合 PCMCIA ATA 规范。

## ATA/IDE 接口卡

- Archos Zip100 MiniDrive (ide_cs)
- Microtech International XpressDock (ide_cs)
- DataStor Technology PCMCIA ATA/ATAPI Card (ide_cs)
- Creo DNBoy (ide_cs)
- GREYSTONE DD-25 (ide_cs)
- Shining Technology CitiDISK 250PE (ide_cs)
- Sicon Peripheral Micro Mate (ide_cs)

## 并口卡

请参阅关于受支持的并口设备的附录。

## 其他杂项卡

- GemPlus GPR400 智能卡读卡器 http://www.linuxnet.com/smartcard/code.html (Wolf Geldmacher wgeldmacher@...)
- IBM Smart Capture (iscc_cs)（Koji Okamura oka@ec.kyushu-u.ac.jp）
- IBM 以太网 (cs89x0_cs)（Danilo Beuche danilo@cs.uni-magdeburg.de）
- National Instruments DAQcard700 ftp://ftp.rtlinux.org/pub/rtlinux/sources/DAQcard700/ (Oleg Subbotin)
- Netwave AirSurfer Plus (asplus_cs) http://ipoint.vlsi.uiuc.edu/wireless/asplus.html (Jay Moorman jmoorma@uiuc.edu)
- New Media Bus Toaster SCSI（新版本）(sym53c500_cs)（Tim Corner tcorner@via.at）
- New Media BASICS SCSI (sym53c500_cs)（Tim Corner tcorner@via.at）
- Nokia/InTalk ST-500A http://www.absoval.com/linux-wlan（Mark Mathews mark@absoval.com）
- Proxim RangeLAN2 和 Symphony 无线 LAN 卡 http://www.komacke.com/distribution.html（Dave Koberstein davek@komacke.com）
- RATOC REX-9590 (iscc_cs)（Koji Okamura oka@nanotsu.kobe-u.ac.jp）
- Samsung MagicWave SWL-1000N http://www.absoval.com/linux-wlan（Mark Mathews mark@absoval.com）
- Silicom SPE 以太网、SEM EtherModem、SES EtherSerial http://www.silicom.co.il/linux.htm
- SIMA TECH SCSI9000 (sym53c500_cs)（Tim Corner tcorner@via.at）
- SST 5136-DN-PC DeviceNet 接口 (ss5136_cs) http://www.gnofn.org/~marksu/ss5136man.html
- Trimble Mobile GPS（使用串口/调制解调器驱动）
- Y-E Data FlashBuster 软驱适配器 (floppy_cs)（David Bateman dbateman@eng.uts.edu.au）
- Zoom Telephonics ZoomAir 4000 http://www.absoval.com/linux-wlan（Mark Mathews mark@absoval.com）

## 正在开发中……

以下卡片的支持正在开发中：

- Roland SC-55 MIDI（Toshiyuki Nakatsu ir9k-nkt@asahi.net.or.jp）
- CyberRom CD-ROM（David Rowntree rowntree@dircon.co.uk）
- IO DATA PCSC-II（Katayama Nobuhiro kata-n@po.iijnet.or.jp）
- Macnica mPS-1x0（Katayama Nobuhiro kata-n@po.iijnet.or.jp）
- Proxim RangeLAN/2 http://students.ou.edu/D/James.R.Duchek-1/rangelan2.htm（Jim Duchek jimduchek@primary.net）
- TView Prose（Brenden Tuck friar@zendragon.com）

## 不支持的设备

- Adaptec/Trantor APA-460 SlimSCSI
- Eiger Labs SCSI（FCC ID K36..）
- New Media WAVjammer 及所有其他声卡
- New Media LiveWire+
- Nikon CoolPix100
- Panasonic KXL-D720、KXL-D745、KXL-D783
- SMC 8016 EliteCard
- Xircom CE II 以太网/调制解调器
- Xircom CE-10BT 以太网

## 受支持的并口设备

并口正越来越多地被用于连接打印机以外的设备。为了支持这种用法，人们编写了相应的并口驱动程序，使这些设备能够正常工作。本节列出了已编写并口支持的设备。

需要说明的是：本附录没有列入打印机，因为这些并口支持项目不支持打印机。

更多信息请查看 Linux 并口支持页面 http://www.torque.net/parport。在那里你可以找到：

- 用于并口 IDE 设备的 Paride 子系统（http://www.torque.net/parport/paride.html）
- 并口 SCSI 设备的支持（http://www.torque.net/parport/psscsi.html）

### 以太网

- Accton EtherPocket 适配器
- AT-Lan-Tec/RealTek 并口以太网适配器
- D-Link DE600/DE620 并口以太网适配器

### 硬盘

- H45 Quick HD
- KingByte IDE/ATAPI 磁盘
- KT Technologies HD 便携式硬盘
- MicroSolutions backpack 硬盘
- SyQuest EZ-135
- SyQuest EZ-230
- SyQuest SparQ
- ValueStor 外置硬盘

### 磁带机

- Hewlett-Packard Colorado Tracker 250 磁带机（T1000e 除外）
- Hewlett-Packard HP Colorado 5GB 磁带机
- Iomega Ditto 磁带机
- MicroSolutions backpack 8000t、8000td 磁带机

### CD-ROM 驱动器

- Freecom Power CD
- Freecom Traveller CD-ROM
- H45 Quick CD
- Hewlett-Packard HP 7100e/7200e CD-R
- KingByte IDE/ATAPI CD-ROM
- MicroSolutions backpack CD-ROM。并口驱动器支持 163550 及之后的型号。对于 160550 和 162550 型号，可提供单独的驱动程序。
- MicroSolutions backpack PD/CD 驱动器
- SyQuest SyJet

### 可移动驱动器

- Avatar Shark 250
- Imation Superdisk
- Iomega ZIP、ZIP Plus 驱动器

### IDE 适配器

- Arista ParaDrive 系列产品
- DataStor Commuter 磁盘
- Fidelity International Technologies TransDisk 系列产品
- Freecom IQ Cable Parallel
- Shuttle Technology EPAT/EP EZ 并口 IDE 适配器
- Shuttle Technology EPIA 并口 IDE 适配器

### SCSI 适配器

- Adaptec APA-348 mini-SCSI plus 适配器线缆
  - 驱动程序可从 `http://www.torque.net/parport/parscsi.html` 获取
- Adaptec APA-358 mini-SCSI EPP 适配器线缆
  - 驱动程序可从 `http://www.torque.net/parport/parscsi.html` 获取
- Shuttle Technology EPSA-2 并口 SCSI 适配器
  - 驱动程序可从 `http://www.torque.net/parport/parscsi.html` 获取
- Shuttle Technology EPST 并口 SCSI 适配器
  - 驱动程序可从 `http://www.torque.net/parport/parscsi.html` 获取

### 数码相机

- Connectix QuickCam

### PCMCIA 并口卡

parport_cs 驱动程序需要内核 2.2.x 或更高版本。

- Quatech SPP-100
- IOtech DBK35、WBK20A

## 即插即用设备

如果你在让即插即用设备正常工作时遇到困难，可以使用 Peter Fox 编写的 ISA PnP 工具。以下内容引自 README：

```
These programs allow ISA Plug-And-Play devices to be configured
on a Linux machine.

This program is suitable for all systems, whether or not they
include a PnP BIOS.
```

