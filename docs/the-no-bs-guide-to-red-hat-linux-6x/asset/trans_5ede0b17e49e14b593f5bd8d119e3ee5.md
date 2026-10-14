

## 设置调制解调器支持

查找 `$_com2` 条目，并将其改为如下内容：

```
$_com2 = "/dev/modem"
```

如果你的调制解调器不在 COM2 上，选择对应你调制解调器端口的 `$comX` 条目。启动 DOSEmu 并测试你的调制解调器应用程序。

## 在 X Windows 下运行 DOSEmu

你可以通过在 xterm 窗口中执行 `xdos` 命令，在 X Windows 下运行 DOSEmu 会话。屏幕上会出现一个标题为“DOS in a Box”的新窗口。xdos 会话的行为应与其他任何 DOSEmu 会话相同，只是它不支持图形。

## 获取更多关于 DOSEmu 的信息

DOSEmu 的志愿开发者们正在努力修复 bug 并解决现有的兼容性问题。你可以访问 James MacLean 的 DOSEmu 主页 http://www.dosemu.org，获取 DOSEmu 的最新消息，并在新版本发布时下载。如果你是程序员，还可以了解如何为 DOSEmu 的开发工作贡献力量。

## 使用 Wine 运行 Windows 程序

Wine（Windows 模拟器——或者“Wine Is Not an Emulator”）是一个允许你在 Linux 下运行部分 Windows 3.1 和 Windows 95/98 应用程序的程序。Wine 的工作原理是拦截 Windows 程序的内部调用，并将其转换为等效的 X Windows 函数。

尽管 Wine 的开发已经取得了长足进展，但它仍被视为 alpha（实验性）代码。许多人报告说，他们不同程度地成功地在 Wine 下运行了一些较大的共享软件和商业程序，但有些程序仍然运行不佳或根本无法运行。

虽然不久之前 Wine 文档还断然声称 32 位 Windows 95/98 应用程序永远无法在 Wine 下运行，但如今许多程序已经运行得相当好。

新闻组 comp.emulators.ms-windows.wine 是查看 Wine 最新消息的最佳场所，偶尔也会有帖子介绍各种 Microsoft Windows 程序在 Wine 下运行的成功与失败案例。官方 WineHQ 网站维护着一个可搜索的数据库，收录了已在 Wine 下测试过的程序。（参见 http://www.winehq.com）

### 如何体验 Wine？

本书附带的 CD 中未包含 Wine 软件包，因为新版本的 Wine 大约每月发布两次。如果你想试用 Wine，就需要获取最新的可执行文件，并在你的 Linux 系统上配置该软件包。在 WineHQ 网站上查找与最新 Wine 版本对应的 RPM 文件，并下载到你的系统中。例如，1999 年 5 月 23 日发布的版本名为 **wine-990523-1.i386.rpm**。

### 如何运行 Wine？

你需要大约 10MB 的硬盘空间来存储 Wine 文件，并且建议你至少有 16MB 的内存和 16MB 的交换分区来运行 Wine。你还需要挂载一个安装了 Microsoft Windows 3.1 或 95/98 的 DOS 分区。

要从 **RPM** 文件安装 Wine，请执行如下命令，将 xxxx 替换为你刚下载的 Wine 文件的日期戳：

```
rpm -i wine-99xxxx-1.i386.rpm
```

安装完成后，你只需再执行一个设置步骤。编辑 /usr/local/wine.conf 文件，在 [Drive C] 部分修改 Path= 行，使其读作 Path=/dos（假设这是你为挂载的 DOS 分区指定的名称）；然后保存文件。如果你的 DOS 分区使用旧式 FAT 文件系统，请在 Filesystem 行使用 msdos 而不是 win95。

```
[Drive C]
Path=/dos
Type=hd
Label=MS-DOS
Filesystem=win95
```

要在 Wine 下运行 Microsoft Windows 程序，你必须首先使用 startx 命令进入 X Windows。在 xterm 窗口中，输入如下命令：

```
wine /path/program
```

例如，如果你想运行 Microsoft Windows 的纸牌游戏，并且已将 DOS 分区挂载为 /dos，则应输入

```
wine /dos/windows/sol.exe
```

几秒钟内，屏幕上应会出现一个纸牌游戏的新窗口（见图 12-2）。随附的所有小程序

![](img/3137cdda7122042e86dbeafe9840d4ed_301_0.png)

图 12-2：*在 Wine 窗口中的纸牌游戏*

