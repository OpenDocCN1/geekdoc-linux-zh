
## 使用 `Shell` 对象

若要使用 `Shell` 对象，请遵循以下常规步骤：

1. **在程序中包含 `Shell` 模块，请添加以下行：**
   `use Shell;`
   在创建 `Shell` 对象之前必须包含此代码行。

2. **要创建 `Shell` 对象，请使用以下语法：**
   `my $sh = Shell->new;`
   其中 `$sh` 是指向 `Shell` 对象的引用。

3. **使用 `Shell` 对象运行 `Linux` 命令，并通过将输出保存到适当的变量中来捕获任何输出。** 例如，要将 `/usr/share/perl/5.8.6` 目录的目录列表保存到一个名为 `@modules` 的数组中，请编写以下代码：
   ```perl
   @modules = $sh->ls("/usr/lib/perl/5.8.6/*.pm");
   ```
   之后，你可以按照自己的意愿处理这个包含 `Perl` 模块文件名的数组（即 `*.pm` 文件）。例如，若要遍历数组并打印每个字符串，请使用以下 `while` 循环：
   ```perl
   while(@modules) {
       $mod = shift @modules;
       # 对模块名称进行任意处理
       print $mod;
   }
   ```

如何知道调用哪些方法以及按什么顺序调用它们？在使用对象之前，必须阅读该对象的文档。方法名称和方法调用的顺序取决于对象的功能。

## 使用 `English` 模块

`Perl` 包含一些具有特殊名称的变量，例如 `$_`（用于默认参数）和 `$!`（用于对应最后一个错误的错误消息）。在阅读程序时，猜测特殊变量的含义可能很困难。结果是你可能会避免使用在程序中可能很有用的特殊变量。

作为一种有益的功能，`Perl` `5` 提供了 `English` 模块（`English.pm`），该模块允许你使用可理解的名字来引用 `Perl` 中的各种特殊变量。要在 `Perl` 程序中使用 `English` 模块，请在程序中包含以下代码行：

`use English;`

之后，你可以将 `$_` 称为 `$ARG`，将 `$!` 称为 `$ERRNO`。（这些 *English* 名称可能仍然有些晦涩，但肯定比标点符号好得多。）

以下程序使用了 English 模块——并打印了一些有趣的变量：

```perl
#!/usr/bin/perl -w
# 文件: english.pl
use English;
print "Perl 可执行文件 = $EXECUTABLE_NAME\n";
print "脚本名称 = $PROGRAM_NAME\n";
```

使用以下命令运行此脚本：

`./english.pl`

当我运行此脚本时，得到的输出如下：

```
Perl 可执行文件 = /usr/bin/perl
脚本名称 = ./english.pl
```

English 模块非常实用，因为它让你能够编写 Perl 脚本，在脚本中可以使用有意义的名称来引用特殊变量。若要了解有关 Perl 特殊变量及其 English 名称的更多信息，请在终端窗口中输入 **man perlvar** —— 或者，更好的方法是让你的 Web 浏览器指向 `perldoc.perl.org/perlvar.html`

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
   Knoppix 是一个 Live CD 发行版，因此此步骤应为你显示 Knoppix 桌面。对于其他发行版，此步骤将运行该发行版的安装程序。从此时起，当安装程序带你完成各个步骤时，请回答所提的问题并做出选择。以下是一些典型的安装步骤：
   - 为 Linux 准备硬驱动器分区。如果你通过减小现有 Windows 分区的大小来创建空间，此步骤允许你为 Linux 创建分区。
   - 配置以太网网络（如有）。通常，你通过使用 DHCP 自动配置网络。
   - 指定本地时区并设置 root 密码。
   - 在你的硬驱动器上安装启动加载器程序，以便在你关机后启动 PC 时可以启动 Linux。
   - 选择你想要安装的具体软件包，例如 X Window System 以及 GNOME 或 KDE 图形桌面。

### DVD 中包含的内容

本节概述了你在 DVD 上找到的软件和其他好东西。如果你需要帮助安装 DVD 上提供的各项内容，请回到上一节的安装说明。

![](img/792720823146d68f19fd50c99ebfce4b_798_0.png)

共享软件是完全功能正常、免费的版权程序的试用版。如果你喜欢特定的程序，可以支付名义费用向作者注册，并获得许可证、增强版本和技术支持。

免费软件是免费的版权游戏、应用程序和实用工具。你可以将它们复制到尽可能多的 PC 上——免费——但它们不提供技术支持。

软件的试用版、演示版或评估版通常受到时间或功能限制（例如，不让你创建项目后保存它）。

GNU 软件受其自己的许可证约束，该许可证包含在 GNU 软件的文件夹中。对 GNU 软件的分布没有限制。有关详情，请参阅 DVD 根目录或本书背面的 GNU 许可证。按照 GNU 许可证的要求，本书包含 Fedora Core 的源代码。至于 Debian、Knoppix、SUSE 和 Xandros 的源代码，以下是如何从互联网获取每个应用程序源代码的方法：

- **Debian:** 浏览 www.debian.org/mirror/list 上的镜像站点列表，并点击离你最近的站点的 URL。站点加载后，进入 pool 目录，然后在三个目录之一（main、contrib 和 non-free）中寻找源代码文件。文件按软件包名称的首字母进一步组织到单独的目录中。例如，sendmail 软件包的源代码在 s 目录中。（有关 pool 目录的更多信息，请参阅 www.debian.org/doc/FAQ/ch-ftarchives.en.html#s-pools。）
- **Knoppix:** 许多用于 Knoppix 的软件包来自 Debian 项目，其源代码可从 Debian 网站获取。（有关下载 Debian 源代码的信息，请参阅上一项目。）从 www.knopper.net/download/knoppix 下载 Knoppix 特定的源代码。
- **MEPIS:** MEPIS 中的大多数软件包来自 Debian 项目，其源代码可从 Debian 网站获取。（有关下载 Debian 源代码的信息，请参阅对 Debian 的描述。）MEPIS 独特的组件，如 MEPIS OS Center，是专有的，其源代码不可用。
- **SUSE:** 从 http://ftp.opensuse.org/pub/opensuse/distribution/SL-OSS-stable/inst-source/suse/src/ 服务器下载 SUSE Linux 的源代码软件包。
- **Ubuntu:** 你可以在 http://archive.ubuntu.com/ubuntu/ 找到 Ubuntu 源代码，其组织方式与 Debian 源代码的组织方式类似（请参阅对 Debian 的描述）。在运行 Ubuntu 时，你可以通过键入来

