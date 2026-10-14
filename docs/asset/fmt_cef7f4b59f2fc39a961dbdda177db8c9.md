
如果你不确定该做出什么选择，可以尝试几种不同的安装配置，看看哪种最符合你的需求且最舒适。对于本示例，我还选择了 `ext2`，即非日志文件系统，因为它具有更快的读写访问速度并使用更少的磁盘空间。其他人可能会发现 `ext3` 文件系统带来的可靠性提升值得付出性能损失。

如果你的系统性能不足（或你赶时间），你可能希望从 DSL CD 以“安装模式”进行安装。在启动提示符下输入 `install`：

```
boot: install
```

这会引导你进入以下 DSL Install Options：

```
┌──[ DSL Install Options ]──────────────────────────────┐
│                                                        Net Access Req’d │
│  1. Make Standard Boot Floppy                         yes              │
│  2. Make USB Boot Floppy                              yes              │
│                                                        │
│  3. **Install to Hard Drive**                         **no**            │
│  4. Frugal Grub Hard Drive Install                    no               │
│  5. Frugal Lilo Compact Flash Install                 no               │
│                                                        │
│  6. USB Pendrive ZIP boot Install                     no               │
│  7. USB Pendrive HDD boot Install                     no               │
│                                                        │
│  8. Split KNOPPIX into floppy sized chunks            no               │
└────────────────────────────────────────────────────────┘
```

+   9. Interactive KNOPPIX split onto floppies    no

+   10. DSL FreeDOS Utilities                      yes

+   11. PCMCIA Module Floppy                       yes

+   12. Reboot

+   13. Shutdown

+   

+       Command:

+   0. quit

要启动硬盘安装脚本，请按如下方式输入数字 `3`：

```
Command: 3
```

`ds1-hdinstall` 脚本开始运行，如图 9-4 所示。

![](img/af53325d7f38f1cdafca9f44568e4ab8_204_0.png)

系统会询问你希望将 DSL 安装到哪个分区。在本例中，我们已将 `/dev/hda1` 准备好用于接收 DSL，因此你需要在提示符下输入 `hda1`。

接下来，系统会询问你是否希望以多用户登录方式运行 DSL，还是直接以用户 DSL 启动到桌面。如果你希望在访问计算机前被提示输入用户名和密码，请输入 `y` 并按 Enter 键（否则，直接按 Enter）。

下一个问题询问你是否希望使用 `ext3`（日志文件系统）或保持默认的 `ext2` 文件系统。如果你想要 `ext3`，请输入 `y` 并按 Enter；如果你想继续使用更轻量的 `ext2` 文件系统，只需按 Enter 键即可。

如 图 9-5 所示，在擦除硬盘分区并开始安装之前，你有最后一次机会退出。

在你输入 `y` 并按 Enter 键后，脚本开始格式化分区并安装运行 DSL 所需的文件。此过程可能需要几分钟。

![](img/af53325d7f38f1cdafca9f44568e4ab8_205_0.png)

文件复制完成后，脚本会询问你是否要安装引导加载程序。如果你的计算机将专门用于 DSL 且不使用多启动选项（如果你按照本章作为指南，这应该是大多数人的做法），你 definitely 需要为此选项输入 `y`。

在这里，你需要在 `Grub` 和 `Lilo` 之间进行选择。两者各有优点；总体而言，大多数人认为 `Grub` 更具通用性，而 `Lilo` 如果你只是想设置好后就不用管它，则使用起来更简单。图 9-6 显示了选择 `Lilo` 的结果。

![](img/af53325d7f38f1cdafca9f44568e4ab8_205_1.png)

脚本完成后，有必要重新启动系统以完成整个过程。系统重新启动后，会要求你设置 `root` 和用户 `DSL` 的密码。这就是最后一步——现在你的计算机上已拥有一个常规安装的 Damn Small Linux。

## 对那些对多启动感兴趣的人的进一步阅读

对多启动系统感兴趣的人可能想查看 `Gparted LiveCD`，其中包含 `Gparted` 软件。使用此 Live CD，你将能够调整大小、移动或销毁现有分区。

`Gparted LiveCD` 网址为：http://gparted.sourceforge.net/

对于对使用 `grub` 双启动感兴趣的人，`tldp.org` 上有一个不错的 howto：http://tldp.org/HOWTO/Linux+win9x+Grub-HOWTO/index.html

对于对使用 `Lilo` 多启动感兴趣的人，`tldp.org` 上也有另一个 howto：http://tldp.org/HOWTO/Multiboot-with-LILO.html

## 使用 DPKG-RESTORE 启用 APT-GET

我们提供了一个脚本，可以简化在计算机上启用 `apt-get` 的过程。假设你的计算机具有 Internet 访问权限，你所需要做的就是打开一个终端窗口并以 `root` 身份输入以下内容：

```
# dpkg-restore
```

这将恢复缺失的 `apt` 工具，并用与 Debian Woody 兼容的应用程序填充你计算机的 `apt-cache`。我们从 Debian 的归档中提取应用程序列表。请记住，许多应用程序不可避免地会覆盖 DSL 框架，最终你会得到一个损坏的桌面或一个经典版本的 Debian（如果你下载了覆盖库的应用程序）。因此，请谨慎操作，并清楚你想对系统做什么。

## 总结

我们逐步介绍了在硬盘上常规安装 Damn Small Linux 的基本步骤，包括硬盘准备和安装过程。如前所述，常规硬盘可能不是许多人的最佳选择；然而，在某些特殊情况下，DSL 非常适合某些计算机，包括内存有限的情况。

如果你尝试了 DSL 的常规硬盘安装，恭喜你！我相信你一定有有趣的故事来解释为什么你选择完成这样一次冒险的过程。但是，如果它能让一台古老的计算机免于被送进垃圾填埋场，那就更值得了！

# 第三部分

# 创建扩展和重新制作

- 第10章 添加应用程序并创建可共享扩展 189

- 第11章 设置完整的重新制作环境 211

## 添加应用程序并创建可共享扩展

正如我们在第5章“使用 MyDSL 扩展应用程序”中所看到的，Damn Small Linux 可以通过 `MyDSL` 扩展系统轻松扩展，以运行比基础 50MB 系统提供的更多应用程序。在本章中，我们将讨论几种制作自己的 `MyDSL` 扩展的方法。

创建扩展的方法有很多——无论是修改现有的软件包，还是 `tarball`、`Debian` 软件包，或是从源代码编译。我们将学习如何制作全部四种类型的 `MyDSL` 扩展：从 `.tar.gz` 到 `.dsl`、`.uci` 和 `.unc`。

### 概述

所有基于 UNIX 的系统都将应用程序作为文件和目录的集合添加到文件系统中。通常使用的方法是 `TAR`（磁带归档）或 `CPIO`（复制输入输出）。后来的软件包管理系统会结合特定于其发行版的安装脚本。有些还会添加已安装应用程序及其所需依赖项的数据库。

不同的软件包管理系统通常具有不同的软件包格式，使用不同的命令来管理其软件包，并将软件包名称扩展更改为其发行版独有的名称。例如，Debian 软件包使用 `.deb`，Red Hat Linux 软件包使用 `.rpm`。`dpkg` 和 `apt-get` 工具通常用于安装和管理 Debian 软件包，而 `rpm` 和 `yum` 命令则最常用于源自 Red Hat Linux 的打包系统（如 Fedora、Red Hat Enterprise Linux 等）。
