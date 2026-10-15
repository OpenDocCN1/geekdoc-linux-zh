
由于 Quake 4 基于 DOOM 3 引擎，你几乎可以期待它为 Linux 提供相当多的支持（见图 13.4）。开始之前，你必须拥有该软件的 Windows 版本，因为你需要多个文件以及 CD 密钥才能玩游戏。首先，先前往 http://zerowing.idsoftware.com/linux/quake4/ 下载所需的 Linux 安装程序（`quake4-linux-1.0*.run`），可通过直接 FTP 或更省带宽的 BitTorrent 下载。

下载文件后，切换到命令行并输入以下内容：

```
$ sudo sh quake4-linux-1.0*.run
```

然后按 Enter。安装程序启动并会询问你几个问题。回答后，安装程序会创建必要的文件和文件夹。你只需将 DVD 上 `/quake4/qbase` 目录中的几个文件复制到 `/usr/local/bin/quake4/qbase`。你可以通过在命令提示符下输入 `quake4` 启动游戏。

## 安装 Wolfenstein: Enemy Territory

与早期的 Return to Castle Wolfenstein 既支持单人又支持多人不同，可免费获得的 Wolfenstein: Enemy Territory 仅支持多人游戏（见图 13.5）。它提供 Win32 和 Linux 原生版本，你可以从 http://www.SplashDamage.com/ 下载。下载完成后，名为 `et-linux-2.55.x86.run` 的 260MB 文件，安装游戏请输入以下命令：

```
# sh et-linux-2.55.x86.run
```

![](img/e464b828c497c99e41f61d4c55f1c0db_290_0.png)

图 13.4 基于流行的 DOOM 3 引擎，Quake 4 让您与邪恶的 Strogg 为敌。出去吧，干掉他们！

然后接受默认值。`/usr/local/bin` 中存在一个指向加载游戏脚本的符号链接。

![](img/e464b828c497c99e41f61d4c55f1c0db_290_1.png)

图 13.5 在这个郁郁葱葱但敌对的图形环境中，团队合作是取得胜利的关键。

## 安装《威森诺之战》

当然，Linux 游戏远不止第一人称射击游戏。目前最受欢迎的 Linux 游戏之一是《威森诺之战》（见图 13.6），这是一款策略游戏，很像《帝国时代》。背景设定在奇幻大陆，您负责组建军队与敌人作战。

《威森诺之战》在 Ubuntu 上安装非常容易。您需要使用 `synaptic` 或 `aptitude` 选择 `wesnoth` 软件包。安装后，您可以通过命令行启动它，输入以下内容：

```
$ wesnoth
```

![](img/e464b828c497c99e41f61d4c55f1c0db_291_0.png)

图 13.6 通过玩《威森诺之战》锻炼您的战略思维——这是一个丰富而完整的奇幻冒险之地。

## 使用 Cedega 玩 Windows 游戏

如前所述，操作系统的大众市场吸引力关键在于可用的应用程序。一群开发者看到绝大多数计算世界都在使用基于 Windows 的生产力和游戏软件，于是决定开发一种在 Linux 上运行这些软件的方法，从而让 Linux 用户能够使用这一庞大的应用程序库。开发者推出了一个名为 `Wine` 的程序，该程序定期更新，并构成了名为 `Cedega` 的游戏变体的基础。这是一款由开发者 TransGaming Technologies（http://www.transgaming.com/）提供的商业产品，因此您无法使用 `aptitude` 获取它。

然而，`Cedega` 是一款流行且最新的产品，支持《半条命 2》、《席德·梅尔的海盗！》和《魔兽世界》等近期发行作品。由于 `Cedega` 的状态不断变化，TransGaming Technologies 提供了订阅服务，这意味着代码发布时您会获得更新——确保您不仅能享受今天的游戏，也能享受明天的游戏。

因此，如果您等不及 Linux 在游戏开发者中变得更受欢迎，请使用 `Cedega` 作为过渡，直到他们能被说服直接支持 Linux。

TIP

在 Linux 中成功游戏的关键是始终彻底阅读文档，始终彻底调查互联网资源，并始终了解您的系统。安装游戏是了解系统的绝佳方式，因为成功的回报非常有趣。

## 参考

- http://www.transgaming.com/—TransGaming Technologies 官方网站提供了在 Cedega 下直接支持的游戏详情。
- http://www.linuxgames.com/—关于 Linux 游戏现状的最新信息的良好来源。
- http://zerowing.idsoftware.com/linux/doom/—包含在 Linux 下运行 DOOM 3 的完整操作指南和故障排除指南。
- http://www.unrealtournament.com/—《无敌战神》的官方网站。
- http://www.nvnews.net/vbulletin/forumdisplay.php?f=14—官方 Nvidia Linux 驱动支持论坛。
- http://www.nvidia.com/object/linux.html—Nvidia Linux 驱动的首页。
- http://tinyurl.com/3pm2v—ATI Linux 驱动的首页（由 tinyurl.com 提供）。

# 第二部分

# 系统管理

## 本部分内容

- 第 14 章 管理用户 265
- 第 15 章 自动化任务 291
- 第 16 章 系统资源 347
- 第 17 章 备份、恢复和恢复 359
- 第 18 章 网络连接 389
- 第 19 章 使用 SSH 和 Telnet 的远程系统 433

# 第 14 章

# 管理用户

您需要学习的最重要的管理任务之一就是有效管理用户。无论是为自己创建单独的用户账户，还是为五口之家提供账户，甚至管理大型企业网络，其基本原理都相同。

有效管理用户包括分配和操作主目录、实施和执行良好的密码策略，以及应用安全策略（主要是文件和目录权限，但也可能涉及为用户工作磁盘空间配额）。在本章中，我们将介绍如何操作用户账户。我们还将介绍超级用户访问，通常称为 root 访问，并在 Ubuntu 的上下文中讨论它，Ubuntu 在这方面是一个相当不寻常的发行版。

## 用户账户

每个 Ubuntu 安装通常包含三种类型的账户：超级用户、日常用户和系统用户。每种类型都很重要，您必须了解各自的职责。如果不协同工作，Ubuntu 将很难做任何事情！

所有用户都必须在系统上拥有账户。Ubuntu 使用 `/etc/passwd` 文件保存用户账户信息。每个用户，无论类型如何，都有一个账户信息的一行条目存储在 `/etc/passwd` 文本文件中。每个账户条目包含一个用户名（用于登录）、一个密码字段包含 x（因为密码实际存储在 `/etc/shadow` 中）、用户 ID（UID）和组 ID（GID）。第五个字段包含可选的人类 ID 信息，例如真实姓名、办公地点、电话号码等。最后两个字段是用户的主目录位置和

## 本章内容

- 用户账户
- 管理组
- 管理用户
- 管理密码
- 向普通用户授予系统管理员权限
- 用户登录过程
- 磁盘配额
- 参考

home directory and the user's default login shell. See the “The Password File” section later in this chapter for more information.
