
在过去的几年里，人们尝试使用 Wine 运行 Windows 程序。当某人在 Wine 下运行程序时，他们可以将其添加到数据库并给出评分。表 7-1 显示了一些程序以及它们的测试年份。表中列出的所有程序评分均为 5.0。数据库中总共列出了 77 个程序，平均分为 2.4。

◆ `xdos` — 在它自己的 X 窗口中启动 DOSEM。你也可以使用 `dos -X` 启动。

◆ `dosec` — 启动 DOSEM 并执行一个 DEXE 文件。你也可以使用 `dos -L` 加载可执行的 DOS 文件。

现在你已经在你的 Linux 系统上运行了一个 DOS 会话，接下来要做什么？你必须知道的一点是如何关闭 DOS 会话。需要输入特定的按键序列才能退出会话。按下 `Ctrl+Alt+PgDn` 关闭 DOSEMU。

DOSEMU 不是一个完成的产品，因此会产生很多 bug 和问题。然而，所有方面都在不断改进。你可以访问网站检查更新、报告 bug 并获取程序的最新消息。你也可以在 `www.debian.org/Packages/unstable/otherosfs/dosemu.html` 检查最新的可用 Debian 软件包。

Wine 不是模拟器，Wine 的名字含义如此。与 DOSEMU 类似，Wine 更像是一个虚拟机，DOS 在其中加载应用程序到模拟的 DOS 环境中。Wine 运行在一个可以运行 Windows 应用程序的环境中，但该环境并没有被模拟。Wine 使用 Windows 接口 (`API`) 构建，它会读取程序在 Windows 中的交互并将其翻译为 Linux 可以理解的内容。你可以在 `www.winehq.com` 了解更多关于 Wine 的信息，那里一直有进展。

# 安装

通过 `dselect` 安装 Wine 时，所有的依赖项、所需文件和冲突应用程序都由 Wine 软件包依赖集预先确定。当然，无论你使用 `dselect` 安装哪个应用程序，这都是真的。使用正斜杠 (`/`) 搜索应用程序，然后输入 `wine` 并按回车。使用反斜杠 (`\`) 查找你搜索的字符串的下一个实例；你真正需要的只有 `wine`；不过你可能也想安装 `wine-doc` 文档包。Wine 还有几个库软件包。

## 配置

使用 Wine 的最佳方法是使用双系统——Windows 和 Linux。你可以将 Windows 分区添加到文件系统中，以便 Linux 能够访问。在你的 `/etc/fstab` 文件中添加以下行：

```
/dev/sda1    /mnt/win    vfat      defaults      0 0
```

`/dev/hd1` 是包含 Windows 软件的 Windows 分区。`/mnt/win` 是 Linux 用于挂载 Windows 分区的起始路径。在挂载分区之前，确保该路径存在。如果不存在，你需要为它创建一个目录。如果你选择将起始路径与我这里的一一样，可以使用此命令创建路径：

```
mkdir /mnt/win
```

你也可以将其更改为你喜欢的任何内容。只需确保路径存在；否则它无法挂载。文件系统表 (`stab`) 的其余部分保持不变。

Windows 分区有了挂载路径后，编辑 Wine 配置文件 (`/etc/wine.conf`) 以反映该路径。从接下来显示的配置文件中的某些设置可以看出，软驱、CD-ROM 和 C 盘的路径都与挂载路径匹配。默认情况下，C 盘设置为 `/c`，我已将其更改以匹配实际路径。最后，WINE 区域设置的此配置参数指向用户的家目录。最后，WINE 区域设置了 Windows 文件和 Windows 系统文件的所在位置。

```
[Drive A]
Path=/floppy
Type=floppy
Label=Floppy
Serial=876543321
Device=/dev/fd0
```

```
[Drive C]
Path=/mnt/win
Type=hd
Label=MS-DOS
Filesystem=win95
```

```
[Drive D]
Path=/cdrom
Type=cdrom
Label=CD-Rom
Filesystem=win95
```

```
[Drive E]
Path=/tmp
Type=hd
Label=Tmp
Filesystem=win95
```

```
[Drive F]
Path=$(HOME)
Type=network
Label=Home
Filesystem=win95
```

```
[wine]
Windows=c:\windows
System=c:\windows\system
Temp=e:\nPath=c:\windows\system;e:\test;f:\nSymbolTableFile=/usr/lib/wine.sym
```

配置文件的其余部分可以安全地留不管，因为它们处理的是程序的细节。这就是设置某些选项的地方——例如串口、并行口和打印端口。

# 运行应用程序

一旦驱动器挂载、配置文件设置好，你就可以准备运行第一个应用程序了。确保带有 Windows 的分区区已挂载，并且你知道想要运行的应用程序的完整路径。按照以下语法加载程序：

```
wine [options] program1 [program2 ...]
```

你可以通过在命令行中添加路径来一次加载多个程序。让我们从一个简单的示例开始测试你的设置。使用此命令启动标准计算器：

```
wine /mnt/win/windows/calc.exe
```

你应该能像在 Windows 下一样看到计算器。图 7-2 显示了科学模式下看到的 Windows 计算器。

![](img/0d314422de05113fe6acc6b5e7b494ff_171_0.png)

图 7-2：在 Linux 世界中运行如 calc 等 Windows 程序

# 应用程序

在过去的几年里，人们尝试使用 Wine 运行 Windows 程序。当某人在 Wine 下运行程序时，他们可以将其添加到数据库并给出评分。表 7-1 显示了一些程序以及它们的测试年份。表中列出的所有程序评分均为 5.0。数据库中总共列出了 77 个程序，平均分为 2.4。

## 表 7-1 在 Wine 下测试的程序

| 制造商 | 产品 | 测试年份 |
| :--- | :--- | :--- |
| Adobe | Acrobat Distiller 3.0 | 1999 |
| Blizzard | 星际争霸 | 1998 |
| Blizzard | 战兽世界 | 1999 |
| Blizzard | 暗黑神 | 2000 |
| Corel | WordPerfect 9 | 1999 |
| Corel | Corel Draw | 1999 |
| Macromedia | Painter 4 | 2000 |
| Microsoft | 记事本 | 1998 |
| Microsoft | WordPad | 1998 |
| Microsoft | Visual Basic | 1998 |
| Microsoft | 计算器 | 1998 |
| Microsoft | Excel | 1998 |
| Microsoft | Access | 1998 |
| RealNetworks | RealPlayer (beta) | 1999 |
| Sierra | 半生之路 | 2000 |
| Westwood | 红色警戒 | 1998 |
| Westwood | 钛金矿 | 1999 |

# VMware 安装

尽管 VMware 不是支持的 Debian 产品且没有 Debian 软件包可以安装，但它有一个自动化安装程序。它交互式将应用程序安装在适当的位置。它还会确定软件是否与内核版本工作，然后进行重新编译以匹配内核。你可以使用默认响应回答大多数问题。

访问 VMware 网站 (`www.vmware.com`)，你可以找到如何下载评估版本。评估版和完整版的区别在于你收到的许可代码。演示版有 30 天有效期，而购买的版本永不过期。下载压缩包并填写注册表，以便 VMware 能将许可发送到你的账户。使用以下命令提取压缩包：

```
tar xzvf VMware-2.x.x-xxx.tar.gz
```

提取完成后，进入新的 `vmware-distrib` 目录。执行 `vmware-install.pl` Perl 脚本开始安装过程。按回车回答有关安装位置的问题。最后，会被要求阅读并响应许可条款。按空格键阅读直到到达底部，必须输入 `yes` 来接受许可条款。

注意：为了完成 VMware 的安装，你可能需要安装内核头文件以匹配你的内核版本。你可以使用 `apt-get install kernel-headers-2.2.xx` 来安装对应内核版本的头文件。如果你不确定正在运行内核的版本，运行 `dmesg |` 并查看结果的第一行文本获取内核版本。

## 第二部分 与 Debian 一工作

![](img/0d314422de05113fe6acc6b5e7b494ff_175_0.png)

**图 7-3：** 在虚拟机中安装整个操作系统。
