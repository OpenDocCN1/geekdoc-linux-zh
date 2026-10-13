
你可以使用 XMMS 来收听你可能在第 11 节中保存的某些音乐。如果你使用 `grip` 将音乐保存到主目录并想收听它，启动 XMMS 并右键点击窗口。选择“Open>File”并选择你创建的任何 WAV 文件。

![](img/cc58a1e8691061866010ce216f881372_198_0.png)

176 第三部分：Linux，哈！它有什么用？简直无所不在！

Ogg 是用于格式化音频流的系统，而 Vorbis 压缩信息。与大多数其他技术系统不同，Ogg/Vorbis 不是缩写词，而是以科幻小说人物命名的。有关 Ogg/Vorbis 及其类似的开源多媒体系统的更多信息，请访问 www.vorbis.com。

![](img/cc58a1e8691061866010ce216f881372_199_0.png)

Ogg 是用于格式化音频流的系统，而 Vorbis 压缩信息。与大多数其他技术系统不同，Ogg/Vorbis 不是缩写词，而是以科幻小说人物命名的。有关 Ogg/Vorbis 及其类似的开源多媒体系统的更多信息，请访问 www.vorbis.com。

![](img/cc58a1e8691061866010ce216f881372_199_0.png)

现在你已经有了一点，启动 XMMS 收听 Ogg：

- 1. 前往 www.vorbis.com。
- 2. 打开窗口。
- 3. 点击 OK 按钮。
- 4. 输入文件名。
- 5. 输入以下命令：

```
xmms
```

- 6. 右键点击窗口。
- 7. 点击 OK 按钮。

![](img/cc58a1e8691061866010ce216f881372_199_1.png)

如果你想刻制音乐，过程会稍微不同。你不需要创建 ISO 镜像。下面的示例显示了如何创建音频 CD：

## 第 12 章

## 来自网络的直播

177

- 1. 前往 www.vorbis.com。
- 2. 打开窗口。
- 3. 点击 OK 按钮。
- 4. 输入文件名。
- 5. 输入以下命令：

```
xmms
```

- 6. 右键点击窗口。
- 7. 点击 OK 按钮。
- 8. 点击 OK 按钮。

Enlightened Sound Daemon (`esd`) 允许多个音频播放器同时使用电脑扬声器，有时 `esd` 会产生混乱，你需要重启它。以 root 身份登录，打开 GNOME Terminal，运行命令 `killall -UP esd`。如果不起作用，你可以配置 XMMS 输出输出。

- 1. 右键点击 XMMS 窗口。
- 2. 选择 Options:Preferences。
- 3. 点击 Output 子窗口。
- 4. 选择 OSS 驱动。
- 5. 点击 Apply 按钮。
- 6. 点击 OK 按钮。

![](img/cc58a1e8691061866010ce216f881372_200_0.png)

178 第三部分：Linux，哈！它有什么用？简直无所不在！

![](img/cc58a1e8691061866010ce216f881372_201_0.png)

图 12-2：在 New Type 窗口中创建应用程序

### 修改 XMMS 以处理 MP3

MP3 (MPEG音频层 3) 是存储音乐和其他音频信息的流行介质，也可用于在互联网上传输多媒体。开源媒体播放器 XMMS 由 Red Hat Linux 默认安装。然而，由于版权和专利考虑，Red Hat 在其任何版本中均未包含 MP3 支持。

本节描述了如何从 XMMS 官方那里安装 MP3 支持。我们包含了这些易于使用且与 Red Hat Linux 绑定的说明。本章介绍的 Mplayer 也支持 MP3，但你可能只需要使用 MP3 并偏好使用。

你可以从 www.xmms.org 获取 XMMS 的 MP3 插件。遵循以下步骤：

- 1. 启动 Mozilla 并访问 http://staff.xmms.org/priv/redhat8//。
- 2. 在适用于 Red Hat 的 XMMS 区域点击 `xmms-mpg123-1.2.7-13.rpm` 链接。

   打开保存文件名的窗口。
- 3. 点击 Save 按钮。
- 5. 如果你尚未以 root 身份登录，请在终端窗口中输入此命令：
- 6. 在提示时输入 root 密码。
- 7. 输入此命令安装支持 MP3 的 XMMS 播放器：

`rpm -ivh rpm-mpg123*`（应该是 `rpm -ivh xmms-mpg123*`）

- 8. 在提示符输入输入命令启动 XMMS：
- 9. 你可以通过点击 XMMS 窗口并选择 Options:Preferences（选项：偏好）来看到 MP3 插件已安装。偏好窗口打开后会显示新增的内容。图 12-3 显示了新的插件。

![](img/cc58a1e8691061866010ce216f881372_202_0.png)

现在，你只需要在互联网上找到一个流媒体音频源即可使用 XMMS 听 MP3。寻找 MP3 位置的好地方是 www.shoutcast.com。它提供了许多流媒体链接。要听某些 MP3，请遵循以下步骤：

- 1. 启动 MP3 并前往 shoutcast.com。
- 2. 点击任何一个 Tune-in 链接。例如，查看 Jazz 流。
- 3. 弹出一个窗口，提示你将文件保存到另一个位置或指定一个应用程序来处理连接。
- 4. 要让 XMMS 建立，点击 Advanced（高级）按钮。打开另一个窗口。
- 5. 点击 Application 字段并输入 `xmms`。
- 6. 点击 OK。
- 7. 点击 Ask Me Before Opening Downloaded Files of This Type（在打开此类类型的下载文件之前询问）按钮。

这一步是为 MP3 MIME 类型定义新辅助应用程序（Helper Application）的快速替代方案。（前面的章节“使用 XMMS 音频播放器”描述了如何创建新的辅助应用程序。）

- 8. 点击 OK 回到上一个窗口。再次点击 OK。

Mozilla 启动 XMMS 以处理 MP3 流。你现在可以使用 XMMS 听你喜欢的任何类型的音乐和任何新闻。

### 使用奇妙的 Mplayer

每当有迫切需求时，开源运动就会出现。直到最近，你还无法使用任何单一 Linux 来听和查看大多数流媒体格式。现在，Mplayer 出现并填补了这一空白。

Mplayer 可以播放大多数流行的（以及许多冷门的）音频和视频流媒体格式。尽管它还没有达到正式发布的程度，但已经非常接近发布且非常好用。在编写这本书的版本时，第二个候选版本（beta 测试的最终形式）刚刚发布。版本 1.0 也已发布。

此列表显示了 Mplayer 可以播放的一些流媒体格式：

- MPEG-1/Layer 3 (MP3)：MP3 是一种用于存储和流传输音频的流行但专利编码格式。
- Ogg/Vorbis：这种新型且即将推出的开源流媒体格式不受任何版权或专利的限制，与其他格式不同。
- Microsoft Media Server (MMS)：你可以使用 Mplayer 收听使用流行的 MMS 格式的广播电节目。此前，你需要使用微软客户端来收听 MMS 流。
- Digital Versatile Disc (DVD)：你可以使用 Mplayer 从电脑播放 DVD。
- RealAudio：你需要下载、编译并安装 RTSP 包来使用 RealAudio。

## 第 12 章：来自网络的直播 181

MPlayer 目前未包含在 Red Hat Linux 发行版中。我们希望它以后会被包含，但目前你必须从其开发者那里获取。这些说明了如何下载、安装和使用 MPlayer：

- 1. 登录并打开 Mozilla。
- 2. 前往 http://www.mplayerhq.hu/homepage/dload.html。
- 3. 点击最新的 Red Hat RPM 版本。

在编写这本书时，Red Hat 7.x 是最新版本。然而，这些说明适用于 Red Hat 9。

- 4. 从 i386 或 x86_64 目录下载这些包：

```
mplayer-0.90rc5-1
mplayer-common-0.90rc5-1
```

- 5. 从 noarch 目录下载这些包：

```
mplayer-gui-0.90rc5-1
mplayer-skin-default-1.6-3
```

以及这些字体包中的任何一个：

```
mplayer-font-iso1-1.0-3
mplayer-font-iso2-1.0-3
mplayer-font-iso9-1.0-3
```

在编写这本书的版本时，最近的 MPlayer 版本是 rc5（发布候选5）。你可能会看到并应该使用最新的可用版本。

- 6. 打开 GNOME Terminal 窗口并切换到 root：

```
su
```

在提示时输入 root 密码。

- 7. 按照此顺序安装包：
