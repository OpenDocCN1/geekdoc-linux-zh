
- 8MB RAM
- 80MB 磁盘空间
- 486 CPU
- 8MB RAM
- 80MB 磁盘空间
- 486 CPU
- 8MB RAM
- 80MB 磁盘空间
- 486 CPU
- 8MB RAM
- 80MB 磁盘空间
- 486 CPU
- 8MB RAM
- 80MB 磁盘空间
- 486 CPU
- 8MB RAM
- 80MB 磁盘空间
- 486 CPU
- 8MB RAM
- 80MB 磁盘空间
- 486 CPU
- 8MB RAM
- 80MB 磁盘空间
- 486 CPU
- 8MB RAM
- 80MB 磁盘空间
- 486 CPU
- 8MB RAM
- 80MB 磁盘空间
- 486 CPU
- 8MB RAM
- 80MB 磁盘空间
- 486 CPU
- 8MB RAM
- 80MB 磁盘空间
- 486 CPU
- 8MB RAM
- 80MB 磁盘空间
- 486 CPU
- 8MB RAM
- 80MB 磁盘空间
- 486 CPU
- 8MB RAM
- 80MB 磁盘空间
- 486 CPU
- 8MB RAM
- 80MB 磁盘空间
- 486 CPU
- 8MB RAM
- 80MB 磁盘空间
- 486 CPU
- 8MB RAM
- 80MB 磁盘空间
- 486 CPU
- 8MB RAM
- 80MB 磁盘空间
- 486 CPU
- 8MB RAM
- 80MB 磁盘空间
- 486 CPU
- 8MB RAM
- 80MB 磁盘空间
- 486 CPU
- 8MB RAM
- 80MB 磁盘空间
- 486 CPU
- 8MB RAM
- 80MB 磁盘空间
- 486 CPU
- 8MB RAM
- 80MB 磁盘空间
- 486 CPU
- 8MB RAM
- 80MB 磁盘空间
- 486 CPU
- 8MB RAM
- 80MB 磁盘空间
- 486 CPU
- 8MB RAM
- 80MB 磁盘空间
- 486 CPU
- 8MB RAM
- 80MB 磁盘空间
- 486 CPU
- 8MB RAM
- 80MB 磁盘空间
- 486 CPU
- 8MB RAM
- 80MB 磁盘空间
- 486 CPU
- 8MB RAM
- 80MB 磁盘空间
- 486 CPU
- 8MB RAM
- 80MB 磁盘空间
- 486 CPU
- 8MB RAM
- 80MB 磁盘空间
- 486 CPU
- 8MB RAM
- 80MB 磁盘空间
- 486 CPU
- 8MB RAM
- 80MB 磁盘空间
- 486 CPU
- 8MB RAM
- 80MB 磁盘空间
- 486 CPU
- 8MB RAM
- 80MB 磁盘空间
- 486 CPU
- 8MB RAM
- 80MB 磁盘空间
- 486 CPU
- 8MB RAM
- 80MB 磁盘空间
- 486 CPU
- 8MB RAM
- 80MB 磁盘空间
- 486 CPU
- 8MB RAM
- 80MB 磁盘空间
- 486 CPU
- 8MB RAM
- 80MB 磁盘空间
- 486 CPU
- 8MB RAM
- 80MB 磁盘空间
- 486 CPU
- 8MB RAM
- 80MB 磁盘空间
- 486 CPU
- 8MB RAM
- 80MB 磁盘空间
- 486 CPU
- 8MB RAM
- 80MB 磁盘空间
- 486 CPU
- 8MB RAM
- 80MB 磁盘空间
- 486 CPU
- 8MB RAM
- 80MB 磁盘空间
- 486 CPU
- 8MB RAM
- 80MB 磁盘空间
- 486 CPU
- 8MB RAM
- 80MB 磁盘空间
- 486 CPU
- 8MB RAM
- 80MB 磁盘空间
- 486 CPU
- 8MB RAM
- 80MB 磁盘空间
- 486 CPU
- 8MB RAM
- 80MB 磁盘空间
- 486 CPU
- 8MB RAM
- 80MB 磁盘空间
- 486 CPU
- 8MB RAM
- 80MB-

# SymBIOS(亦 NCR):

53C810, 53C810a, 53C815, 53C820, 53C825a, 53C860, 53C875, 53C875j, 53C885 和 53C896 PCI SCSI 控制器，包括 ASUS SC-200；Data Technology DTC3130（所有变体）；Diamond FreePort（所有）；NCR 适配卡（所有）；SymBIOS 适配卡（所有）；Tekram DC390W, 390U 和 390F；以及 Tyan S1365

# QLogic:

1020, 1240, 2100 和 2200 系列 SCSI 和光纤网

FreeBSD 支持 SCSI-I 和 SCSI-II 设备。然而，FreeBSD 自带的驱动仅以只读模式支持 CD-RW 和 WORM 设备。要获取这些设备的写入权限，请从 FreeBSD ports 树安装 `deisdisc`。

# 光学（CD-ROM/DVD）驱动器

- 任何符合 ATAPI 标准的驱动器
- 基于 SCSI 的驱动器
- 松下/Panasonic (Creative Labs SoundBlaster) 专用驱动器 (562/563 型)
- 所有 Sony 专用驱动器

# 网卡

本节列出了 FreeBSD 支持的网络适配器。请注意，许多通用网卡以及许多内置网络适配器都会使用这些芯片组之一。因此，如果你在这里没有找到你的特定网卡，可以查询它使用的是什么芯片组。例如，许多通用网卡具有兼容 NE 2000 的芯片组，而许多内置适配器使用 Intel EtherExpress 芯片组——两者都被 FreeBSD 支持。

# Adptec:

基于 Adaptec AIC-6195 Fast以太网控制器芯片的 Duralink PCI Fast以太网适配器，包括：
- ANA-62011 64位单端口 10/100BaseTX 适配器
- ANA-62022 64位双端口 10/100BaseTX 适配器
- ANA-62044 64位四端口 10/100BaseTX 适配器
- ANA-69011 32位单端口 10/100BaseTX 适配器
- ANA-62020 64位单端口 100BaseFX 适配器

# Allied-Telesyn:

AT1700 和 RE2000

# Alteon Networks:

基于 Tigon 1 和 Tigon 2 芯片组的 Alteon Networks PCI 千兆以太网网卡，包括 Alteon AceNIC (Tigon 1 和 2)、3Com 3c985-SX (Tigon 1 和 2)、Netgear GA620 (Tigon 2)、Silicon Graphics 千兆以太网、DEC/Compaq EtherWORKS 1000 以及 Dec 千兆以太网

# AMD:

PCnet/PCI (79C97x 系列和 53C974 或 79C94)

# RealTek:

8129/8139 Fast以太网网卡，包括：
- Allied-Telesyn AT2550
- Allied-Telesyn AT2500TX
- Genius GF100TXXR (RTL8139)
- NDC Communications NE1000TX-E
- OvisLink LEE-8129TX
- OvisLink LEE-8139TX
- Netronix IC. EA-1210 NetEther 10/100
- KTX-9130TX 10/100 Fast以太网
- Accton “Cheetah” EN1207D (MPX 5030/5038; RealTek 8139 隆隆)
- SMC EZ Card 10/100 PCI 1211-TX

# Lite-On:

98713, 98713A, 98715 和 98725 Fast以太网网卡，包括：
- LinkSys EtherFast LNE100TX
- NetGear FA310-TX Rev. D1
- Matrox FastNIC 10/100
- Kingston KNE110TX

# Macronix:

98713, 98713A, 98715, 98715A 和 98725 Fast以太网网卡，包括：
- NDC Communications SFA100A (98713A)
- CNet Pro120A (98713 或 98713A)
- CNet Pro120B (98715)
- SVEC PN102TX (98713)

# Macronix/Lite-On:

PNIC IC LC82C115 Fast以太网网卡，包括 LinkSys EtherFast LNE100TX，版本 2
