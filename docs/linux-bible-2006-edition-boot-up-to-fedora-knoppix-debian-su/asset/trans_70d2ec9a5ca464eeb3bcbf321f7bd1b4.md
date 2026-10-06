

# 第 12 章 ♦ 运行 Yellow Dog Linux

◆ Anaconda 安装程序 — Yellow Dog 利用了经过充分测试的 Anaconda 安装器来实现轻松安装。

◆ Kudzu 硬件检测 — Yellow Dog 从用于检测和配置硬件的 Fedora Core kudzuset开始，这为探测设备提供了稳定的基础，该功能已扩展到 Mac 硬件。

有关 Fedora Core 项目及其某些实现细节的更多信息，请参阅第 8 章。

![](img/a2d958d7eab32ca5b89b2b8af808aa70_398_0.png)

# 安装 Yellow Dog Linux

在安装 Yellow Dog Linux 之前，你需要从许多可用资源中获取它的副本。第一种最推荐的方法是从供应商处购买。这具有双重效果：既从源源获取，又能支持创建 Yellow Dog Linux 的公司，使其继续为 PowerPC 平台开发。

要从 Terra Soft Solutions 购买 Yellow Dog Linux，请访问 Terra Soft 网上：http://terrasoftolutions.com/store/。从 Terra Soft Solutions 购买时，你将在一个套装中收到以下内容：

- 四张 CD 和源码 CD。

- 《Yellow Dog Linux 入门》，这书涵盖了初级 Yellow Dog 用户运行完全操作的 Yellow Dog 系统所需的所有信息。

- 可选的 60 天安装支持（你可以根据自己的需求和对 Linux 的技能水平购买带支持或不带支持的套装）。

- 其他小礼物（贴纸、灵活传单，取决于购买的软件包）。

- 你正在支持创建该产品的公司，从而允许进一步开发的知识。

购买 Yellow Dog Linux 套装的替代方案包括：

- 购买 YDL.net 订阅 — 这是 Terra Soft Solutions 为 Yellow Dog 用户提供的在线资源。你可以获得电子邮件帐户和 Web 空间，还能在 Yellow Dog Linux 最新版本正式发布之前获得其预发布访问权限。费用取决于你选择的版本。更多信息请参阅 www.ydl.net。

- 下载并创建你自己的 ISO — 你可以从 http://yellowdoglinux.com/resources/ftp_mirrors.shtml 中列出的众多 Linux 镜像站之一下载发行版，并刻录你的 ISO。

# 368 第三部分 ♦ 选择与安装 Linux 发行版

## 硬件支持

Linux 系统的硬件支持在过去是一个主要问题，但随着 Linux 流行性的增加，许多设备制造商已经提供了其硬件驱动程序的访问权限，或者在某些情况下为 Linux 创建了硬件驱动程序。虽然这对于 X86 社区中的全新硬件仍然是一个问题，但在 PowerPC 平台上影响被减轻了，因为硬件通常按照 Apple 严苛的标准制造。Terra Soft Solutions 专注于 Apple 硬件，通常硬件变体较少，这使得 PowerPC 平台的支持更快。

Yellow Dog Linux 的伟大之处之一是，当你深入研究它时，会发现 X86 Linux 面临的一些硬件问题（例如 Winmods 问题、众多的硬件配置等）被降至最低或消除了。通过获得授权的 Apple 增值经销商 Terra Soft Solutions，你可以确保你正在使用的硬件将获得支持。YDL 4.0 和 4.1 发布时在原生硬件支持上存在差异，但功能完备的 3.0.1 版本涵盖了 4.0.x 系列的所有空白。

除了可以在自己的 Apple 硬件上安装 Yellow Dog Linux 之外，你还可以从 Terra Soft Solutions 购买预装 Yellow Dog Linux 的 Apple 硬件。

Terra Soft Solutions 开发了专门针对 Yellow Dog Linux 测试过的硬件配置官方列表（http://yellowdoglinux.com/support/hardware/breakdown/index.php）。Yellow Dog 4.0.1 包括：

- Power Mac G3 (Yosemite Blue and White 300–400 MHz G3)
- Power Mac G4 (Power Mac G4 PCI 350–400 MHz G4 及以上)
- Power Mac G5 (1.6 GHz G5 及以上)
- Mac Mini
- iMac (Rev A,B 233 MHz G3, eMac G4, 和 iMac G5)
- PowerBook (Lombard 300–400 MHz G3, Pismo 400–500 MHz FW G3, Titanium 400–1 MHz G4, Powerbook 12" 867 MHz–1.33 GHz, 以及 Powerbook 15–17 1.0–1.5 GHz G4)
- iBook (300–366 MHz G3—800 MHz 1.2 GHz G4)
- HPC (Xserver Cluster Node 1 1.33 MHz G4, Single/Dual 1.33 MHz G4, Cluster Node 2 2.0 GHz G5, 以及 Single/Dual 2.0 GHz G5)

# 第 12 章 ♦ 运行 Yellow Dog Linux

Yellow Dog Linux 4.0 和 4.0.1 支持的硬件中明显缺失的是 Old World ROM 或米色 G3 及以下硬件，如 8500s、7200s 和 Performa PowerWCs。YDL 3.0.1 支持这种硬件以及 Yellow Dog Linux 4.0.1 目前支持的大多数硬件。Yellow Dog Linux 4.0.1 支持并测试的硬件包括：

- Power Mac G3 (Yosemite Blue and White 300–400 MHz G3)
- Power Mac G4 (Power Mac G4 PCI 350–400 MHz G4 及以上)
- Power Mac G5 (1.6 GHz G5 及以上)
- Mac Mini
- iMac (Rev A,B 233 MHz G3, eMac G4, 和 iMac G5)
- PowerBook (Lombard 300–400 MHz G3, Pismo 400–500 MHz FW G3, Titanium 400–1 MHz G4, Powerbook 12" 867 MHz–1.33 GHz, 以及 Powerbook 15–17 1.0–1.5 GHz G4)
- iBook (300–366 MHz G3—800 MHz 1.2 GHz G4)
- HPC (Xserver Cluster Node 1 1.33 MHz G4, Single/Dual 1.33 MHz G4, Cluster Node 2 2.0 GHz G5, 以及 Single/Dual 2.0 GHz G5)

Yellow Dog Linux 4.0 和 4.0.1 支持的硬件中明显缺失的是 Old World ROM 或米色 G3 及以下硬件，如 8500s、7200s 和 Performa PowerWCs。YDL 3.0.1 支持这种硬件以及 Yellow Dog Linux 4.0.1 目前支持的大多数硬件。Yellow Dog Linux 4.0.1 支持并测试的硬件包括：

- Old World ROM 或米色 G3 及以下硬件，如 8500s、7200s 和 Performa PowerWCs。
- Power Mac G3 (Yosemite Blue and White 300–400 MHz G3)
- Power Mac G4 (Power Mac G4 PCI 350–400 MHz G4 及以上)
- Power Mac G5 (1.6 GHz G5 及以上)
- Mac Mini
- iMac (Rev A,B 233 MHz G3, eMac G4, 和 iMac G5)
- PowerBook (Lombard 300–400 MHz G3, Pismo 400–500 MHz FW G3, Titanium 400–1 MHz G4, Powerbook 12" 867 MHz–1.33 GHz, 以及 Powerbook 15–17 1.0–1.5 GHz G4)
- iBook (300–366 MHz G3—800 MHz 1.2 GHz G4)
- HPC (Xserver Cluster Node 1 1.33 MHz G4, Single/Dual 1.33 MHz G4, Cluster Node 2 2.0 GHz G5, 以及 Single/Dual 2.0 GHz G5)

Yellow Dog Linux 4.0 和 4.0.1 支持的硬件中明显缺失的是 Old World ROM 或米色 G3 及以下硬件，如 8500s、7200s 和 Performa PowerWCs。YDL 3.0.1 支持这种硬件以及 Yellow Dog Linux 4.0.1 目前支持的大多数硬件。Yellow Dog Linux 4.0.1 支持并测试的硬件包括：

- Old World ROM 或米色 G3 及以下硬件，如 8500s、7200s 和 Performa PowerWCs。
- Power Mac G3 (Yosemite Blue and White 300–400 MHz G3)
- Power Mac G4 (Power Mac G4 PCI 350–400 MHz G4 及以上)
- Power Mac G5 (1.6 GHz G5 及以上)
- Mac Mini
- iMac (Rev A,B 233 MHz G3, eMac G4, 和 iMac G5)
- PowerBook (Lombard 300–400 MHz G3, Pismo 400–500 MHz FW G3, Titanium 400–1 MHz G4, Powerbook 12" 867 MHz–1.33 GHz, 以及 Powerbook 15–17 1.0–1.5 GHz G4)
- iBook (300–366 MHz G3—800 MHz 1.2 GHz G4)
- HPC (Xserver Cluster Node 1 1.33 MHz G4, Single/Dual 1.33 MHz G4, Cluster Node 2 2.0 GHz G5, 以及 Single/Dual 2.0 GHz G5)

Yellow Dog Linux 4.0 和 4.0.1 支持的硬件中明显缺失的是 Old World ROM 或米色 G3 及以下硬件，如 8500s、7200s 和 Performa PowerWCs。YDL 3.0.1 支持这种硬件以及 Yellow Dog Linux 4.0.1 目前支持的大多数硬件。Yellow Dog Linux 4.0.1 支持并测试的硬件包括：

- Power Mac G3 (Yosemite Blue and White 300–400 MHz G3)
- Power Mac G4 (Power Mac G4 PCI 350–400 MHz G4 及以上)
- Power Mac G5 (1.6 GHz G5 及以上)
- Mac Mini
- iMac (Rev A,B 233 MHz G3, eMac G4, 和 iMac G5)
- PowerBook (Lombard 300–400 MHz G3, Pismo 400–500 MHz FW G3, Titanium 400–1 MHz G4, Powerbook 12" 867 MHz–1.33 GHz, 以及 Powerbook 15–17 1.0–1.5 GHz G4)
- iBook (300–366 MHz G3—800 MHz 1.2 GHz G4)
- HPC (Xserver Cluster Node 1 1.33 MHz G4, Single/Dual 1.33 MHz G4, Cluster Node 2 2.0 GHz G5, 以及 Single/Dual 2.0 GHz G5)

Yellow Dog Linux 4.0 和 4.0.1 支持的硬件中明显缺失的是 Old World ROM 或米色 G3 及以下硬件，如 8500s、7200s 和 Performa PowerWCs。YDL 3.0.1 支持这种硬件以及 Yellow Dog Linux 4.0.1 目前支持的大多数硬件。Yellow Dog Linux 4.0.1 支持并测试的硬件包括：

- Power Mac G3 (Yosemite Blue and White 300–400 MHz G3)
- Power Mac G4 (Power Mac G4 PCI 350–400 MHz G4 及以上)
- Power Mac G5 (1.6 GHz G5 及以上)
- Mac Mini
- iMac (Rev A,B 233 MHz G3, eMac G4, 和 iMac G5)
- PowerBook (Lombard 300–400 MHz G3, Pismo 400–500 MHz FW G3, Titanium 400–1 MHz G4, Powerbook 12" 867 MHz–1.33 GHz, 以及 Powerbook 15–17 1.0–1.5 GHz G4)
- iBook (300–366 MHz G3—800 MHz 1.2 GHz G4)
- HPC (Xserver Cluster Node 1 1.33 MHz G4, Single/Dual 1.33 MHz G4, Cluster Node 2 2.0 GHz G5, 以及 Single/Dual 2.0 GHz G5)

Yellow Dog Linux 4.0 和 4.0.1 支持的硬件中明显缺失的是 Old World ROM 或米色 G3 及以下硬件，如 8500s、7200s 和 Performa PowerWCs。YDL 3.0.1 支持这种硬件以及 Yellow Dog Linux 4.0.1 目前支持的大多数硬件。Yellow Dog Linux 4.0.1 支持并测试的硬件包括：

- Power Mac G3 (Yosemite Blue and White 300–400 MHz G3)
- Power Mac G4 (Power Mac G4 PCI 350–400 MHz G4 及以上)
- Power Mac G5 (1.6 GHz G5 及以上)
- Mac Mini
- iMac (Rev A,B 233 MHz G3, eMac G4, 和 iMac G5)
- PowerBook (Lombard 300–400 MHz G3, Pismo 400–500 MHz FW G3, Titanium 400–1 MHz G4, Powerbook 12" 867 MHz–1.33 GHz, 以及 Powerbook 15–17 1.0–1.5 GHz G4)
- iBook (300–366 MHz G3—800 MHz 1.2 GHz G4)
- HPC (Xserver Cluster Node 1 1.33 MHz G4, Single/Dual 1.33 MHz G4, Cluster Node 2 2.0 GHz G5, 以及 Single/Dual 2.0 GHz G5)

Yellow Dog Linux 4.0 和 4.0.1 支持的硬件中明显缺失的是 Old World ROM 或米色 G3 及以下硬件，如 8500s、7200s 和 Performa PowerWCs。YDL 3.0.1 支持这种硬件以及 Yellow Dog Linux 4.0.1 目前支持的大多数硬件。Yellow Dog Linux 4.0.1 支持并测试的硬件包括：

- Power Mac G3 (Yosemite Blue and White 300–400 MHz G3)
- Power Mac G4 (Power Mac G4 PCI 350–400 MHz G4 及以上)
- Power Mac G5 (1.6 GHz G5 及以上)
- Mac Mini
- iMac (Rev A,B 233 MHz G3, eMac G4, 和 iMac G5)
- PowerBook (Lombard 300–400 MHz G3, Pismo 400–500 MHz FW G3, Titanium 400–1 MHz G4, Powerbook 12" 867 MHz–1.33 GHz, 以及 Powerbook 15–17 1.0–1.5 GHz G4)
- iBook (300–366 MHz G3—800 MHz 1.2 GHz G4)
- HPC (Xserver Cluster Node 1 1.33 MHz G4, Single/Dual 1.33 MHz G4, Cluster Node 2 2.0 GHz G5, 以及 Single/Dual 2.0 GHz G5)

Yellow Dog Linux 4.0 和 4.0.1 支持的硬件中明显缺失的是 Old World ROM 或米色 G3 及以下硬件，如 8500s、7200s 和 Performa PowerWCs。YDL 3.0.1 支持这种硬件以及 Yellow Dog Linux 4.0.1 目前支持的大多数硬件。Yellow Dog Linux 4.0.1 支持并测试的硬件包括：

- Power Mac G3 (Yosemite Blue and White 300–400 MHz G3)
- Power Mac G4 (Power Mac G4 PCI 350–400 MHz G4 及以上)
- Power Mac G5 (1.6 GHz G5 及以上)
- Mac Mini
- iMac (Rev A,B 233 MHz G3, eMac G4, 和 iMac G5)
- PowerBook (Lombard 300–400 MHz G3, Pismo 400–500 MHz FW G3, Titanium 400–1 MHz G4, Powerbook 12" 867 MHz–1.33 GHz, 以及 Powerbook 15–17 1.0–1.5 GHz G4)
- iBook (300–366 MHz G3—800 MHz 1.2 GHz G4)
- HPC (Xserver Cluster Node 1 1.33 MHz G4, Single/Dual 1.33 MHz G4, Cluster Node 2 2.0 GHz G5, 以及 Single/Dual 2.0 GHz G5)

Yellow Dog Linux 4.0 和 4.0.1 支持的硬件中明显缺失的是 Old World ROM 或米色 G3 及以下硬件，如 8500s、7200s 和 Performa PowerWCs。YDL 3.0.1 支持这种硬件以及 Yellow Dog Linux 4.0.1 目前支持的大多数硬件。Yellow Dog Linux 4.0.1 支持并测试的硬件包括：

- Power Mac G3 (Yosemite Blue and White 300–400 MHz G3)
- Power Mac G4 (Power Mac G4 PCI 350–400 MHz G4 及以上)
- Power Mac G5 (1.6 GHz G5 及以上)
- Mac Mini
- iMac (Rev A,B 233 MHz G3, eMac G4, 和 iMac G5)
- PowerBook (Lombard 300–400 MHz G3, Pismo 400–500 MHz FW G3, Titanium 400–1 MHz G4, Powerbook 12" 867 MHz–1.33 GHz, 以及 Powerbook 15–17 1.0–1.5 GHz G4)
- iBook (300–366 MHz G3—800 MHz 1.2 GHz G4)
- HPC (Xserver Cluster Node 1 1.33 MHz G4, Single/Dual 1.33 MHz G4, Cluster Node 2 2.0 GHz G5, 以及 Single/Dual 2.0 GHz G5)

## 规划安装

在开始之前，备份你想要保留的数据。下一步是决定你是要多启动还是安装。

## 在同一个硬盘上安装 OS X 和 Yellow Dog Linux

如果你想在一个硬盘上除了 Yellow Dog Linux 外安装 OS 9 或以下版本，你可以对双启动机器执行以下操作：

1. 插入 Mac OS CD 并启动。
2. 双击 Utilities（工具）。

除了可以在自己的 Apple 硬件上安装 Yellow Dog Linux 之外，你还可以从 Terra Soft Solutions 购买预装 Yellow Dog Linux 的 Apple 硬件。

Terra Soft Solutions 开发了专门针对 Yellow Dog Linux 测试过的硬件配置官方列表（http://yellowdoglinux.com/support/hardware/breakdown/index.php）。Yellow Dog 4.0.1 包括：

- Power Mac G3 (Yosemite Blue and White 300–400 MHz G3)
- Power Mac G4 (Power Mac G4 PCI 350–400 MHz G4 及以上)
- Power Mac G5 (1.6 GHz G5 及以上)
- Mac Mini
- iMac (Rev A,B 233 MHz G3, eMac G4, 和 iMac G5)
- PowerBook (Lombard 300–400 MHz G3, Pismo 400–500 MHz FW G3, Titanium 400–1 MHz G4, Powerbook 12" 867 MHz–1.33 GHz, 以及 Powerbook 15–17 1.0–1.5 GHz G4)
- iBook (300–366 MHz G3—800 MHz 1.2 GHz G4)
- HPC (Xserver Cluster Node 1 1.33 MHz G4, Single/Dual 1.33 MHz G4, Cluster Node 2 2.0 GHz G5, 以及 Single/Dual 2.0 GHz G5)

