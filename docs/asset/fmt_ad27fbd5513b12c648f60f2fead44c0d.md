
由于 Direct3D 和 OpenGL 都试图暴露一组硬件特性，因此这两个 API 之间存在某种一致性——它们封装了相同的概念。事实上，Direct3D API 的最新版本已明显向 OpenGL 提供的接口风格移动。这是一件非常好的事，会让你的移植任务变得更容易。

接下来的章节将讨论 OpenGL 和 Direct3D API 之间的差异和相似之处。

# 294 LINUX 游戏编程

## 坐标系

OpenGL 使用右手坐标系，而 Direct3D 使用左手坐标系。然而，OpenGL 的模型矩阵（Model matrix）可以通过将 Z 轴缩放 -1 来产生左手坐标系。以下示例展示了现有的 Direct3D 坐标系，通过简单应用 `glScale()`，即可将其转换为 OpenGL 系统：

```
glMatrixMode(GL_MODELVIEW);
glLoadIdentity();
// 想要左手坐标系
glScale(1.0, 1.0, -1.0);
// 现在照常进行变换...
```

## 多边形绕向

Direct3D 将顶点按顺时针顺序排列的多边形识别为正面多边形。在 OpenGL 中，默认假设正面多边形按逆顺时针顺序定义。可以使用 `glFrontFace()` 此行为：

```
void glFrontFace(GL_Cenum mode);
```

在此语法中，`mode` 为 `GL_CW` 表示顺时针，`GL_CCW` 表示逆顺时针。

## 纹理管理

OpenGL 中的纹理是高度不透明的对象。一旦你创建了纹理并将其传入，其余工作将由系统为你处理。你不需要担心显存需求，也不需要使用传输机制将纹理数据从系统内存或其他任何潜在的硬件特定操作中移动出来。这些都交由驱动程序处理。

Direct3D 的早期版本假设程序员需要对纹理管理的细节拥有完全控制权——本质上，每个应用程序都可以提供自己的自定义纹理管理。虽然较新版本的 Direct3D 提供了类似于 OpenGL 风格的自动纹理管理，但移植使用旧系统编写的代码可能会带来一些挑战。

## OpenGL 扩展

乍一看，你可能认为 Direct3D 具有某些 OpenGL 欠缺的功能。事实上，这些功能大部分实际上是作为 OpenGL 扩展提供的。扩展以新函数或现有函数对应新枚举值的形式存在。必须进行运行时查询以确定 OpenGL 驱动程序是否支持所需的扩展。

一个很好的例子是多纹理渲染（multitexturing），硬件可以一次性执行多次渲染。如今大多数消费级 3D 显卡都具有这种能力。在 OpenGL 中，多纹理通过 `_multitexture` 扩展暴露。

通常情况下，如果 Direct3D 提供了基础 OpenGL 规范中缺失的硬件，将会有相应的 OpenGL 扩展来支持它。

位于 `http://www.opengl.org` 的 OpenGL 网站维护着关于扩展的最新信息。当然，硬件制造商也会利用可用的扩展信息，鼓励你在他们最新、强大的芯片组上支持新功能。

## 音频问题

除非原始音频代码是用跨平台 API 编写的，否则你将对原游戏的这些部分进行完全重写。好消息是，音频代码的封装得非常好。大多数游戏都有一套定义良好的音频需求：播放音效、播放音乐轨道、调整音量等。移植音频代码是在保留游戏其他部分可见的接口的同时，替换其实现。

DirectX 通过 DirectSound API 提供音频支持。这是一个相当底层的接口，围绕管理包含波形数据的音频缓冲区展开。这与 Linux 以文件为中心的音频生成方法形成某种对比，后者涉及将波形数据流向音频设备。

## 网络问题

### WINSOCK

Winsock API 提供了熟悉的 BSD 库的 Windows 实现。但它有一些可能让移植变得复杂的特殊特性。

## 文件和套接字句柄

UNIX 的“万物皆文件”方法意味着文件句柄和套接字句柄通常是可以互换的。Windows 不允许将套接字视为文件。当 UNIX 文件和套接字句柄通常只是整数时，Windows 定义了 `SOCKET` 数据类型表示套接字句柄。

当 UNIX 程序使用 `read()` 从套接字拉取数据时，Windows 对等方法必须使用套接字特定的 `recv()` 或 `WSARecvEx()`。幸运的是，

# 附录 C

## 参考文献

好了，我的朋友们，这段时光非常愉快。但美好的事物总有终结，现在就是这里。我把你们交给游戏开发这片混沌的世界，我给你们一些建议：阅读这些网站并购买本节列出的书籍。它们曾帮助过我，我相信它们也会帮助你们在游戏开发社区中成为下一个大红的人物。

### 网站

在互联网这片巨大的白色世界里，有数以百万计的专门为游戏开发者提供的网站。其中一些很棒，大多数都不行，但这里有一些比较实用的在线资源。

#### GAMEDEV.NET

```
http://www.amedev.net
```

这可能是对业余开发者最好的资源，该网站涵盖了从每日新闻到参考资料和留言板的所有内容。它由业余开发者为业余开发者创建，包含了游戏编程初学者所需的一切。此外还提供 GDN 邮件服务（`http://www.gnmail.com`），这是一个免费的 Web 系统，让人们知道你是一个游戏程序员。

#### GAMASUTRA

```
http://www.gamasutra.com
```

这个网站资金充足，有来自游戏开发领域一些大咖的支持和定期文章。该网站设有定期发布热门游戏的复盘报告、行业观点以及一个吸引了业内最顶尖开发者的留言板。

#### FLIPCODE

```
http://www.flipcode.com
```

尽管 Flipcode 为游戏开发社区提供了许多服务，但它也吸引了一个类似 slashdot 这种风格的喷子社区。但不要让这让你望而却步，因为这个网站包含了一些高级文章和其他值得搜索的内容。Flipcode 是 FutureGaming 网络的一部分。

#### HAPPY PENGUIN

```
HTTP://HAPPYPENGUIN.ORG
```

这个网站提供 Linux 游戏开发新闻和资源。该网站包含了几乎所有已知的 Linux 游戏。该网站还提供了关于如何在 WINE (`http://winehq.org`) 下运行各种游戏的教程链接。

#### INDREMA DEVELOPER NETWORK

```
HTTP://INDREMA.COM
```

这个网站是即将推出的 Linux 游戏机 L600 开发者端的门户。虽然这个网站运行速度有点慢，但它包含的邮件列表多到你可以挥一根大尖棍来数。

#### LINUX GAMES

```
HTTP://LINUXGAMES.COM
```

我不确定这个网站是做什么的。它提供了针对 Linux 游戏开发两个方面的良好混合内容，绝对值得一看。

#### LINUX GAME DEVELOPER RESOURCE CENTRE

```
HTTP://SUNSITE.AUC.DK/LGDC
```

LGDC 托管在最强大的 Web 网络之一上，提供了一系列精彩的链接和文章，还偶尔对 Linux 社区的大大人物进行采访。

### 书籍

没有书的图书馆是不完整的。为了帮助你填满那些架子，这里有一些关于游戏编程各个方面的实用指南，以及其他一些参考资料。

#### OPENGL 超圣经（红书）

任何 3D 程序员的必读之，这本书涵盖了从变换到凹凸贴图的所有内容。

#### OPENGL 参考指南（蓝书）

OpenGL 手册页的打印版。

#### 图形编程黑书（GRAPHICS PROGRAMMING BLACK BOOK）

作者：Michael Abrash (Coriolis)

ISBN 1-56710-174-6

这是图形程序员的圣经。除了 Abrash 生活中趣味性的轶事，这本书还涵盖了从抗锯齿到底层优化的所有技术。

#### 游戏架构与设计（GAME ARCHITECTURE AND DESIGN）

作者：Andrew Rollings 和 Dave Morris (Coriolis)

ISBN 1-56710-425-7

这本书涵盖了设计的每一个方面，从团队分配到界面规划。

#### TCP/IP 图解（第二卷）（TCP/IP ILLUSTRATED VOLUME 2）

作者：Richard W. Stevens

由已故的 TCP/IP 大师编写，这本书涵盖了所有可能需要的调用。

#### Linux 设备驱动（LINUX DEVICE DRIVERS）

作者：Alessandro Rubini (O'Reilly)

ISBN 1-56592-292-1

如果你想在 Linux 下进行底层工作，了解内核如何工作以及任务优先级将帮助你从代码中榨出每一丝性能。

#### 游戏开发系列（GAME DEVELOPMENT SERIES）

作者：各种（Prima Publishing）

ISBN（各种）

你手中的这本书只是 Prima 出版不断增长的游戏开发书籍系列之一。

### 杂志

#### 游戏开发者杂志（GAME DEVELOPER MAGAZINE）

```
http://www.gomag.com
```

由带来 GameSutra 的同仁推出了《游戏开发者杂志》。这杂志基本上是网站的纸质版，充满了实用的技术和行业新闻。

#### DEVELOP

《游戏开发者杂志》的英国版，Develop 在被购买 MCV 的人员收购后由 Future Publishing 出版。

#### EDGE

```
http://www.futurenet.com
```

由 Future Publishing 出版，这杂志更适合对开发方面感兴趣的玩家。

# 报纸

如果没有行业更新，我们将处于何种地？除了 Web 之外，许多公司倾向于在将信息发布到网站之前，先向传统媒体发布新闻稿。

# 计算机贸易每周周刊 (COMPUTER TRADE WEEKLY)

CTW 充满了行业新闻，从谁聘佣了谁到零售商应该在货架上摆放哪些游戏。如果你对游戏开发的业务方面感兴趣，这份报纸绝对适合你。对英国开发者免费。

# MCV

MCV 充满了行业新闻，从谁聘佣了谁到零售商应该在货架上摆放哪些游戏。如果你对游戏开发的业务方面感兴趣，这份报纸绝对适合你。对英国开发者免费。

# 计算机每周周刊 (COMPUTER WEEKLY)

Computer Weekly 是一份面向整个 IT 行业的周刊，而不仅仅是游戏。它对英国 IT 专业人士免费，拥有一个相当不错的招聘板块。

# 计算机 (COMPUTING)

与 Computer Weekly 一，Computing 杂志并不严格针对游戏行业，但它确实能让你跟上整个 IT 行业的现状。

# 新闻组 (NEWSGROUPS)

最好的新闻组通常包含在 `rec.games.*` 和 `comp.games.*` 组中。请注意，许多人更倾向于邮件列表而不是新闻组，因为那里没有垃圾邮件机器人。

# 邮件列表 (MAILING LISTS)

你应该加入的明显邮件列表是 LGDC 邮件列表（`http://sunsite.auc.dk`）。

Indrema 和 ColabNET 还针对各种主题运行了一些与 Indrema 相关的列表。你可以在 IDN 网站（`http://idn.indrema.com`）订阅所有这些列表。

# 附录 D

# 术表

## ALSA

ALSA (高级 Linux 音效架构)。一组用于 Linux 的音频驱动程序，支持 OSS 仿真。

## BeOs

BeOs。一种多媒体操作系统。

## Blender

Blender。一个免费软件的 3D 建模和可视化软件包；最新版本包含一个游戏引擎。

## BSD

BSD。根据 BSD 许可证分发的 UNIX 版本。

## BSD Sockets

BSD Sockets。一种 TCP/IP 编程 API。

## 客户端 (Client)

客户端。一个连接到服务器的程序。在 X Windows 下运行的游戏就是一个客户端程序。

## 控制台 (Console)

控制台。a) Linux 上的文本模式界面。b) 一个家庭娱乐系统。

## 著权共享 (Copyleft)

著权共享。传统版权的替代方案。它与较低的分发限制有关。

## CVS

CVS (并发版本系统)。一个允许用户共享和编辑源码的系统。

## Debian HURD

Debian HURD。一种类 Unix 系统，类似于 Linux，但它使用模块化微内核而不是单体内核。

## DRM

DRM (数字权利管理)。一种旨在防止 Indrema L600 控制机上软件盗版的系统。

## DV Linux

DV Linux。一种特殊的 Linux 发行版，旨在确保 Indrema 游戏可以在运行 DV Linux 的标准 Linux 设备上运行。

## E

**Eric S. Raymond.** OpenSource.org 的创始人，开源运动公认的大师。

## F

**自由软件基金会 (Free Software Foundation)。** 一个促进使用自由软件的组织。

**FreeBSD。** *参见* BSD。

**Freshmeat。** 一个 Linux 软件目录，位于 `http://www.freshmeat.net`。

## G

**GameDev.Net.** 面向所有水平游戏开发者的在线参考，位于 `http://www.gamedev.net`。

**GDNet。** *参见* GameDev.Net。
