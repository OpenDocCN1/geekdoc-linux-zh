
安装很简单，有两种方式。你可以插入 DVD 并挂载它，或者在 GNOME 中打开 DVD，然后双击 `linux-installer.sh` 图标。当系统询问你是要运行它还是显示其内容时，点击“在终端中运行”以启动图形化安装程序。与《DOOM 3》一样，你必须阅读并接受 EULA（最终用户许可协议）的条款，才能获准安装 UT2004。你可以选择软件的安装位置；默认位置是你的主目录。选择目标目录后，点击“开始安装”，剩下的工作就由 UT2004 自己完成了。

另一种启动图形化安装程序的方式是通过命令行。将目录切换到 `/media/cdrom/`，然后输入以下命令：

```
$ sh linux-install.sh
```

这会启动图形化安装程序。一路继续下去，完成后，你应该能在 `/home/username/ut2004` 目录下找到《Unreal Tournament 2004》。

如果你想卸载 UT2004，可以使用 `ut2004` 目录中的卸载脚本。输入以下命令：

```
$ sh uninstall.sh
```

确认之后，Unreal Tournament 就会从你的系统中移除。

## Quake 4

由于基于 DOOM 3 引擎，你几乎可以预期《Quake 4》（见图 9.5）会自带对 Linux 的良好支持。要开始安装，你必须拥有该软件的 Windows 版本，因为你需要几个文件以及 CD 密钥才能运行游戏。不过，首先要做的事是前往 http://zerowing.idsoftware.com/linux/quake4/ 下载所需的 Linux 安装程序（`quake4-linux-1.0*.run`），可以通过直接 FTP 下载，也可以使用更节省带宽的 BitTorrent 下载。

下载完成后，进入命令行并输入以下命令：

```
$ sudo sh quake4-linux-1.0*.run
```

然后按下回车键。安装程序启动后，会问你几个问题。你回答这些问题后，安装程序会创建必要的文件和文件夹。你只需将 DVD 上 `/quake4/qbase` 目录中的几个文件复制到 `/usr/local/bin/quake4/qbase`。之后，你可以在命令提示符下输入 `quake4` 来启动游戏。

## Wolfenstein: Enemy Territory

早期的《Return to Castle Wolfenstein》同时支持单人模式和多人模式，而免费提供的《Wolfenstein: Enemy Territory》则仅支持多人模式（见图 9.6）。该游戏提供 Win32 和 Linux 原生版本，你可以从 http://www.SplashDamage.com/ 下载。下载名为 `et-linux-2.55.x86.run` 的 260MB 文件后，输入以下命令进行安装：

```
$sudo sh et-linux-2.55.x86.run
```

然后接受默认设置。`/usr/local/bin` 中会有一个指向加载游戏脚本的符号链接。

![](img/7aaa8e4f2209bf9f2fb443905096e94c_217_0.png)

图 9.5 基于广受欢迎的 DOOM 3 引擎，《Quake 4》让你对抗邪恶的 Strogg。出去把他们轰成渣！

![](img/7aaa8e4f2209bf9f2fb443905096e94c_217_1.png)

图 9.6 在这个葱郁但充满敌意的图形环境中，团队合作是取胜的关键。

## Battle for Wesnoth

当然，Linux 游戏远不止第一人称射击游戏。目前 Linux 上最流行的游戏之一是《Battle for Wesnoth》（见图 9.7），这是一款策略游戏，风格与《帝国时代》很相似。游戏设定在一个奇幻大陆上，你负责组建军队与敌人作战。

《Battle for Wesnoth》在 Ubuntu 上安装起来很容易。你需要使用 `synaptic` 或 `aptitude` 选择 `wesnoth` 软件包。安装完成后，你可以在命令行中输入以下命令启动它：

```
$ wesnoth
```

![](img/7aaa8e4f2209bf9f2fb443905096e94c_218_0.png)

图 9.7 通过玩《Battle for Wesnoth》来锻炼你的战略头脑——一个充满奇幻与冒险的丰富世界。

## 使用 Cedega 玩 Windows 游戏

如前所述，一个操作系统能否吸引大众市场，关键在于其可用的应用程序。一群开发者注意到，计算世界中的绝大多数人都在使用基于 Windows 的生产力软件和游戏软件，于是决定开发一种在 Linux 上运行这些软件的方法，从而让 Linux 用户也能访问这个庞大的应用库。这些开发者提出了一个名为 Wine 的程序，它定期更新，并构成了游戏变体 Cedega 的基础。这是一个商业产品，由开发商 TransGaming Technologies（http://www.transgaming.com/）提供，因此你无法使用 `aptitude` 获取它。

