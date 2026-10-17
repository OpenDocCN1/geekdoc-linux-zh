
```
$ sh linux-install.sh
```

这会启动图形化安装程序。一路继续下去，完成后，你应该能在`/home/username/ut2004`目录下找到《Unreal Tournament 2004》。

如果你想卸载 UT2004，可以使用`ut2004`目录中的卸载脚本。输入以下命令：

```
$ sh uninstall.sh
```

确认之后，Unreal Tournament 就会从你的系统中移除。

### Quake 4

由于基于 DOOM 3 引擎，你几乎可以预期《Quake 4》（见图 9.5）会自带对 Linux 的良好支持。要开始安装，你必须拥有该软件的 Windows 版本，因为你需要几个文件以及 CD 密钥才能运行游戏。不过，首先要做的事是前往 http://zerowing.idsoftware.com/linux/quake4/ 下载所需的 Linux 安装程序（`quake4-linux-1.0*.run`），可以通过直接 FTP 下载，也可以使用更节省带宽的 BitTorrent 下载。

下载完成后，进入命令行并输入以下命令：

```
$ sudo sh quake4-linux-1.0*.run
```

然后按下回车键。安装程序启动后，会问你几个问题。你回答这些问题后，安装程序会创建必要的文件和文件夹。你只需将 DVD 上`/quake4/qbase`目录中的几个文件复制到`/usr/local/bin/quake4/qbase`。之后，你可以在命令提示符下输入`quake4`来启动游戏。

### Wolfenstein: Enemy Territory

早期的《Return to Castle Wolfenstein》同时支持单人模式和多人模式，而免费提供的《Wolfenstein: Enemy Territory》则仅支持多人模式（见图 9.6）。该游戏提供 Win32 和 Linux 原生版本，你可以从 http://www.SplashDamage.com/ 下载。下载名为`et-linux-2.55.x86.run`的 260MB 文件后，输入以下命令进行安装：

```
$sudo sh et-linux-2.55.x86.run
```

然后接受默认设置。`/usr/local/bin`中会有一个指向加载游戏脚本的符号链接。

![](img/7aaa8e4f2209bf9f2fb443905096e94c_217_0.png)

图 9.5 基于广受欢迎的 DOOM 3 引擎，《Quake 4》让你对抗邪恶的 Strogg。出去把他们轰成渣！

![](img/7aaa8e4f2209bf9f2fb443905096e94c_217_1.png)

图 9.6 在这个葱郁但充满敌意的图形环境中，团队合作是取胜的关键。

### Battle for Wesnoth

当然，Linux 游戏远不止第一人称射击游戏。目前 Linux 上最流行的游戏之一是《Battle for Wesnoth》（见图 9.7），这是一款策略游戏，风格与《帝国时代》很相似。游戏设定在一个奇幻大陆上，你负责组建军队与敌人作战。

《Battle for Wesnoth》在 Ubuntu 上安装起来很容易。你需要使用`synaptic`或`aptitude`选择`wesnoth`软件包。安装完成后，你可以在命令行中输入以下命令启动它：

```
$ wesnoth
```

![](img/7aaa8e4f2209bf9f2fb443905096e94c_218_0.png)

图 9.7 通过玩《Battle for Wesnoth》来锻炼你的战略头脑——一个充满奇幻与冒险的丰富世界。

### 使用 Cedega 玩 Windows 游戏

如前所述，一个操作系统能否吸引大众市场，关键在于其可用的应用程序。一群开发者注意到，计算世界中的绝大多数人都在使用基于 Windows 的生产力软件和游戏软件，于是决定开发一种在 Linux 上运行这些软件的方法，从而让 Linux 用户也能访问这个庞大的应用库。这些开发者提出了一个名为 Wine 的程序，它定期更新，并构成了游戏变体 Cedega 的基础。这是一个商业产品，由开发商 TransGaming Technologies（http://www.transgaming.com/）提供，因此你无法使用`aptitude`获取它。

然而，Cedega 是一款广受欢迎且持续更新的产品，支持《上古卷轴 IV：湮没》和《魔兽世界》等最新发布的游戏。由于 Cedega 处于不断变化之中，TransGaming Technologies 提供订阅服务，这意味着每当代码有新版本发布时，你都能获得更新——确保你不仅能享受今天的游戏，也能享受明天的游戏。

因此，如果你等不及 Linux 在游戏开发者中变得更受欢迎，可以在他们被说服直接支持 Linux 之前，先用 Cedega 作为过渡方案。

> **提示**
>
> 在 Linux 中成功玩游戏的诀窍在于：始终彻底地阅读文档，始终彻底地研究互联网资源，并且始终了解你的系统。安装游戏是了解你系统的好方法，因为成功的回报十分有趣。

### 参考

- http://www.transgaming.com/——TransGaming Technologies 官方网站，提供 Cedega 直接支持的游戏详细信息。
- http://www.linuxgames.com/——提供 Linux 游戏现状最新信息的绝佳来源。
- http://zerowing.idsoftware.com/linux/doom/——包含在 Linux 下运行 DOOM 3 的完整操作指南和故障排除指南。
- http://www.unrealtournament.com/——虚幻竞技场的官方网站。
- http://www.nvnews.net/vbulletin/forumdisplay.php?f=14——Nvidia Linux 驱动官方支持论坛。
- http://www.nvidia.com/object/linux.html——Nvidia Linux 驱动程序的首页。
- http://tinyurl.com/3pm2v——ATI Linux 驱动程序的首页（由 tinyurl.com 提供）。

此页有意留空

## 第三部分

## 系统管理

### 本部分包括

- 第 10 章 管理用户 195
- 第 11 章 自动化任务 219
- 第 12 章 系统监控工具 275
- 第 13 章 备份 287
- 第 14 章 网络 311
- 第 15 章 通过 SSH 和 Telnet 进行远程访问 355

此页有意留空

### 第 10 章

### 管理用户

如果没有用户，系统管理员的生活就会清静得多！然而，你不可能拥有一个完全没有用户的系统，因此在用户与你的系统打交道时，学会如何有效地管理他们非常重要。无论你是在创建单个用户账户，还是在修改一个包含数百个用户账户的组，用户管理的基本原理都是相同的。

用户管理包括负责主目录的分配和管理、制定良好的密码策略，以及实施有效的安全策略，其中包括磁盘配额和文件与目录访问权限。在本章中，我们将探讨所有这些领域，以及你在一个典型的 Linux 系统上可能遇到的不同类型的用户。

#### 用户账户

在所有 Linux 系统上，你通常可以找到三种类型的用户：超级用户、日常用户和系统用户。每种类型的用户对于你系统的平稳运行都至关重要，而要在 Linux 环境中高效、安全地工作，了解这三者之间的区别也是必不可少的。

所有访问你系统的用户都必须在系统本身拥有账户。Ubuntu 使用`/etc/passwd`文件来存储系统中用户账户的信息。所有用户，无论其类型如何，在该文件中都有一行条目，其中包含其用户名（通常用于登录系统）、一个密码字段（其中包含一个 x 表示存在密码）、一个用户 ID（通常称为 UID）和一个组 ID

- 用户账户
- 管理组
- 管理用户
- 管理密码
- 向普通用户授予系统管理员权限
- 磁盘配额
- 参考

（通常称为 GID）。最后两个字段显示主目录的位置（通常是`/home/username`）和用户的默认 shell（新用户的默认值为`/bin/bash`）。

> 注意
>
> 密码字段中包含 x 并不代表这就是你的密码！所有密码实际上都经过加密并存储在`/etc/shadow`中妥善保管。每当需要密码时，Ubuntu 都会自动引用该文件。

与其他基于 UNIX 的操作系统一样，Linux 和 Ubuntu 采用了既有的 UNIX 文件所有权和权限系统。所有文件（可能包括目录和设备）都可以被赋予读取、写入和/或执行权限中的一种或多种。这三个“标志”也可以赋予文件所有者、组成员或系统中的任何人。文件的安全性来自这些权限以及文件所有权。作为系统管理员（通常称为超级用户），你有责任有效地管理这些设置，并确保用户拥有适当的 UID 和 GID。也许最重要的是，你需要通过文件权限将敏感文件锁起来，使其远离那些不应该访问这些文件的用户。

#### 超级用户/Root 用户
