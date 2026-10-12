
所有 NIS 数据库均由此文件覆盖。清单 14.11 包含来自 nsswitch.conf 文件的一个示例片段。

### LISTING 14.11 一个示例 /etc/nsswitch.conf 片段

```
hosts: nis dns files
networks: nis [NOTFOUND=return] files
```

第一个条目说明主机名查找首先传递给 NIS；如果 NIS 服务器无法找到匹配项，则查找随后传递给 DNS，最后将 /etc/hosts 文件用作最后手段。第二个条目说明网络名称使用 NIS 进行查找。[NOTFOUND=return] 表示对查找过程的精细控制。在这种情况下，如果查找工作正常（即 NIS 正在运行）但未找到名称（NOTFOUND），则查找应立即返回失败指示（=return）。这意味着只有在 NIS 宕机时才会检查 /etc/networks 文件。

## 摘要

在本章中，您已了解到网络对于现代计算机设施至关重要，并且 TCP/IP 是部署最广泛的网络系统。TCP/IP 允许使用多种物理介质类型，其中最常见的一种是 Ethernet。交换机可以减轻拥塞的 Ethernet 网络的负担，并可减少一些安全漏洞。

TCP/IP 使用 32 位 IP 地址来区分系统；这些地址具有可变长度的网络部分和主机部分。一个称为路由的过程使数据能够发送到正确的地址。静态配置的路由对于简单网络来说足够，但具有冗余路由的大型安装需要动态路由。UNIX 和 Linux 系统使用路由表来控制路由。routed 和 gated 守护进程通过操作此路由表执行动态路由。

TCP/IP 使用的数字地址对人类来说不方便。称为名称服务器的程序可以将符号化的、易于记忆的名称转换为数字地址。BIND（named 守护进程）是一个 Internet 域名服务器。NIS 提供全站名称查找服务，但不能对 Internet 主机执行相同的操作。

## 资源共享（打印和文件服务）

### 本章内容

- 网络就是关于共享 410
- 设置打印队列 411
- 网络文件服务 418
- Automount 守护进程和 Autofs 427

### 网络就是关于共享

网络计算机与独立系统之间的主要区别在于网络提供了在所有连接的计算机之间共享通用资源的机会。这使您可以降低个人工作站的成本，通过更小的磁盘空间需求、共享昂贵的资源例如激光打印机，并通过允许应用程序共享并为用户相互交互提供简单方式来降低管理成本。本章介绍几个具体的资源共享领域，即打印机和文件。首先提供 Linux 和 UNIX 系统共享资源的方式的概述，以及 Linux 如何与其他操作系统共享。然后介绍共享打印机和文件资源的某些具体细节。

### 与 Linux/UNIX 主机共享

Linux 就像 UNIX 一样，长期以来一直具有与同类系统共享资源的能力，这是这些操作系统的优势之一。Linux 下的网络打印机支持通过使用 Berkeley 行式打印机守护进程 lpd（随 Red Hat Linux 包含）或功能更强大的 LPRng 套件（您可以自行安装）来实现。LPRng 套件本文未描述；但是，如果您有兴趣了解其功能，可以访问 LPRng 主页 at http://www.astart.com/lprng/LPRng.html。此外，Linux 通过传统的网络文件系统 NFS 或诸如 Coda 和 AFS 之类的新型分布式文件系统支持与其他 Linux 和 UNIX 系统的文件共享。NFS 和 Coda 支持均包含在 Red Hat 提供的 Linux 内核中。AFS 系统是 Transarc 为您的 Linux 系统提供的商业产品，网址为 http://www.transarc.com/。

### 与其他操作系统共享

Linux 的优势之一是它不仅可以与其他 Linux 和 UNIX 系统共享资源，还可以与包括 Windows、NetWare 和 MacOS 在内的其他操作系统共享资源。这种共享可以采取两种形式之一。第一种是通过为这些其他操作系统提供的软件包来实现 Linux 原生的共享协议。这些软件包允许外来操作系统通过为运行在 Linux 系统上的打印机守护进程提供客户端来访问 NFS 文件系统并访问打印队列。另一种方法是 Linux 实现其他操作系统使用的协议。一个例子是使用 Samba 将您的 Linux 系统集成到 Windows 网络中。本主题在第 17 章“与 Windows NT 网络集成”中有更详细的介绍。另一个例子是 Linux 对 NetWare 或 AppleTalk 服务器的仿真，这也在第 17 章中介绍。

### 设置打印队列

考虑到激光打印机的成本，为网络上的每台工作站配备自己的打印机将是一项非常昂贵的提议。尤其是考虑到耗材成本，或如果需要提供彩色打印时更是如此。共享这些打印资源更有意义，这样您就不必在单独的打印机上花费巨资，而是可以用更少的钱获得打印资源的更多功能。

请考虑以下示例。您有一个由四台服务器和 25 台用户工作站组成的网络。其中三台工作站由市场部使用，需要彩色功能来制作营销材料。两台工作站由技术写作者使用，他们需要 PostScript 激光质量来打印产品手册的母版。其余 20 台具有正常的打印需求，从激光质量到简单的行式打印机不等。为了满足这些需求，您需要三台彩色激光打印机、两台 PostScript 激光打印机以及供其余工作站和服务器使用的 24 台标准打印机。按当前价格，仅打印机一项就可能花费您近两万美元。幸运的是，由于可以共享打印机资源，您可以大幅减少需求。共享使您可以使用一台彩色激光打印机供市场部使用，一台高速 PostScript 打印机供技术写作者使用，以及几台标准打印机，费用约为五千美元，这是如果打印机不可共享时的总成本的 25%。此外，维护成本和耗材成本也大大降低。

本节介绍在本地机器上设置打印机的步骤，如何向网络上的其他用户授予访问权限，以及如何配置没有打印机的系统以便跨网络打印。

### 设置本地打印机

在 Red Hat Linux 系统上设置打印机通常相当容易，前提是您有一台来自流行制造商且具有 GhostScript 驱动程序的打印机。GhostScript 是一个软件包，实现了 PostScript 语言，其中包含许多流行打印机的驱动程序。随 Red Hat Linux 6.0 安装提供的可用打印机驱动程序列表包含在表 15.1 中。

### 表 15.1 GhostScript 支持的打印机

| GhostScript 驱动程序 | 打印机名称 |
|---|---|
| djet500 | HP DeskJet 500 |
| cdj500 | HP DeskJet 400/500C/520/540C |
| cdj550 | HP DeskJet 550C/560C/6xxC series |
| pj | HP PaintJet |
| pjxl | HP PaintJet XL |
| pjx1300 | HP PaintJet XL300 and DeskJet 1200C |
| declj250 | DEC LJ250 (Alt) |
| dnj650c | HP DesignJet 650C |
| lj4dith | HP LaserJet 4—dithered |
| bjc600 | Canon BJC-600 and BJC-4000 |
| deskjet | HP DeskJet/DeskJet Plus |
| laserjet | HP LaserJet |
| laserjetplus | HP LaserJet Plus |
| ljet2p | HP LaserJet IID/IIP/III* with TIFF compression |
| ljet3 | HP LaserJet III* with Delta Row Compression |
| ljet3d | HP LaserJet III* with duplex capability |
| ljet4 | HP LaserJet 4/5/6 series |
| st800 | Epson Stylus 800 & ESC/P 2 printers |
| ap3250 | Epson AP3250 & ESC/P 2 printers |
| jetp3852 | IBM 3853 JetPrinter |
| r4081 | Ricoh 4081 laser printer |
| t4693d2 | Tek 4693d color printer, 2-bit mode |
| t4693d4 | Tek 4693d color printer, 4-bit mode |
| t4693d8 | Tek 4693d color printer, 8-bit mode |
| m8510 | C.Itoh M8510 |
| appledmp | Apple Dot Matrix |
| iwlo | Apple Imagewriter, low-resolution |
| iwhi | Apple Imagewriter, high-resolution |
| iwlq | Apple Imagewriter, letter quality |
| bj10e | Canon BJ-10e |
| bj200 | Canon BJ-100/200/210/240 |
| cp50 | Mitsubishi CP50 |
| epsonc | Epson Color Dot Matrix, 9 pin |
| epsonc | Epson Color Dot Matrix, 24 pin |
| epson | Epson Dot Matrix, 9 pin |
| epson | Epson Dot Matrix, 24 pin |
| eps9mid | Epson Dot Matrix, 9 pin, med-res |
| eps9high | Epson Dot Matrix, 9 pin, hi-res |
| imagen | Imagen ImPress |
| lbp8 | Canon LBP-8II |
| lips3 | Canon LIPS III |
