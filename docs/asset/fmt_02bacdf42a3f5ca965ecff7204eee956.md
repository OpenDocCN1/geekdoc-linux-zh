
English 模块非常实用，因为它让你能够编写 Perl 脚本，在脚本中可以使用有意义的名称来引用特殊变量。若要了解有关 Perl 特殊变量及其 English 名称的更多信息，请在终端窗口中输入 `man perlvar` —— 或者，更好的方法是让你的 Web 浏览器指向 `perldoc.perl.org/perlvar.html`

## 附录：关于 DVD

### 本附录内容

- 系统要求
- DVD 安装说明
- DVD 中包含的内容
- 故障排除

本书的配套 DVD 包含七个主要的 Linux 发行版——Debian GNU/Linux、Fedora Core、Knoppix、MEPIS、SUSE、Ubuntu 和 Xandros Desktop OS——以帮助开始你的 Linux 之旅。本附录简要介绍了该 DVD 并告诉你如何开始安装。

### 系统要求

请确保你的计算机满足以下列表中的最低系统要求。如果你的计算机不满足大多数这些要求，你在使用该 DVD 上的软件和文件时可能会遇到问题：

- 处理器运行速度为 400 MHz 或更快的 PC 用于图形安装
- 计算机上至少安装 192MB 总 RAM 用于图形安装（建议 256MB）
- 硬驱动器上至少有 520MB 可用空间用于最小安装；如果你计划安装大多数软件包以体验本书涵盖的所有内容，则建议有 5GB 可用空间
- DVD-ROM 光驱和 CD 刻录机（请参阅第一本书第 2 章了解刻录安装 CD 的说明）
- 能够显示至少 256 种颜色的显卡和显示器
- 声卡
- 以太网网络接口卡（NIC）或速度至少为 56 Kbps 的调制解调器

### DVD 安装说明

要从配套 DVD 安装 Linux 发行版，请遵循这些步骤。（有关详细信息，请参阅第一本书第 2 章。）

1. 在安装 Linux 之前，收集关于你的 PC 硬件的信息，例如显卡、网卡和 SCSI 卡。
2. 使用分区程序，如 PartitionMagic 或 FIPS 程序，在你的硬驱动器上为 Linux 创建空间。
   如果你计划将 Linux 用作你 PC 上唯一的操作系统，或者计划将其安装在空的第二块硬驱动器上，则跳过此步骤。
3. 为你的发行版刻录 CD。（如果你正在安装 Fedora Core，则跳过此步骤。）
   请参阅第一本书第 2 章了解特定于每个发行版的说明。
4. 使用 DVD（用于 Fedora Core 和 Knoppix）或第一张 CD（用于 Debian、MEPIS、SUSE、Ubuntu 和 Xandros）启动你的 PC。

### DVD 中包含的内容

本节概述了你在 DVD 上找到的软件和其他好东西。如果你需要帮助安装 DVD 上提供的各项内容，请回到上一节的安装说明。

共享软件是完全功能正常、免费的版权程序的试用版。如果你喜欢特定的程序，可以支付名义费用向作者注册，并获得许可证、增强版本和技术支持。

免费软件是免费的版权游戏、应用程序和实用工具。你可以将它们复制到尽可能多的 PC 上——免费——但它们不提供技术支持。

软件的试用版、演示版或评估版通常受到时间或功能限制（例如，不让你创建项目后保存它）。

GNU 软件受其自己的许可证约束，该许可证包含在 GNU 软件的文件夹中。对 GNU 软件的分布没有限制。有关详情，请参阅 DVD 根目录或本书背面的 GNU 许可证。按照 GNU 许可证的要求，本书包含 Fedora Core 的源代码。至于 Debian、Knoppix、SUSE 和 Xandros 的源代码，以下是如何从互联网获取每个应用程序源代码的方法：

- **Debian:** 浏览 `www.debian.org/mirror/list` 上的镜像站点列表，并点击离你最近的站点的 URL。
- **Knoppix:** 许多用于 Knoppix 的软件包来自 Debian 项目，其源代码可从 Debian 网站获取。从 `www.knopper.net/download/knoppix` 下载 Knoppix 特定的源代码。
- **MEPIS:** MEPIS 中的大多数软件包来自 Debian 项目，其源代码可从 Debian 网站获取。MEPIS 独特的组件，如 MEPIS OS Center，是专有的，其源代码不可用。
- **SUSE:** 从 `http://ftp.opensuse.org/pub/opensuse/distribution/SL-OSS-stable/inst-source/suse/src/` 服务器下载 SUSE Linux 的源代码软件包。
- **Ubuntu:** 你可以在 `http://archive.ubuntu.com/ubuntu/` 找到 Ubuntu 源代码，其组织方式与 Debian 源代码的组织方式类似。
- **Xandros：** 通过遵循 `www.xandros.com/support/source_code.html` 上的说明，下载 Xandros 免费和开源组件的源代码。

以下命令：`sudo apt-get build-dep packagename`，随后输入 `sudo apt-get source packagename`，其中 `packagename` 是软件包的名称。

DVD 中包含几种不同格式的 Linux 发行版：

- **完整发行版：** 您可以从 DVD 启动并安装完整的发行版。
- **即插即用的 Live CD：** 您可以从 DVD 启动计算机来运行 Live CD。
- **ISO 镜像：** 您需要将 ISO 镜像刻录到 CD 上，然后从这些 CD 进行安装。

以下是 DVD 中包含的 Linux 发行版：

- **Debian：** 以网络安装 ISO 镜像的形式提供。
- **Fedora Core：** 作为完整发行版包含在内。
- **Knoppix：** 作为即插即用的 Live CD 包含在内。
- **MEPIS：** 提供为 Live CD ISO 镜像，同时也充当安装 CD。
- **SUSE：** 提供为单个 Live DVD ISO 镜像文件。
- **Ubuntu：** 提供为单个安装 CD ISO 镜像。
- **Xandros Open Circulation Edition：** 提供为单个 CD ISO 镜像。

### DVD 中您将找到的内容

每种 Linux 发行版的详细软件列表略有不同，但大多数发行版都包含以下内容：

- Linux 内核 `2.6.x`
- 基于 X Window 系统的图形用户界面，带有 GNOME `2.12` 和 KDE `3.4` 图形桌面
- Apache Web 服务器和 Mozilla Firefox Web 浏览器
- Samba `3.0.20` LAN 管理软件
- OpenOffice.org `1.9` 办公套件

### 故障排除

如果您在安装或使用配套 DVD 上的材料时遇到困难，请参阅第一册中详细的安装和故障排除说明。

若要追加订单或获取有关其他威利产品的信息，请致电 `(800) 225-5945`。

# 索引

### 符号

- （星号）通配符，167–168
- `!` FTP 命令，368

### A

- ABI（应用程序二进制接口），与 LSB 相关，15
- Apache Web 服务器
  - 访问控制指令，601–603
  - 配置，589–606

# B

- backups。参见 archives
- bash shell
  - built-in commands，739–742
  - overview，162

# C

- C 语言编程
  - 数组，707–708
  - break 语句，715
  - if-else 语句，718–719

# D

- Debian GNU/Linux 描述，11
  - GNOME 桌面，142–144
  - 安装，42–48

# E

- 电子邮件
  - 附件，316
  - MTA，314
  - MUA，314

# F

- Fedora Core
  - 描述，12
  - 安装，48–57
  - GNOME 桌面，144–146

# G

- GNOME (GNU 对象模型环境)
  - 自定义，119–121
  - Debian 桌面，142–144
  - 简介，20

# H

- 硬盘
  - 安装及，34
  - 编程，674

# I

- Internet
  - 连接，254–256
  - 电子邮件，253

# K

- KDE (K 桌面环境)
  - 简介，20
  - Knoppix，146–150

# L

- Linux
  - 命令，170–173
  - 发行版，10–14

# M

- MEPIS Linux
  - 描述，12
  - 安装，57–60

# N

- NFS（网络文件系统）
  - 描述，279
  - 文件共享，661–665

# O

- OpenOffice.org 办公套件
  - Calc，216–217
  - Writer，215–216

# P

- Perl
  - 描述，23
  - 表达式，746，751–752
  - 流程控制语句，746，755–758

# S

- 安全
  - 框架，建立，500–505
  - 防火墙，509，534–545

# T

- TCP/IP（传输控制协议/互联网协议）
  - 应用层，276
  - 网络层，276

# U

- Ubuntu Linux
  - 描述，13
  - GNOME 桌面，156–158

# X

- Xandros 桌面操作系统
  - 描述，130
  - 安装，73–80

## GNU 通用公共许可证

版本 2，1991 年 6 月

版权所有 © 1989, 1991 自由软件基金会，Inc.

### 前言

大多数软件的许可协议旨在剥夺您分享和修改它们的自由。相比之下，GNU 通用公共许可证旨在保证您分享和修改自由软件——确保软件对所有用户都是自由的。

### 复制、分发和修改的条款与条件

- 0. 本许可证适用于包含版权所有者放置的通知，声明其可依据本通用公共许可证条款进行分发的任何程序或其他作品。
- 1. 你可以以你收到的形式，复制和逐字分发程序的源代码。
- 2. 你可以修改你持有的程序或其任何部分的副本，从而形成基于程序的作品。
- 3. 你可以依据上述第1节和第2节的条款，以目标代码或可执行形式复制和分发程序。
- 4. 除本许可证明确规定的情况外，你不得复制、修改、再许可或分发程序。
- 5. 你无需接受本许可证，因为你未签署它。
- 6. 每次你重新分发程序时，接收者自动从原始许可方获得根据这些条款和条件复制、分发或修改程序的许可证。
- 7. 如果由于法院判决或专利侵权指控，或由于任何其他原因强加给你的条件与本许可证的条件相矛盾，这些条件并不免除你遵守本许可证的条件。
