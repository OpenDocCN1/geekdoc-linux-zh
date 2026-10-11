
`lsmod` 的输出显示 `pwc` 驱动已加载，并与 `videodev` 模块和 `usbcore` 模块关联。

# 为 Ekira 开放防火墙

为了使用 Ekira，你需要在防火墙中打开多个端口。特别是，你需要打开 TCP 端口 1720 和 TCP 端口范围 30000 到 30010。对于 UDP 端口，你必须打开 5000 到 5007 端口以及 5010 到 5013 端口。你可以用于打开这些端口的 `iptables` 设置示例包含在 Ekira FAQ (`www.ekira.org/faq`) 中。

# 运行 GnomeMeeting

要在终端窗口中启动 Ekira，请输入 `ekira &`。如果尚未安装，你可以在安装 GNOME 桌面时获取适用于你的 Linux 发行版的包。首次运行 Ekira 时会启动 Ekira 配置向导，允许你输入以下信息：

- 个人数据 — 你的名、姓、电子邮件地址、备注和位置。你还可以选择是否出现在 Ekira ILS 目录中。
- 连接类型 — 指明你的互联网连接速度（56K 调制解调器、ISDN、DSL/缆、T1/LAN 或自定义）。

一旦输入数据，Ekira 窗口就会打开。

图20.8 显示了带有通话日志的 Ekira 窗口。选择“Calls History”（通话历史）打开该日志。它显示了你在会话期间进行的通话历史。要打开通讯录，从 Ekira 窗口左侧选择通讯录图标。在该窗口中添加 ILS 服务器和朋友，然后选择你想联系的用户或服务器并点击“Contact”（联系）。

使用视频窗口下方的标签调整你的音频和视频外观。“History”（历史）标签显示你的活动日志。

## 播放音乐和视频

图 20.8

连接到 ILS 服务器与 Ekira 进行视频会议。

![](img/fa18693414a802b12c8add5f8c4be910_576_0.png)

# 观看电影和视频

虽然 Linux 提供了几种相当高质量的视频播放器，但由于法律问题，很少在正式发行版中看到这些播放器。在 Linux 中播放加密 DVD 电影的相关问题可能是导致 `MPlayer` (`freshmeat.net/mplayer`)、`Ogle` (`http://www.dtek.chalmers.se/groups/dvd`) 和 `xine` (`xine.sourceforge.net`) 等视频播放器未包含在常见发行版中的原因。

然而，只要你不下载并使用 `DeCCS`（用于解密 DVD 电影的软件），就可以使用这些视频播放器播放各种视频内容。以下章节提供了常用视频播放器的说明。

## 使用 xine 观看视频

`xine` 播放器是一个播放各种视频和音频格式的优秀应用程序。你可以从 `xine.sourceforge.net` 或你的 Linux 发行版相关的软件库获取 `xine`。

你可以在终端窗口中输入 `xine&` 来启动 `xine` 播放器。图20.9 显示了 `xine` 视频播放器窗口和控件的示例。

### 图 20.9 使用 xine 播放视频 CD、MP3、QuickTime 和其他视频格式。

![](img/fa18693414a802b12c8add5f8c4be910_577_0.png)

> 注意：当你尝试安装 `xine` 时，它会提示你是否需要任何额外的包。如果 `xine` 播放器无法启动，请参见本章稍后部分的“Xine 技巧”章节。

`Xine` 支持多种视频和音频格式，包括：

- MPEG (1, 2 和 4)
- QuickTime（如果你的 QuickTime 内容无法播放，请参见“Xine 技巧”）
- WMV
- DVDs、CDs 和 VCDs
- Motion JPEG

- MPEG 音频 (MP3)
- AC3 和杜比数字音频
- DTS 音频
- Ogg Vorbis 音频

`xine` 理解代表音频视频组合的文件格式，包括 `.mpg` (MPEG 程序流)、`.ts` (MPEG 传输流)、`.mpv` (原始 MPEG 音频/视频流)、`.avi` (MS AVI 格式) 和 `.asf` (高级流格式)。虽然 `xine` 可以播放视频 CD 和 DVD，但它无法播放加密 DVD 或 Video-on-CD 混合格式（由于前面提到的解密 DVD 的法律问题）。

## 使用 xine

启动 `xine` 后，在 `xine` 窗口中点击右键查看控件。播放视频的最快方法是点击以下按钮之一，然后按下 Play 按钮（右箭头或 Play，取决于你使用的皮肤）：

接下来，你可以使用 Pause/Resume、Stop、Play、Fast Motion、Slow Motion 或 Eject（退出的）按钮来处理视频。你还可以使用 Previous 和 Next 按钮切换到不同的轨道。这些控件与你预期的非常相似。

### 创建播放列表

要选择单个文件或组合一个列表进行播放，请使用 Playlist 功能。

`Xine` 支持文件播放列表。你可以通过 `playlist...` 创建播放列表。

图20.10 显示了播放列表窗口。要向播放列表添加文件，点击 Add 按钮。要删除文件，点击 Remove 按钮。要重新排序文件，使用 Up 和 Down 按钮。你可以点击 Save 按钮保存播放列表。

要播放播放列表，点击 Play 按钮。要删除播放列表，点击 Delete 按钮。

# 第四部分 运行应用程序

表 20.2

| 按钮 | 描述 |
| :--- | :--- |
| Add | 向播放列表添加文件。 |
| Remove | 从播放列表中删除文件。 |
| Up | 将选中的文件在列表中向上移动。 |
| Down | 将选中的文件在列表中向下移动。 |
| Save | 将当前播放列表保存到磁盘。 |
| Play | 开始播放当前播放列表。 |
| Delete | 删除当前播放列表 |

# Xine Tips

当你尝试安装 `xine` 时，它会提示你是否需要任何额外的包。如果 `xine` 播放器无法启动，请参见本章稍后部分的“Xine 技巧”章节。

# 第四部分 应用程序

通过在 Real Networks 知识库中查询“Linux”一词来查找它们。要到达那里，点击 Support（支持，位于大多数 Real Networks 页面上），然后点击 Knowledge Base（知识库）。

当你安装 RealPlayer 时，系统会询问你是否想将其配置为 Netscape 插件（我建议这样做，这样你就可以在 Mozilla Firefox 中播放真实内容）。之后，当你在浏览器中打开任何 Real 内容时，RealPlayer 会打开并处理它。或者，你也可以通过在桌面的 Terminal 窗口中输入以下命令来启动 RealPlayer：

```bash
```
