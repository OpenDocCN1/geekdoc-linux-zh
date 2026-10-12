
```
$ hourly.r
        artistName     hour   x
19          Rainbow    0     4
28          Sparkys    1     9
30          Sparkys    2    10
31          Sparkys    3    14
32          Sparkys    4     7
33      The Killers    6     1
36  Eros Ramazzotti    7     7
40 Adriano Celentano    8     1
48  Eros Ramazzotti    9     4
56          Alice   10     1
59     Ace of Base   11     1
64     Ace of Base   12     1
68     Amy Winehouse  13     3
72    Foster The People 14     4
75        The Monkees  15     2
76     Ace of Base   16     3
111  Eros Ramazzotti  17     5
161         Falco   18     7
243        Guster   19     7
349   Linkin Park   20    11
460       Jan Delay  21     9
596       Jan Delay  22    10
782   Element of Crime  23    12
```

##### 图 7：哪些艺术家在什么时间被播放的频率最高？

![](img/e3f454b04d121b3750fddfda8dd21e_47_0.png)

##### 图 8：Spotify – 错误地 – 认为作者是浅色啤酒爱好者。

第 10 行根据方括号中指定的 `order()` 函数对之前生成的 `agg` 数据框进行排序。其第一个参数是小数值字段名（正值）；第二个是计数器的负值，由 `length` 函数确定。在 R 中，由聚合函数新建的列名为 `x`，在此情况下包含结果的数量。

第 11 行对现在名为 `winners` 的数据框运行 `recode` 语句，并使用 `ldup1|cat(d winners[2])` 来指定第二个字段（即小小时值；R 数组索引始终从 1 开始，而不是 0）在结果中必须仅出现一次。因此，该函数仅保留之前正向排序的最高结果（针对具有相关艺术家的小小时值），并丢弃所有其他结果。

这样就解决了 Perlmeister Studios 中最受欢迎乐队列表（作为一天中时间的函数）的问题！图 7 展示了 `hourly.r` 程序的输出（代码列表 4）。午夜过后，要么是尴尬的 1980 年代老歌（Rainbow；我记得模糊地，从凌晨 1:00 到 4:00，每一首都是乐队 Sparks 的曲目），在制作了一部关于该乐队的 Netflix 纪录片后，随后连续播放了四个小时的他们歌曲。第二天的工作当然很糟糕，但你只活一次。

根据经验，用户可能会花几天时间摆弄 R 来找到合适的数据结构和方法，而往往只需三行代码就能实现他们想要的结果。造成这种情况的原因可能包括该语言的年龄，它带有一种反 Python 的心态（“你的意思是一种方法就够了？”），以及自首次发布以来几十年间以不协调的方式发布的许多包。针对特定问题的 Google 搜索通常会揭示解决同一问题的三种或四种不同方法。Robert I. Kaboff 的培训书籍 [1] 很好地解释了一些基本过程，但它绝不是一个全面的参考手册。

#### 更多秘密

如果你在 Spotify 档案的 ZIP 文件中进一步挖掘，你很可能会挖掘出更多的数据宝藏。例如，Spotify 的 `Inferences.json` 文件包含关于用户的既定事实 – presumably 是为了帮助 Spotify 提供听众也会响应的合适广告。

就我的情况而言，Spotify 假设我对“浅色啤酒”有偏好（图 8），这是一个玩笑且完全错误 – 如果有紧急情况，任何认识我的人都作证！这是 Bud Light 广告开始出现在我屏幕上的可能解释。

#### 信息

- 1. Kaboff, Robert I. *R in Action, Second Edition*. Manning, May 2015: [https://www.manning.com/books/r-in-action-second-edition](https://www.manning.com/books/r-in-action-second-edition)

### 想要随时随地工作？

![](img/e3f454b04d121b3b3750fddfda8dd21e_48_0.png)

立即查找远程工作！

**开源工作中心**

opensourcejobhub.com/

### 深入解析

![](img/e3f454b04d121b3b3750fddfda8dd21e_49_0.png)

#### 用 unsnap 交换 snaps 为 Flatpaks

#### 软件包交换

如果你想远离 Ubuntu 的 Snap 软件包格式，`unsnap` 脚本会从你的计算机中移除 snaps，并在可能的情况下用 Flatpaks 替代它们。**作者：Ferdinand Thormoes**

Linux 社区与其他社区一样，并不特别擅长欢迎新事物。大多数人希望维持现状。用哲学家伏尔泰的话说，好的是更好的敌人。没有什么比放弃好的去追求更好的更危险了。

Systemd，这个仍有争议的系统和服务管理器，阐明了这一概念。其他例子包括新的软件包系统 Flatpak、Snap 和 AppImage，*Linux Magazine* 曾在 2022 年 12 月 [1] 对此进行过报道。这些软件包系统在 Linux 社区中并未得到一致认可。特别是 Snap 格式，Canonical 最初将其设计用于云应用和物联网（IoT），但后来移植到桌面应用，除了对新软件包系统的基本批评外，还面临着反对。

如果你对 Snap 感到失望，`unsnap` 脚本可以帮助你替换在 Ubuntu 及其衍生版中可用的 snaps 为 Flatpaks。

#### 糟糕的经历

Linux 社区对 Canonical 的任何单独努力都持怀疑态度，因为有过糟糕的过去经历。对 Snap（图 1）的主要批评是 Snap Store 的专有后端 [2]，以及 Canonical 越来越强地在 Ubuntu 中推广该格式，且没有官方方法来移除 snaps。

Snap 守护进程（`snapd`）是从 Canonical 服务器检索 snaps 及相关元数据的定义工具。此外，snaps 存在功能缺陷，公司一直缓慢地消除这些缺陷。另一方面，Flatpak 受到替代软件包系统拥护者的欢迎。Flatpak 可能是

![](img/e3f454b04d121b3b3750fddfda8dd21e_49_1.png)

**图 1：** 当你通过 *Ubuntu 软件* 安装程序时，可以通过右上角的选择框定义来源。某些软件包（如 Firefox）通常仅以 snaps 形式提供。

大多数 Ubuntu 环境外部用户的选择。这最终可能导致 Canonical 再次搁置 Snap，正如过去常发生的那样，例如 Ubuntu Touch 或 Mir 显示管理器。

这种情况导致一些发行版拒绝甚至阻止 snaps。一个突出的例子是基于 Ubuntu LTS 的 Linux Mint，其开发者早在 2020 年就决定不交付 snaps [3]。他们还宣布，从版本 20 开始，Linux Mint 将通过图形软件包管理器主动防止安装 Snap 框架，防止通过后台将 snaps 自动发送到用户系统。笔记本电脑制造商 System76 [Pop!_OS] 和 Tuxedo（Tuxedo OS 1）也避免在其 Ubuntu 衍生版中附带 snaps。甚至 Ubuntu 用户也没有响应 Snap，正如许多指南所建议的那样，描述在 Ubuntu 中作为 DEB 安装 Firefox。

#### unsnap

前 Snap 共同开发者 Alan Pope，在该公司工作了 10 年后于 2021 年离开 Canonical，开发了 `unsnap` [4]，一个在可用时将 snaps 替换为 Flatpaks 的脚本。该脚本托管在 GitHub 上，开发者已测试其在提供 snap 和 Snap 格式软件包的 Ubuntu 及所有衍生版上的使用。

为了在新安装的 Ubuntu 22.04 LTS 上测试 `unsnap`，我除了现有的 snaps 外，还通过 Ubuntu 软件包管理器设置了一些来自 Snap Store 的软件包，然后列出来以确保（图 2）。然后我从 GitHub 下载了 `unsnap` 脚本。为此，我首先必须安装 `git` 包，然后运行代码列表 1 中的命令。
