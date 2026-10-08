
```
[esp+8] pause on condition
log always
log arguments on condition (这一切可以在暂停调试器的情况下完成（动态插入））现在去 regedit 并运行一下，OllyDbg 将中断并带有所有其他字符串，如下所示
```

| Address | Message |
| --- | --- |
| 7DDAAF | COND: log Subkey = 0007FC8 "SYSTEM\CurrentControlSet\Services\asw" |
| 7DDAAF | COND: log Subkey = 0007FC8 "SYSTEM\CurrentControlSet\Services\asw" |
| 7DDAAF | COND: log Subkey = 0007FC8 "SYSTEM\CurrentControlSet\Services\asw" |
| 7DDAAF | COND: log Subkey = 0007FC8 "SYSTEM\CurrentControlSet\Services\asw" |
| 7DDAAF | COND: log Subkey = 0007FC8 "SYSTEM\CurrentControlSet\Services\asw" |
| 7DDAAF | COND: log Subkey = 0007FC8 "SYSTEM\CurrentControlSet\Services\asw" |
| 7DDAAF | COND: log Subkey = 0007FC8 "SYSTEM\CurrentControlSet\Services\asw" |
| 7DDAAF | COND: log Subkey = 0007FC8 "SYSTEM\CurrentControlSet\Services\asw" |
| 7DDAAF | COND: log Subkey = 0007FC8 "SYSTEM\CurrentControlSet\Services\asw" |
| 7DDAAF | COND: log Subkey = 0007FC8 "SYSTEM\CurrentControlSet\Services\asw" |
| 7DDAAF | COND: log Subkey = 0007FC8 "SYSTEM\CurrentControlSet\Services\asw" |
| 7DDAAF | COND: log Subkey = 0007FC8 "SYSTEM\CurrentControlSet\Services\asw" |
| 7DDAAF | COND: log Subkey = 0007FC8 "SYSTEM\CurrentControlSet\Services\asw" |
| 7DDAAF | COND: log Subkey = 0007FC8 "SYSTEM\CurrentControlSet\Services\asw" |
| 7DDAAF | COND: log Subkey = 0007FC8 "SYSTEM\CurrentControlSet\Services\asw" |
| 7DDAAF | COND: log Subkey = 0007FC8 "SYSTEM\CurrentControlSet\Services\asw" |
| 7DDAAF | COND: log Subkey = 0007FC8 "SYSTEM\CurrentControlSet\Services\asw" |
| 7DDAAF | COND: log Subkey = 0007FC8 "SYSTEM\CurrentControlSet\Services\asw" |
| 7DDAAF | COND: log Subkey = 0007FC8 "SYSTEM\CurrentControlSet\Services\asw" |
| 7DDAAF | COND: log Subkey = 0007FC8 "SYSTEM\CurrentControlSet\Services\asw" |
| 7DDAAF | COND: log Subkey = 0007FC8 "SYSTEM\CurrentControlSet\Services\asw" |
| 7DDAAF | COND: log Subkey = 0007FC8 "SYSTEM\CurrentControlSet\Services\asw" |
| 7DDAAF | COND: log Subkey = 0007FC8 "SYSTEM\CurrentControlSet\Services\asw" |
| 7DDAAF | COND: log Subkey = 0007FC8 "SYSTEM\CurrentControlSet\Services\asw" |
| 7DDAAF | COND: log Subkey = 0007FC8 "SYSTEM\CurrentControlSet\Services\asw" |
| 7DDAAF | COND: log Subkey = 0007FC8 "SYSTEM\CurrentControlSet\Services\asw" |
| 7DDAAF | COND: log Subkey = 0007FC8 "SYSTEM\CurrentControlSet\Services\asw" |
| 7DDAAF | COND: log Subkey = 0007FC8 "SYSTEM\CurrentControlSet\Services\asw" |
| 7DDAAF | COND: log Subkey = 0007FC8 "SYSTEM\CurrentControlSet\Services\asw" |
| 7DDAAF | COND: log Subkey = 0007FC8 "SYSTEM\CurrentControlSet\Services\asw" |
| 7DDAAF | COND: log Subkey = 0007FC8 "SYSTEM\CurrentControlSet\Services\asw" |
| 7DDAAF | COND: log Subkey = 0007FC8 "SYSTEM\CurrentControlSet\Services\asw" |
| 7DDAAF | COND: log Subkey = 0007FC8 "SYSTEM\CurrentControlSet\Services\asw" |
| 7DDAAF | COND: log Subkey = 0007FC8 "SYSTEM\CurrentControlSet\Services\asw" |
| 7DDAAF | COND: log Subkey = 0007FC8 "SYSTEM\CurrentControlSet\Services\asw" |
| 7DDAAF | COND: log Subkey = 0007FC8 "SYSTEM\CurrentControlSet\Services\asw" |
| 7DDAAF | COND: log Subkey = 0007FC8 "SYSTEM\CurrentControlSet\Services\asw" |
| 7DDAAF | COND: log Subkey = 0007FC8 "SYSTEM\CurrentControlSet\Services\asw" |
| 7DDAAF | COND: log Subkey = 0007FC8 "SYSTEM\CurrentControlSet\Services\asw" |
| 7DDAAF | COND: log Subkey = 0007FC8 "SYSTEM\CurrentControlSet\Services\asw" |
| 7DDAAF | COND: log Subkey = 0007FC8 "SYSTEM\CurrentControlSet\Services\asw" |
| 7DDAAF | COND: log Subkey = 0007FC8 "SYSTEM\CurrentControlSet\Services\asw" |
| 7DDAAF | COND: log Subkey = 0007FC8 "SYSTEM\CurrentControlSet\Services\asw" |
| 7DDAAF | COND: log Subkey = 0007FC8 "SYSTEM\CurrentControlSet\Services\asw" |
| 7DDAAF | COND: log Subkey = 0007FC8 "SYSTEM\CurrentControlSet\Services\asw" |
| 7DDAAF | COND: log Subkey = 0007FC8 "SYSTEM\CurrentControlSet\Services\asw" |
| 7DDAAF | COND: log Subkey = 0007FC8 "SYSTEM\CurrentControlSet\Services\asw" |
| 7DDAAF | CALL to RegOpenKeyEx from regedit.010B2 |
| | key = HKLM_MACHINE |
| | Subkey = "SYSTEM\CurrentControlSet\Services" |
| | Reserved = 0 |
| | Access = 000000 |
| | Conditional breakpoint at ADVAPI32.RegOpenEx |

标签: windbg (上一个)

# Android

跳转到问题，由 user 提供

[Android](https://en.wikipedia.org/wiki/Android) 是 Google 用于移动设备的软件，由 Google 和 [开放手机联盟](https://en.wikipedia.org/wiki/Open_Handset_Alliance) 开发。移动设备的软件，由 Google 和开放手机联盟开发。关于非逆向工程，请参阅 Android Enthusiasts Exchange 网站。

Android 是一个基于 Linux 的操作系统，主要为智能手机和平板电脑等触摸屏移动设备设计。最初由 Android, Inc. 开发（Google 提供了资金支持并于 2005 年收购），Android 随着开放手机联盟的成立而面世：开放手机联盟是一个致力于移动设备开放标准的硬件、软件和电信公司联盟。第一部 Android 手机于 2008 年 10 月上市。

Android 是开源的，Google 根据 Apache License 发布代码。此开源代码允许设备制造商、无线运营商和爱好者自由地修改和分发。此外，Android 拥有庞大的开发者社区编写应用程序（“应用”）来扩展设备功能，主要使用 Java 编程语言的自定义版本编写。2012 年 10 月，Android 大约有 700,000 个可用应用，从 Android 应用商店 Google Play 下载的应用程序数量估计为 250 亿。

# Android 版本

- 1.0 Astro（Google 指定为 BASE）
- 1.1 Bender（Google 指定为 BASE_1_1）
- 1.5 [Cupcake](https://en.wikipedia.org/wiki/Android_1.5)
- 1.6 [Donut](https://en.wikipedia.org/wiki/Android_1.6)
- 2.0/2.1 [Eclair](https://en.wikipedia.org/wiki/Android_2.0)
- 2.2 [Froyo](https://en.wikipedia.org/wiki/Android_2.2)
- 2.3 [Gingerbread](https://en.wikipedia.org/wiki/Android_2.3)
- 3.0/3.1/3.2 [Honeycomb](https://en.wikipedia.org/wiki/Android_3.0)
- 4.0 [Ice Cream Sandwich](https://en.wikipedia.org/wiki/Android_4.0)
- 4.1/4.2 [Jelly Bean](https://en.wikipedia.org/wiki/Android_4.1)

官方 API 文档

- Android 2.3.3 Gingerbread
- Android 2.3.4 Gingerbread
- Android 3.0 Honeycomb
- Android 3.1 Honeycomb
- Android 3.2 Honeycomb
- Android 4.0 Ice Cream Sandwich
- Android 4.0.3 Ice Cream Sandwich
- Android 4.1 Jelly Bean
- Android 4.2 Jelly Bean

# 

- [Google Play](https://play.google.com/store)

# 源代码与构建

- [源代码](https://source.android.com/)
- [源代码镜像](https://source.android.com/mirrors)
- [构建与运行](https://developer.android.com/guide/build)
- [为设备构建](https://developer.android.com/guide/build)
- [构建内核](https://kernel.android.org/)

# 开发者

- [Android 开发者](https://developer.android.com/) 包含 SDK 下载、文档、类引用和教程。从这里开始。
- [Android 开发者博客](https://developer.android.com/) Google 为 Android 开发者提供的博客，讨论技术主题以及与 Google Play（原 Android Market）相关的话题。
- [Android 官方博客](https://blog.android.com/) Android 团队的新闻和笔记
- [Google 的 Android 开发者](https://developer.android.com/) Android 团队面向开发者的新闻和公告。也是讨论近期新闻和公告的场所。
- [Android 设计指南](https://material.material.io/design) Android 的 UI 指南集。主要侧重于设计模式和导航。
- [Twitter  @AndroidDev](https://twitter.com/androiddev) Android 团队面向开发者的新闻和公告。
- [Android 开发者 Google Groups](https://groups.google.com/g/android-dev) Android 的备选开发者论坛。

- Android 开源项目（也称为 AOSP）
包含关于 Android 源代码的所有必要信息。

- 维基百科上的 Android 页面
关于 Android 系统的详细信息。

- Android.com
关于 Android 系统的通用性信息。

- Google I/O 2010 开发者会议
包含 Android 产品工程师的详细视频和幻灯片。

- Google I/O 2011 开发者会议
包含 Android 产品工程师的视频和幻灯片。

- Google I/O 2012 开发者会议
包含 Android 产品工程师的视频和幻灯片。（2012年6月27-29日）

- [Google I/O 2013 开发者会议][77]
一个包含 Android 产品工程师视频和幻灯片的网站。可以在此处通过在线直播观看完整会议。（2013年5月15-17日）

- Google Maps API
适用于 Android 的 Maps API，它提供了大量关于如何在 Android 上使用 Maps API 的信息（这些信息在 Android 开发者网站上找不到）。

- Youtube 上的 Android 开发者频道
Android 开发者频道。这里是包含演示、教程以及任何与 Android 相关视频的聚集地，它是第一个完整、单一且免费的移动平台。

- Youtube  Google I/O - Android 会话
Android 项目网站，关于 Android 开发工具（ddms, logcat, lint）以及各种技巧文档。对于非开发人员的问题，请参阅 Android 爱好者网站。

## 免费 Android 编程书籍

- 使用 HTML、CSS 和 JavaScript 构建应用
- Ed Burnette 著《Hello Android》
- Wei Lee 著《Beginning Android》
- Wallace Jackson 著《绝对初学者应用》
- Mark Murphy 著《程序员的 Android指南》
- Reto Meier 著《专业 Android 开发》
- Shane Conder & Lauren Darcy 著《无线应用开发》
- Shawn Van 著：智能手机和平板的图形、音乐和富媒体开发
- James Steele & Nelson 著《开发者食谱：使用 SDK 构建应用》
- Diego Torres Milano 著《应用测试指南》
- Mark L. Murphy 著《Beginning Android》
- Sigurd Mednie 著《编程 Android》
- Jason Morris 著《用户界面开发：入门指南》
- Marko Garg 著《Learning Android》

## 问题

### Q: 分析加密的应用 (.apk)？

我一直在尝试逆向工程一个付费应用，该应用会写一些二进制数据以便我可以将这些数据导出到其他程序中（这是一个计时器，如果有人好奇的话）。但看起来该 apk 是经过加密的，并存储在 `/data/app/[app_id]` 中。有一篇博客说使用的加密是 AES，密钥存储在 `/data/misc/system/keys` 中，但我无法通过直接使用该密钥的简单策略来解密文件。

我该如何解密它以获得一个实际上可以分析的 apk 呢？

注意：我意识到在 xda-developers 等地方，这些信息被认为是敏感的，因为可能被用于盗版。我没有这种意图，我只是想检查序列化。

用户：brendan-dolan-gavitt

brendan-dolan-gavitt 回答：
在稍了更多工作并仔细阅读后，我发现了我的错误：`/data/app/` 下的文件是加密容器。它们实际上是 dm-crypt 卷，然后挂载到 `/mnt/`。该目录下的 apk 是未加密的，可以使用此回答中的任何工具进行分析。

## Osx

跳转到问题，用户 aperson 提供的 Wiki
源自维基百科：**OS X（此前称为 Mac X）** 是 Apple 公司开发、营销和销售的一系列基于 Unix 的图形界面系统。它专为在 Mac 电脑上运行而设计，自 2002 年以来已预装在所有 Mac 上。它是 Mac OS 9 的继任者，于 1999 年发布，这是“经典” Mac OS 的最后一个版本，该系统自 1984 年以来一直是 Apple 的主要操作系统。发布的第一个版本是 OS X Server 1.0。OS X 的版本以大猫命名：例如，OS X v10.0 “Cheetah”（猎豹）于2001年3月24日发布；v10.8 “Mountain Lion”（山狮）。

## 问题

### Q: OSX 上的线程注入

在 Windows 上已经进行了很多关于 `CreateRemoteThread` 的逆向工程，但在 OSX 上线程注入的主题相对未发现。由于操作系统如此复杂，我应该从哪里开始寻找如何注入线程的校验字节？

用户：mrduclaw

omghai 回答：
诚实地说，我不了解 OSX，甚至不了解 Linux。但我建议查看 GDB 源码。GDB 似乎可以连接到运行的进程。我想这至少可以提供你正在寻找的类似功能。如果你在寻找一个系统调用，似乎 `ptrace` 是 GDB 这样做的方式。

更新：实际上有人写了一篇涵盖该主题的文章。很多人似乎从 Linux 或 BSD 背景转向 Mac，并期望 `ptrace` 是有用的。遗憾的是，在 Mac 上并非如此。由于某种原因，Apple 决定让 `ptrace()` 不完整，无法做到更多。

此外，从这一点来看，`thread_create` 可能是你正在寻找的函数：链接链接。

broadway 回答：对于 OSX 注入，我会查看 mach_star 项目（mach_override 和 mach_inject）
https://github.com/rentzsch/mach_star

此外，Pin 现在支持 os x

分隔符（换行符或问号？），我也不参与校验和的计算。

31e2362e3754553540000000000000000000000000000 最终由 00 终止字符处理，这与校验和也没有关系。

我可以操纵这段字节序列的数据部分，这里有更多示例：

### 示例 2:
```
