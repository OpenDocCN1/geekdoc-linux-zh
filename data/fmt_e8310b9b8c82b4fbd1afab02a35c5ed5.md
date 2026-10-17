
当你准备好关闭 Linux 时，必须以有序的方式进行。即使你是 SUSE Linux PC 的唯一用户，通常也有几个其他程序在后台运行。此外，像 Linux 这样的操作系统尝试优化将数据写入硬盘的方式。由于硬盘访问相对缓慢（与访问内存位置所需的时间相比），数据通常保留在内存中并大块写入硬盘。因此，如果你简单地关闭电源，就会面临某些文件未能正确更新的风险。

任何用户（你甚至不需要登录）都可以从桌面或图形登录界面关闭系统。在 KDE 中，选择主菜单~注销。在 GNOME 中，选择系统菜单~注销。会出现一个对话框（图 3-10 显示了 KDE 桌面的示例），提供重启或关闭系统或简单注销的选项。要关闭系统，只需选择关闭计算机（在 GNOME 中为关机）。（图 3-10 显示了 KDE 桌面的示例）

图 3-10：关机

# 第3章：首次启动 SUSE

此命令运行了带有三个选项 `-s`、`r` 和 `-v` 的 `uname` 命令（如示例所示，可以将它们组合为 `-srv`）。`-s` 选项使 `uname` 打印内核名称，`r` 打印内核发布版本，`v` 打印内核版本号。该命令在某个 Linux 系统上生成的输出：

```
Linux 2.6.8-24-default #1 Wed Oct 6 09:16:23 UTC 2004
```

在这种情况下，系统运行的是内核版本 2.6.8。

要读取文件，请使用 `more` 命令。这里有一个显示 `/etc/passwd` 文件内容的示例：

```
root:x:0:0:root:/root:/bin/bash
bin:x:1:1:bin:/bin/bash
daemon:x:2:2:Daemon:/sbin/bin/bash
lp:x:4:7:printing daemon:/var/spool/lp:/bin/bash
... lines deleted ...
```

要查看系统上正在运行的所有程序列表，使用 `ps` 命令，如下：

```
ps ax
```

`ps` 命令接受许多选项，你可以在不带通常的横杠 `-` 前缀的情况下提供这些选项。此示例使用了 `a` 和 `x` 选项 -`a` 选项列出你正在运行的所有进程，`x` 选项显示所有其余进程。结果是系统上运行的所有进程列表，如下样本输出：

| PID TTY STAT TIME COMMAND |
|---|---|---|---|
| 1 | S | 0:00 init [5] |
| 2 | SN | 0:00 [ksoftird/0] |
| 3 | S | 0:00 [events/0] |
| 4 | S | 0:00 [khelper] |
| 5 | S | 0:00 [netlink/0] |
| 6 | S | 0:00 [kblockd/0] |
| 31| S | 0:00 [kapmd] |
| lines deleted |

# 第 4 章：了解 SUSE 包含的内容

新闻阅读器允许你阅读 Usenet 新闻组，这些新闻组就像人们在上面发布消息的公告板。任何人都可以阅读和回复这些消息。类似于电子邮件，你需要访问所属 ISP（互联网服务提供商）的服务器才能读取新闻组。GNOME 桌面提供了 Pan 新闻阅读器；在 KDE 上，请使用 KNode 阅读新闻组。

视频会议和 IP 电话应用程序用于拨打电话和运行视频会议（将视频会议想象成一种“画面”，你可以在说话时看到其他参与者，其他参与者也能看到你）。GNOME 桌面包含了 GnomeMeeting 视频会议应用。GnomeMeeting 符合 H.323 标准，这意味着它可以与其他符合 H.323 标准的视频会议软件（如 Microsoft Netmeeting）配合使用。KDE 桌面默认不包含视频会议应用程序。

## 介绍办公软件

我所说的办公软件是指用于文字处理、电子表格、演示文稿（报告幻灯片）、日历和联系人管理的软件。当然，你也可以将互联网应用程序——至少包括电子邮件和网络浏览器——视为办公软件，但我正在区分需要互联网才能运行的应用程序与可能在独立式 PC 上使用的应用程序。

无论你使用什么桌面——KDE 还是 GNOME——OpenOffice.org 都是 SU Linux 中主要的办公套件。OpenOffice.org 包含了用于不同任务的不同应用程序，例如文字处理、处理电子表格和准备演示文稿。表 4-2 总结了 GNOME 和 KDE 桌面中提供的办公软件。

我将在第 12 和第 13 章中详细介绍这些办公软件。

| 表 4-2 | GNOME 和 KDE 桌面上的典型办公软件 |
|---|---|
| 应用程序类别 | GNOME 桌面 | KDE 桌面 |
| 文字处理 | OpenOffice.org Writer, AbiWord | OpenOffice.org Writer |
| 电子表格 | OpenOffice.org Calc, Gnumeric | OpenOffice.org Calc |
| 演示文稿 | OpenOffice.org Impress | OpenOffice.org Impress |
| 日历/组织器 | Novell Evolution | Kontakt |

以下是你使用办公软件可以完成的工作：

- `文字处理` 应用程序用于准备信函、报告和任何文档，包括像这样的大型书籍等。在 GNOME 和 KDE 桌面中，你都可以使用 OpenOffice.org Writer 进行文字处理。Writer 的优之处在于它可以与 Windows 世界中流行的 Microsoft Word 软件兼容。
- `电子表格` 应用程序用于创建——还能干什么呢——电子表格。OpenOffice.org 办公套件包含了用于准备电子表格的 Calc 应用。Calc 与 Microsoft Excel 兼容。
- `演示文稿` 软件允许你为汇报准备幻灯片。也许最著名的演示文稿软件是 Microsoft PowerPoint。OpenOffice.org 办公套件带有与 PowerPoint 兼容的 impress 软件。
- `日历/组织器` 应用程序用于跟踪你的预约和待事项。在 GNOME 桌面中，你可以使用多功能的 Novell Evolution 作为组织器，同时将其作为你的电子邮件收件箱。KDE 桌面带有 Kontact 应用用于跟踪你的日历和待办列表。Kontact 还整合了 KMail 阅读器。

## 探索多媒体应用程序

多媒体是指音频、视频或两者兼有——出现在电影中。自然地，多媒体应用程序用于听或看音乐或电影，通常来自数字文件或 CD 或 DVD 等介质。我还将与创建多媒体相关的应用程序包含在多媒体类别中，例如视频编辑器或 CD/DVD 刻录机。SUSE Linux 提供了很好的多媒体应用程序补充。

涉及到播放多媒体——MP3、MPEG 和 QuickTime 等各种格式的音频和视频——免费的 Linux 发行版（包括本书附带 DVD 上的 SUSE Linux）很少带有相应的解码器，因为其中某些解码器存在许可限制。结果就是多媒体应用程序运行了，但由于缺少解码器而无法播放 MP3 文件或 DVD 电影。SUSE Linux 带有一套良好的多媒体应用程序。表 4-3 总结了 SUSE 中的多媒体应用程序。我将在第 14 章详细介绍这些多媒体应用程序。

| 表 4-3 | GNOME 和 KDE 桌面上的典型多媒体应用程序 |
|---|---|
| 应用程序类别 | GNOME 桌面 | KDE 桌面 |
| CD 播放器 | GNOME | CD |
| CD 刻录机 | 刻rip | juK |
| 音频播放器 | XMMS, RealPlayer 10 | |
| CD/DVD 刻录机 | |3b |
| 视频播放器（需要单独解码器） | Totem, RealPlayer 10 | Caffeine, RealPlayer 10 |
| 视频编辑器 | kino | |
| 电视播放器（需要电视卡） | kdetv | |

以下是你使用多媒体应用程序可以完成的工作：

- `CD 播放器` 应用程序允许你在 SUSE 系统上播放音频 CD。你只需要将音频 CD 放入驱动器并使用这些应用程序。
- `CD 刻录机` 应用程序用于从 CD 中刻录（提取）歌曲并将其转换为 MP3 格式。你可以使用音频播放器从 CD 中刻录歌曲并生成它们的数字版本。
- `音频播放器` 用于播放存储在各种格式文件中的音乐，如 MP3 或 Oggbis（一种免费的压缩音频格式）。你可以在 KDE 中使用 amaroK，在 GNOME 中使用，并在两个桌面上使用 RealPlayer10。
- `CD/DVD 刻录机` 应用程序允许你使用 CD/DVD-R（可刻录的）刻录 CD 或 DVD。通过这些应用程序，你通常可以从 ISO 映像文件刻录音频 CD、数据 CD 和 DVD。
