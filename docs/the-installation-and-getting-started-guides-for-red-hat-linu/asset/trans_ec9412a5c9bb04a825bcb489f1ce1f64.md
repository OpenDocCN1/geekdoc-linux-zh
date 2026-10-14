

他们的目标是继续添加 linuxconf 文档；你在这里看到的只是这一过程的第一步。软件包列表已被证明非常受欢迎；这次他们通过添加图标来改进它，以显示某个软件包是否属于预定义的软件包集。所有这些导致《安装指南》略微增重。这是预计会继续的趋势。

## 我不可能独自完成...

我要向本手册的过去作者们表示衷心感谢。他们的许多工作仍保留在此处。还要感谢那些耐心倾听我提问并更加耐心地给我答案的开发者和测试人员。没有他们的帮助，我无法完成这本手册。还要向文档团队的两位成员表示“BIG”感谢。我们的编辑 Paul Gallagher 对本手册的校对和编辑工作做得非常出色。他还撰写了本书的 GnoRPM 章节和《Red Hat Linux 官方入门指南》。文档团队的“无畏领袖”兼负责人 Edward Bailey 在让我保持最新信息并帮助我朝着正确的方向前进方面做得非常出色。他还被认为撰写了本《安装指南》中的新分区附录。没有他的领导和指导，这对我来说将是一项不可能完成的任务。你们二位合作起来很愉快，我真的无法表达足够的感谢。还要感谢过去《安装指南》的所有读者。没有他们的更正、建议甚至偶尔的赞扬，我就不知道自己是否走在正确的轨道上。你们的反馈已尽可能被纳入（在页数和截止日期允许的情况下）。请继续提供反馈。还要感谢 Cynthia Dale 更新了常见问题解答章节，以及 Jeff Goldin 为出版进行了校对。不幸的是，由于手册中空间不足，我们无法印刷它。但是，你可以在 http://www.redhat.com/knowledgebase/index.html 找到最新版本的 FAQ。最后，感谢 Red Hat Software 的支持团队。他们基于对数千名 Red Hat Linux 客户的丰富经验，对本手册提出了许多富有洞察力的建议。如果你发现自己阅读本《安装指南》更加轻松，其中很大一部分要归功于他们的努力。感谢 Red Hat Software 的每一个人对你们的帮助和支持。

Sandra A. Moore

## 1 Red Hat Linux 6.0 的新功能

本章描述了 Red Hat Linux 6.0 的新功能。

### 安装相关增强

以下是为了使 Red Hat Linux 安装过程更加简单而做出的许多更改的列表：

- New HTTP Installation Method
- “Out-of-the-Box” Processor Optimized Kernel Support
- New Boot Disks
- Improved Package Selection Screen
- New Authentication Configuration Screen
- Xconfigurator Now Part of Install

让我们更详细地了解一下每一个。

### New HTTP Installation Method

Red Hat Linux 6.0 安装程序已将 HTTP 添加到其可用的网络类安装列表中。与执行 FTP 安装的方式类似，你现在能够登录到一个网站并安装 Linux。有关网络类安装的更多信息，请参阅第 5 章。

### ‘Out-of-the-Box’ Processor Optimized Kernel Support

现在支持 Pentium Pro、Pentium II 和 Pentium III 处理器的优化内核以及 APM 启用的内核。此外，Red Hat Linux 6.0 安装现在具有 SMP 主板支持。安装过程将探测你的系统，如果检测到多于一个处理器，则会自动安装 SMP 启用的内核。

### The Installation Guide for Red Hat Linux 6.0

### New Boot Disks

Red Hat Linux 现在有两个启动盘。一个用于从本地媒体安装（CD-ROM 安装、硬盘安装），另一个用于基于网络的安装（NFS、FTP 或 HTTP）。此外，补充盘已被 PCMCIA 支持盘取代。所有安装方法现在只需要一张盘，除非你在安装过程中需要 PCMCIA 支持。如果需要，将提示你插入 PCMCIA 支持盘。

### Improved Package Selection Screen

单个软件包选择已得到改进，采用可折叠和可扩展的树形菜单，以便在安装过程中轻松选择软件包。

### New Authentication Configuration Screen

身份验证配置屏幕为你提供了启用三种不同类型密码的选项：

- Enable NIS — 允许你在一个 Network Information Service 域中以通用密码和组文件运行一组计算机。这里有两个选项可供选择：
  - NIS Domain — 此选项允许你指定系统将属于哪个域或计算机组。
  - NIS Server — 此选项会导致你的计算机使用特定的 NIS 服务器，而不是“广播”一条消息到局域网请求任何可用服务器托管你的系统。
- Enable Shadow Passwords — 提供一种非常安全的方法来保留你的密码。
- Enable MD5 Passwords — 允许密码长达 256 个字符，而非标准的八个。

