

## 第8章
## 使用 Ubuntu 打印

从一开始，Ubuntu 就为来自众多不同制造商的海量打印机提供支持。本章将介绍如何将打印机连接到 Ubuntu 并使其与 Ubuntu 通信，以及 Ubuntu 用于管理打印机和打印作业的软件。

与大多数其他 Linux 发行版保持一致，Ubuntu 使用 CUPS（Common Unix Printing System，通用 Unix 打印系统）来处理打印机。其他系统也得到支持，例如 LPRng，但您无法从 Ubuntu 中访问其中的一些图形化管理工具。

### 互联网打印协议

CUPS 支持互联网打印协议，即 IPP，并提供许多独特功能，例如网络打印机目录（打印机浏览）服务、加密支持以及对 PostScript Printer Description（.ppd）文件的支持。

根据互联网工程任务组（IETF）的说法，IPP 源于 Novell 于 1996 年提出的一项创建可在互联网上使用的打印协议的提案。此后，该系统得到了开发并成熟为可在各种 Linux 和类 Unix 操作平台上使用的稳定打印系统。

### Ubuntu 打印概述

Ubuntu 的打印过滤器系统是实现打印多种类型文档的主要引擎。该引擎的核心是 Aladdin Ghostscript 解释器的 GNU GPL 版本，即 gs 客户端。系统管理员的打印机配置工具是 system-config-printer 客户端。

> **注意。**
> 
> Ubuntu 的打印系统可用于打印到本地（连接）或远程（网络）打印机。如果您使用本地打印机，它由打印机设备表示，例如 `/dev/lp0` 或 `/dev/usb/lp0`（如果您有 USB 打印机），而远程打印机使用在系统打印机功能数据库 `/etc/printcap` 中定义的打印队列。正在打印的文档称为打印作业，您可以查看并监控其打印队列，即 spool 目录中的当前打印作业，该目录为 `/var/spool/cups`。请注意，您只能控制自己的打印作业；只有 root 操作员才能控制系统上任何用户的打印作业。

要向系统添加打印机，您可以使用 system-config-printer 客户端创建、配置并保存打印机的定义。

CUPS 在 `/etc/cups` 目录下的名为 `printers.conf` 的文件中维护其自己的已定义打印机数据库。例如，之前在 `/etc/printcap` 中定义的关联打印机可能在 `/etc/cups/printers.conf` 中具有以下条目：

```
 <DefaultPrinter lp>
Info Created by system-config-printer 0.7.x
DeviceURI parallel:/dev/lp0
Location HP P135 local printer
State Idle
Accepting Yes
JobSheets none none
QuotaPeriod 0
PageLimit 0
KLimit 0
</Printer>
```

此示例显示了名为 lp 的打印机的定义，以及与其关联的设备、描述、状态和其他信息。此文件中各种可能的字段和条目在 printer.conf 手册页中有文档记录。

CUPS 使用一个名为 cupsd 的打印服务器（守护进程），在 CUPS 文档中也称为调度程序。服务器可以像其他 Ubuntu 服务一样通过 `/etc/init.d/cupsys` 命令或 system-config-services 客户端进行控制。服务器在系统上的工作方式由其配置文件 cupsd.conf 决定，该文件位于 `/etc/cups` 目录下。CUPS 可执行文件位于 `/usr/lib/cups` 目录下。

cupsd.conf 手册页记录了服务器的 80 多种不同设置，您可以将其配置以匹配您的系统、网络或打印环境。默认的 CUPS 相关文件和目录存储在 `/usr/share/cups` 目录下。日志记录可设置为七个不同的级别，访问和错误信息存储在 `/var/log/cups` 目录下的日志文件中。

### 本章内容

- Ubuntu 打印概述
- 配置和管理打印服务
- 创建和配置本地打印机
- 参考

