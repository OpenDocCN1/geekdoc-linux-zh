
![](img/7aaa8e4f2209bf9f2fb443905096e94c_48_1.png)

FIGURE 1.14 Update Manager 帮你省去了保持软件为最新版本的繁重工作。

### Shutting Down

在某个时候，你会想要关闭电脑。与 Linux 中的大多数事情一样，有多种方法可以做到。你可以使用屏幕右上角的 Quit 图标，或使用系统菜单中的相同按钮。无论哪种方式，你都可以选择关闭或重新启动系统。你还可以选择休眠（将运行状态保存到磁盘并关机）或挂起（将当前运行状态保存到内存）。我们建议使用 `shutdown` 或 `reboot`，以确保系统恢复时是干净的。

如果你在命令行工作，可以立即通过以下方式关闭系统，使用 `shutdown` 命令：

```bash
$ sudo shutdown -h now
```

你也可以使用 `shutdown` 命令重新启动计算机，如下所示：

```bash
$ sudo shutdown -r now
```

对于新用户来说，安装 Ubuntu 只是学习 Linux 之路上一个全新且极具回报的旅程的开始。对于 Ubuntu 系统管理员来说，前方的任务是微调安装并自定义服务器或用户环境。

#### Reference

- http://www.ubuntu.com—寻找有关安装、配置和使用 Ubuntu 的新闻、信息和文档时开始的地方。
- http://tinyurl.com/c2x5u—Symantec 的 PartitionMagic 实用程序包含 BootMagic，可用于支持 Linux 或遗憾的是其他功能较弱的操作系统（如 Windows XP）的启动。
- http://www.v-com.com/product/System_Commander_Home.html—V Communications, Inc. 的 System Commander，一个商业 42MB 下载，可用于支持在当今 PC 上运行的任何操作系统的启动。智能分区实用程序 Partition Commander 包含在内。
- http://www.nwc.com/columnists/1101colron.html—如何使用 Intel 的预执行环境（PXE）协议远程启动工作站。
- http://www.gnu.org/software/grub/—GRUB 启动加载程序的主页。
- http://www.ibiblio.org/pub/Linux/docs/HOWTO/other-formats/html_single/BootPrompt-HOWTO.html—BootPrompt-HOWTO，关于使用启动提示传递内核参数的指南。
- http://www.tldp.org/HOWTO/Installation-HOWTO/index.html—Linux 安装 HOWTO，由 Eric S. Raymond 编写，关于安装 Linux 的指南。

## 第 2 章

## 安装后配置

### 本章内容

现在最困难的部分已经完成（安装 Ubuntu），你可以开始自定义你的新操作系统了。默认情况下，Ubuntu 为你提供了一个相当空白的画布来个性化你的体验。有些人选择保留巧克力色的背景，而其他人则进行彻底的改造。

在本章中，我们将了解如何开始使用 Ubuntu，包括快速浏览桌面。我们还将介绍一些自定义 Ubuntu 安装的方法，例如确保日期和时间设置正确，以及向你展示如何执行一些基本的管理任务，例如识别硬件中的任何问题。到本章结束时，你应该感到足够舒适，可以继续阅读本书的其余部分。

### 注意

在本章中，我们将介绍与本书其他章节也相关的几个关键应用程序。我们在这里包含它们是因为它们对于使你的系统按预期工作至关重要。随着你阅读本书，你会发现参考本章非常有价值。

- 安装后配置问题的故障排除
- `sudo` 命令
- 首次更新
- 配置软件存储库
- 安装图形驱动程序
- 更改 Ubuntu 的外观
- 首选行为
- 输入设备
- 检测和配置调制解调器
- 在 Ubuntu 中配置电源管理
- 重置日期和时间
- 配置和使用 CD、DVD 和 CD-RW 驱动器
- 配置无线网络
- 配置 Firestarter
- 参考

使用复制命令如下：

```
$ cp file file.backup
```

你永远不应该使用 `.bak` 扩展名，因为这可能会被其他自动进程覆盖，并在你尝试恢复原始文件时让你感到沮丧。

如果由于你更改了原始文件而导致某些问题，你始终可以使用以下命令将原始文件复制回原位：

```
$ cp file.backup file
```

（像这样简单的操作真的可以救你一命，尤其是在你对生产系统做了不该做的更改而承受压力时。也就是说，如果你愚蠢到在生产系统上做大规模更改的话！）

### sudo 命令

如果你接触过 Linux，你可能已经知道命令行了。正如你在阅读本书时会发现的，Ubuntu 在命令行工作中非常依赖 `sudo` 命令。该命令用于放在其他命令前面，以告诉 Ubuntu 你希望使用超级用户权限运行指定的命令。这听起来非常特别，而且确实如此。当你使用 `sudo` 命令工作时，你可以对系统进行广泛的更改，从而影响其运行方式。然而，在运行任何以 `sudo` 为前缀的命令时要格外小心；错误的选项或错误的命令可能会造成毁灭性的后果。

使用 `sudo` 很简单。你只需像这样输入：

```
$ sudo command commandoptions
```

只需将单词 `command` 替换为你想要运行的命令以及任何选项。例如，以下命令在 `vi` 中打开你的 `xorg.conf` 文件，并允许你以超级用户身份进行任何更改，然后再保存它：

```
$ sudo vi /etc/X11/xorg.conf
```

每当你使用 `sudo` 执行命令时，系统会提示你输入密码。这与你用于登录 Ubuntu 的密码相同，因此记住它很重要。

有时，你可能希望使用经典的 root 提示符，而不是在每个命令前都输入 `sudo`（例如，如果你必须在命令行上使用大量需要超级用户访问的命令）。`sudo` 通过使用 `sudo -i` 命令使你能够做到这一点。同样，系统会提示你输入密码，你应该输入它，之后 Ubuntu 会给你标准的 root 提示符，如下所示：

```
#
```

从这里开始，你可以执行任何命令而无需不断输入 `sudo`。

### 第一次更新

如第 1 章所述，你应在首次登录 Ubuntu 后尽快更新软件，以便受益于任何可用的安全补丁和错误修复。在那个示例中，我们使用了更新管理器，它实际上是命令 `apt-get` 的图形界面封装。在后台，Ubuntu 会自动轮询配置为标准源的软件仓库，以确定是否有可用更新。当检测到已安装软件的新版本可用时，屏幕右上角会弹出提示消息（见图 2.1）。点击面板中的“更新”图标，你会自动打开更新管理器，但在此之前会提示你输入密码（因为你即将进行系统级更改）。

![](img/7aaa8e4f2209bf9f2fb443905096e94c_54_0.png)

图 2.1 要快速轻松地安装更新，可以留意更新通知。

另一种更新系统的方法（可能比更新管理器更快）是使用命令行。如果你进入“应用程序”→“附件”菜单，选择“终端”选项，屏幕上会显示一个空白窗口。这就是命令行（通常称为终端），也是 Linux 最强大的功能之一。第 30 章“命令行大师班”会详细讨论它，因此我们这里不作深入介绍。

你会看到一个类似这样的提示符：

```
andrew@optimus:~$
```

还有一个闪烁的光标。Ubuntu 正在等待你的第一条命令。这里我们要发出以下命令：

```
$ sudo apt-get update
```

Get: 5 http://gb.archive.ubuntu.com gutsy-backports Release.gpg [189B]

Hit http://gb.archive.ubuntu.com gutsy Release

Get: 6 http://gb.archive.ubuntu.com gutsy-updates Release [30.9kB]

Get: 7 http://security.ubuntu.com gutsy-security/main Packages [25.1kB]

Get: 8 http://gb.archive.ubuntu.com gutsy-backports Release [19.6kB]

Hit http://gb.archive.ubuntu.com gutsy/main Packages

Get: 9 http://gb.archive.ubuntu.com gutsy/restricted Packages [4571B]

Hit http://gb.archive.ubuntu.com gutsy/universe Packages

Get: 10 http://gb.archive.ubuntu.com gutsy/multiverse Packages [95.2kB]
