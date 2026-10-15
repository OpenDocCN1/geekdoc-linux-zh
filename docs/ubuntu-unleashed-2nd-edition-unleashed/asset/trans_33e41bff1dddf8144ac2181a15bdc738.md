

```
$ fglrxinfo
display: :0.0  screen: 0
OpenGL vendor string: ATI Technologies Inc.
OpenGL renderer string: RADEON 9600 XT Generic
OpenGL version string: 2.0.5814 (8.25.18)
```

Ubuntu 现在允许你使用 synaptic 同时安装 Nvidia 和 ATI 驱动程序。你只需要找到 linux-restricted-modules 以及 xorg-driver-fglrx 或 nvidia-glx，就能轻松完成安装。

## 安装 DOOM 3

臭名昭著的 DOOM 和 DOOM II 的续作于 2004 年下半年发布（见图 13.2），它提供了一种在 Linux 下运行的方法。你仍然需要购买 Windows 版本，因为你需要光盘上的一些文件。其余文件可从 id Software 的 http://zerowing.idsoftware.com/linux/doom 获取。你也可以在那里找到有关显卡的其他信息。

![](img/e464b828c497c99e41f61d4c55f1c0db_287_0.png)

**FIGURE 13.2.** Descending into the pits of hell. DOOM 3 is one of the most graphic computer games available.

你可以从 id Software 的 FTP 服务器下载文件 doom3-linux-*.run，或使用 BitTorrent。当下载完成后，打开一个终端并切换到保存该文件的目录。输入以下命令：

```
# sh doom3-linux-*.run
```

这将开始演示的安装。与其他商业游戏一样，在安装前你必须同意 EULA。按照安装步骤进行。当安装完成后，你需要准备好 Windows 光盘。

你需要复制的文件如下：

- pak000.pk4
- pak001.pk4
- pak002.pk4
- pak003.pk4
- pak004.pk4

它们必须保存在 /usr/local/games/doom3/base/ 目录中。复制文件后，你可以通过输入 doom3 启动游戏，或通过输入 doom3-dedicated 启动多人游戏的专用服务器。

## 安装 Unreal Tournament 2004

Epic 出品的 Unreal Tournament 2004（或亲切地称为 UT2004）在 32 位和 64 位版本中都原生支持 Linux（见图 13.3）。请注意，如果你运行 64 位版本，需要确保你的图形驱动程序在 64 位模式下得到支持。

![](img/e464b828c497c99e41f61d4c55f1c0db_288_0.png)

FIGURE 13.3 Unreal Tournament 2004 builds on the classic deathmatch scenario with more enemies and more combatants!

安装很简单，有两种方法。你可以插入 DVD 并挂载它，或在 GNOME 中打开 DVD 并双击 linux-installer.sh 图标。当被问及是否要运行它或显示其内容时，点击 Run in Terminal 以启动图形安装程序。与 DOOM 3 一样，你必须下载并接受 EULA 条款后才被允许安装 UT2004。你可以选择要安装软件的位置；默认位置在你的主目录中。选择目标目录后，点击 Begin Install；UT2004 会完成其余工作。

通过命令行访问图形安装程序的另一种方法是：切换到 `/media/cdrom/` 目录并输入以下内容：

```
$ sh linux-install.sh
```

这会启动图形安装程序。继续操作，完成后，你应该能在 `/home/username/ut2004` 中找到 Unreal Tournament 2004。

如果你想卸载 UT2004，可以使用 `ut2004` 目录中的卸载脚本。输入以下命令：

```
$ sh uninstall.sh
```

确认后，Unreal Tournament 将从你的系统中移除。

## 安装 Quake 4

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

