

下载文件后，打开命令行并输入以下内容：

```
$ sudo sh quake4-linux-1.0*.run
```

然后按 Enter。安装程序启动并询问你几个问题。回答后，安装程序会创建必要的文件和文件夹。你只需将 DVD 上 /quake4/q4base 目录中的几个文件复制到 /usr/local/bin/quake4/q4base。你可以通过在命令提示符下输入 quake4 来启动游戏。

## Wolfenstein: Enemy Territory

与早期的《Castle Wolfenstein 归来》既支持单人又支持多人不同，免费提供的《Wolfenstein: Enemy Territory》仅支持多人游戏（参见图 9.6）。该游戏提供 Win32 和 Linux 原生版本，你可以从 http://www.splashdamage.com/ 下载。下载完名为 et-linux-2.55.x86.run 的 260MB 文件后，通过输入以下命令安装游戏：

```
$ sudo sh et-linux-2.55.x86.run
```

![](img/8f9e74e2b343ff525bebfb720a3d8441_232_0.png)

图 9.6  在这个精美但充满敌意的图形环境中，团队合作是取得胜利的关键。

然后接受默认设置。`/usr/local/bin` 中存在一个指向加载游戏脚本的符号链接。

## Battle for Wesnoth

当然，Linux 游戏远不止第一人称射击游戏。目前最受欢迎的 Linux 游戏之一是《Battle for Wesnoth》（参见图 9.7），这是一款策略游戏，很像《帝国时代》。背景设定在一个幻想大陆，你负责组建军队与敌人作战。

![](img/8f9e74e2b343ff525bebfb720a3d8441_233_0.png)

图 9.7  通过《Battle for Wesnoth》锻炼你的战略思维——一个丰富而完整的幻想冒险世界

《Battle for Wesnoth》在 Ubuntu 上安装非常容易。你只需使用 synaptic 或 aptitude 选择 wesnoth 包。安装后，你可以通过命令行输入以下内容启动它：

```
$ wesnoth
```

## 使用 Cedega 玩 Windows 游戏

如前所述，操作系统的应用软件决定了其大众市场的吸引力。一群开发者看到绝大多数计算世界都在使用基于 Windows 的生产力和游戏软件，于是

决定开发一种在 Linux 上运行这些软件的方法，从而让 Linux 用户能够使用这一庞大的应用库。开发者创建了一个名为 Wine 的程序，该程序定期更新，并构成了名为 Cedega 的游戏变体的基础。这是一款由开发者 TransGaming Technologies（http://www.transgaming.com/）提供的商业产品，因此你无法通过 aptitude 获取它。

然而，Cedega 是一款流行且更新及时的产品，支持《上古卷轴 IV：湮灭》和《魔兽世界》等最新发行作品。由于 Cedega 的状态不断变化，TransGaming Technologies 提供订阅服务，这意味着代码发布时你会获得更新——确保你不仅能享受今天的游戏，也能享受明天的游戏。

因此，如果你等不及 Linux 变得更受游戏开发者欢迎，就可以使用 Cedega 作为过渡，直到他们被说服直接支持 Linux。

## TIP

在 Linux 中成功游戏的关键是始终彻底阅读文档，始终彻底研究互联网资源，并始终了解你的系统。安装游戏是学习系统的绝佳方式，因为成功的回报非常有趣。

## Reference

- http://www.transgaming.com/—TransGaming Technologies 官方网站提供在 Cedega 下直接支持的游戏详情。
- http://www.linuxgames.com/—关于 Linux 游戏现状的最新信息的良好来源。
- http://zerowing.idsoftware.com/linux/doom/—包含在 Linux 下运行 DOOM 3 的完整操作指南和故障排除指南。
- http://www.unrealtournament.com/—《无敌浩劫》官方网站。
- http://www.nvnews.net/vbulletin/forumdisplay.php?f=14—官方 Nvidia Linux 驱动支持论坛。
- http://www.nvidia.com/object/linux.html—Nvidia Linux 驱动程序主页。
- http://tinyurl.com/3pm2v—ATI Linux 驱动程序主页（由 tinyurl.com 提供）。

