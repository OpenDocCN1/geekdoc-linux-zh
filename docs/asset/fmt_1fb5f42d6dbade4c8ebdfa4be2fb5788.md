
| 30 | 0 | `ID_SD` | 27 | 28 | `ID_SC` | 31 |

| 21 | 5 | `GPCLK1` | 29 | 30 | |

| 22 | 6 | `GPCLK2` | 31 | 32 | `PWMO` | 16 |

| 13 | | `PWM1` | 33 | 34 | |

| 24 | 19 | `PCM_FMS` | 35 | 36 | 17 |

| 25 | 26 | | 37 | 38 | `PCM_DIN` | 20 | 28 |

| | | | `OV` | 39 | 40 | `PCM_OUT` | 29 |

# MAKESPACE Piggio

直接在树莓派上运行并通过树莓派输出：

第二种方案稍微有点手。你需要在 Linux 机器上下载 PiScope 的二进制版本，并通过网络连接到树莓派上的守护进程。在这种情况下，请通过 `PISCO_ADDR` 环境变量检查树莓派的 IP 地址，你需要设置该变量：

```
$ wget abyz.me.uk/rpi/piggio/piscope.tar
$ tar xvf piscope.tar
$ cd piscope/
$ make
$ make install
$ ./piscope
```

```
$ wget abyz.me.uk/rpi/piggio/piscope.tar
$ tar -xvf piscope.tar
$ cd piscope/
$ export PISCO_ADDR={raspberrypi.local}
$ ./piscope.x86_64
```

这种方法直接将源代码下载到树莓派并进行现场编译。PiScope 然后将根据你使用的 Raspberry Pi OS 安装版本连接到本地守护进程，你可能需要一些依赖项。

# 结论

Piggio 库无疑是编写代码的一个有用替代方案。所有的编程语言都有封装器和模块。这些可用工具让你工作顺顺畅，并支持通过网络监控 GPIO。

在使用 Piggio 时，你会发现单个 GPIO 引脚的命名与 wiringPi 相比不同。然而，有一点非常引人注目：在一年多的时间里，该项目一直在 GitHub 上进行。我希望这很简单，因为自那之后没有看到任何更改：

在测试中，我能够在 Ubuntu 上无需任何额外操作就运行 PiScope。

# 信息

- [1] wiring 项目投影: https://web.archive.org/web/2018082314617/http://wiringpi.com/wiringpi-deprecated/
- [2] Piggio: https://abyz.me.uk/rpi/piggio/
- [3] piggio 参数: https://abyz.me.uk/rpi/piggio/piggio.html
- [4] pigs 参数: https://abyz.me.uk/rpi/piggio/pigs.html
- [5] PiScope 安装选项: https://abyz.me.uk/rpi/piggio/piscope.html

# 作者

Martin Mohr 经历了现代计算机技术的完整发展过程。大学毕业后，他主要开发 Java 应用程序。树莓派唤醒了他对电子领域的老激情。

![](img/6816acb85ab93ecedbe75e6e9cb5d00d_67_0.png)

图 2：引脚 0 到 15 在不断变化状态下的 PiScope。读取不断变化的

# 引言 LINUX 之声

ImageMagick 图像处理工具是开源工具包中的宝石之一。你可以使用 ImageMagick 从命令行调整图像。如果你有一组数字照片且它们都需要调整，既然可以使用 ImageMagick 修复它们，为什么为什么要减慢 GUI 的速度呢？但 ImageMagick 的功能远不止于编辑图像。本月，我们将为你带来一个使用 ImageMagick 和简单脚本从零开始绘图的教程。本月，我们还深入研究了 KOReader 电子阅读器，并向你介绍经典的 Linux 策略游戏《帝国时代》（Age A.D.）。

![](img/6816acb85ab93ecedbe75e6e9cb5d00d_68_0.png)

Doghouse — 算法与书籍 71

Jon "maddog" Hall

KOReader 电子阅读器 72

Dmitri Popov

回顾计算机内存的历史以及经典：算法教材。

D.A.D. 76

Daniel Tibi

KOReader 丰富的功能可以为你的简易电子书赋予新力量，并完全改变你的阅读体验。

FOSSPicks 84

Graham Morrison

用这款实时策略游戏引导古代文明的命运。

教程 — ImageMagick 90

Raf Kirschner

ImageMagick 的功能不仅仅是编辑现有图像。你可以编写一个脚本来创建一个简单的画作。

# ELVVIE

现在很好

运行 SSH 命令

哇！

仅仅三个字母

就有如此大的力量

某种意义上的终端...

我为你制作了这张表

为你提供最实用的选项

![](img/6816acb85ab93ecedbe75e6e9cb5d00d_68_1.png)

我们可以利用它创建的隧道

远程运行命令和图形程序，

传输文件，

转发端口以及更多...

LINUX-MAGAZINE.COM | LINUXPROMAGAZINE.COM 第 263 期 2022年10月 69

# 通过特刊精炼你的技能！

从我们的特刊库中了解 Shell、LibreOffice、Linux 等等。

Linux Magazine 团队创建了一系列单本，让你深入研究你感兴趣的话题。

提供纸质版或数字版。

## 查看完整库！

shop.linuxnewmedia.com

![](img/6816acb85ab93ecedbe75e6e9cb5d00d_69_0.png)

![](img/6816acb85ab93ecedbe75e6e9cb5d00d_69_1.png)

# LINUX VOICE KOREADER 电子阅读器

## 使用 KOReader 强化你的电子阅读器：玩转阅读

KOReader 提供了丰富的功能，让你的电子阅读器获得新能力，并彻底改变你的阅读体验。

作者：DMITRI POPOV

一看，KOReader [1] 看起来非常简陋。但它那平淡的界面背后隐藏着功能强大的应用程序，拥有一系列惊人的特性，从广泛的支持到内置的 SSH 服务器。通过一些技巧和创造性的思维，你可以使用 KOReader 释放设备的全部潜力。

## 首先

KOReader 带有合理的默认设置，但为了获得的阅读体验，你可能需要调整一些设置。第一件事是添加自定义字体。KOReader 支持 TrueType 字体（TTF），因此你只需要将包含 `.ttf` 文件的文件夹拷贝到电子阅读器上的 `koreader/fonts` 目录即可。要启用任何添加的字体，点击屏幕顶部打开顶部栏，然后选择 Document / Font（设置）。要设置所需的字体，长按字体条目并点击 Set as default（设置为默认）按钮。

长按配置选项将其设置为默认。例如，点击底部菜单中的 Line Spacing（行间距）选项。说到底部菜单，激活顶部栏也会打开底部菜单。这可能是设计本意，但它很快就会变成一种干扰。要禁用它，打开 Settings / Taps and gestures（设置 / 点击与手势）菜单，并禁用 Auto-show bottom menu（自动显示底部菜单）。

图 1：使用 KOReader 选择字体。

| | | | | |
|---|---|---|---|---|
| Not Serif（无衬线体） | | | | |
| Vollkorn ★ | | | | |
| < 第 3 页，共 3 页 | | 12:20 | 89% | |

图 2：禁用自动显示底部菜单功能。

| | | | | |
|---|---|---|---|---|
| With a tap（点击） | | | | |
| With a swipe（滑动） | | | | |
| Auto-show bottom menu（自动显示底部菜单） | | | | |
| | | 12:23 | 88% | |

默认情况下，当你启动 KOReader 时，它会打开文件管理器，因此你每次启动应用时都必须选择想要阅读的书。在某些情况下，让 KOReader 在应用启动时自动打开列表更为实用。打开顶部栏并切换到文件管理器。点击顶部标题打开主菜单，切换到文件管理器部分，并选择 Start | with last file（启动 | 使用上次打开的文件）。

屏幕底部的状态栏提供了有用信息，例如阅读进度、时间等。默认情况下，你可以通过点击切换页面。但你也可以通过单视图查看信息。要这样做，打开顶部栏，选择 Settings | Status Bar | Settings（设置 | 状态栏 | 设置），并启用 Show all（显示所有）。返回 Settings | Status Bar 菜单并切换所需的选项（图 3）。
