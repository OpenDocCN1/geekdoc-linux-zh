
如前所述，你可以播放除 MP3 外的其他音频格式。支持的音频格式包括：

- MP2 和 MP3 流
- WAV
- AU
- CD 音频
- CIN 电影

XMMS 播放器有以下用法：

1. 从网上下载音乐文件（例如从 mp3.com）并将其存储在可访问目录中。
2. 点击 GNOME 桌面菜单上的“程序 -> XMMS”打开 XMMS 播放器（或在终端窗口中输入 `xmms`）。
3. 点击播放按钮（箭头）打开播放器。

# 第 8 章 红帽 Linux 中的多媒体

保存播放列表 — 要保存当前播放列表，按住“加载列表”（Load List）按钮并选择“保存列表”（Save List）。输入您想要为播放列表指定的名称并点击确定。

加载播放列表 — 要重新加载已保存的播放列表，点击“加载列表”按钮。从文件列表中选择一个之前保存的播放列表并点击确定。

播放列表编辑器底部还有一组小按钮。这些按钮与主界面上的按钮相同，用于选择不同的轨道，或播放、暂停、停止或退出当前轨道。

## 使用 freeamp 播放 MP3

freeamp MP3 播放器具有一些巧妙的控制功能。您可以点击显示区域循环切换与音乐相关的当前时间、剩余时间和总时间。按住显示器两侧旋钮上的左鼠标键，移动它们来调整音量（左侧旋钮）或查找歌曲的特定位置（右侧旋钮）。

freeamp 播放器可以从 FreeAmp 主页（http://www.freeamp.org）获取，或者您可以输入 `rpmfind freeamp` 从红帽镜像站找到它。要启动并在您的 X 显示上运行，请输入以下命令：

```bash
freeamp &
```

图 8-4 显示了 freeamp 显示窗口。

![](img/380d929a08ad0f9245d542259c5760b8_314_0.png)

**图 8-4：** 使用旋钮在 freeamp 中调整音量和查找歌曲。

freeamp 的偏设置存储在 `$HOME/.freeamp/preferences` 文件中。`~/.freeamp` 目录下的子目录存储了关于您存储的音乐、字体以及在 freeamp 播放器使用的主题的信息。

您可以在文本模式下运行 freeamp。要这样做，请向 `freeamp` 命令行添加 `-ui textUI` 选项。然而，您不需要添加 `-ui` 选项。如果设置了 `DISPLAY` 变量，则会启动 freeamp 的 X 界面；否则 freeamp 以文本模式启动。

www.united.com 额外内容

freeamp 的“我的音乐收藏”（My Music Collection）功能允许您创建和管理自己的音乐库。您可以包含 MPEG-1 和 MPEG-2 音频文件。您还可以保存单个播放列表。当打开存储的播放列表时，freeamp 会找到您列出的文件并按照指定的顺序进行播放。

要播放 SHOUTcast/http 流或 RTP/组播流，请在 freeamp 命令行上指定 URL。例如，第一个命令行代表 SHOUTcast 流，第二行代表组播流：

```bash
freeamp http://123.48.23.4:8000
freeamp rtp://132.43.21.4:4420
```

您可以通过更改主题来改变 freeamp 窗口的外观和按钮布局。点击“选项”（options）按钮，在选项窗口中点击“主题”（Themes）选项卡，从主题选择区域选择一个主题，然后点击确定。新主题将立即应用于 freeamp。

## MIDI 音频播放器

MIDI 代表乐器数字接口（Musical Instrument Digital Interface）。MIDI 文件由合成器创建，比其他类型的音频文件小，因为它们不存储完整的声音，而是包含所播放的音符。MIDI 播放器重现音符，使其听起来像各种 MIDI 乐器。

互联网上有许多下载 MIDI 文件的网站。尝试 Infini MIDI 网站（http://www.ifni.com），其中包含了按专辑分类的披头士乐队、齐齐飞飞、涅灭乐队和其他乐队的歌曲。大多数 MIDI 音乐非常简单，但你可以从中找到玩的乐趣。

红帽 Linux 自带了几个不同的 MIDI 播放器，包括 `playmidi` 和 `xplaymidi`。`playmidi` 命令是一个基于文本的 MIDI 播放器。`xplaymidi` 命令为 `playmidi` 命令提供了一个界面。

对于任何命令，您只需输入命令并在后跟您想要播放的 MIDI 文件名即可。少数选项包括掩码特定通道号（`-c#`，`#` 替换为要掩码的通道）或忽略任何打击乐轨道（`-d`）。但如果您使用 `xplaymidi`，界面允许您选择性地开启或关闭轨道。图 8-5 显示了 `xplaymidi` 窗口（正在播放巴赫的《勃兰登堡协曲曲第3号》）。

![](img/380d929a08ad0f9245d542259c5760b8_316_0.png)

**图 8-5：** `xplaymidi` 窗口在播放时显示 MIDI 轨道。

每个轨道显示乐器名称（左侧），而条形（右侧）显示每个轨道播放时的音量水平。点击代表每个轨道的按钮可以开启或关闭该轨道。要听几个轨道的情况，请点击不想听的轨道上的按钮；这样您就能听到想听的轨道。

## 播放视频

如果您想显示视频片段或从互联网播放流视频，您可以播放多种视频格式，尽管这在 Linux 中某些有限。带有用于 X 的 Xanim Viewer 可以播放 Quicktime 和 AVI。还有一个 Linux 版本的 RealPlayer 用于播放大量的 RealMedia 内容。

由于您可能正在查看视频片段或从互联网播放流视频，您可能希望在您的浏览器中整合此类视频技术。Netscape 具有播放视频（以及其他格式）的能力。

www.united.com 额外内容

## Xanim 查看器

Xanim viewer 是一个用于 X 的视频播放器。它可以播放各种视频格式，包括 AVI、MPEG 和 Quicktime。它还支持从互联网播放流视频。

# RealPlayer

互联网上提供了大量的 RealMedia 和 RealAudio 格式内容。你可以观看和听到流行音乐家和漫画的视频片段。你可以观看直播活动，例如会议、新闻报道和演唱会。当你离开家时，还可以收听你喜欢的广播电台。

正如你可能想到的，要播放 RealMedia 和 RealAudio 内容，你需要 RealPlayer。Real Networks (http://www.real.com) 是互联网流媒体领域的领导者。有超过 5000 万名唯一用户在 Real Networks 及其网站注册，每天下载超过 175,000 个文件。这还不是好消息。好消息是，现在可以在红帽 Linux 上运行 RealPlayer 了。

若要免费下载 RealPlayer，请访问 RealPlayer 下载页面（http://www.real.com/products/player）。到达页面后，点击免费播放器链接，然后寻找适用于 UNIX 的 RealPlayer 链接。你会被要求填写表单以获取免费下载。你需要选择你使用的系统类型和 CPU。选择支持 i386 libc6 的 Linux 版本（如果有相应的 RPM 包，请选择它）。你也可以从 download.com 的 Linux 区域获取 Linux 版 RealPlayer。

配置 RealPlayer 的说明以 HTML 格式提供，因此你可以在 Netscape 或其他 浏览器中阅读。如果需要任何补丁或变通方法，你可以在 Real Networks 知识库中找到。要到达那里，点击 Support（在大多数 Real Networks 页面上），然后点击 Knowledge Base。在那里，查询单词“Linux”以查找任何问题和修复方案。

当安装 RealPlayer 时，系统会询问你是否将其配置为 Netscape 插件（我强烈建议你这样做）。之后，当你打开任何 Real 内容时，RealPlayer 会自动打开并处理该内容。作为替代，你可以通过在桌面的终端窗口中输入以下命令来启动 RealPlayer：

```
realplay &
```

图 8-7：使用 RealPlayer 从网页播放音乐视频、体育和新闻。

![](img/380d929a08ad0f9245d542259c5760b8_319_0.png)

图 8-7：使用 RealPlayer 从网页播放音乐视频、体育和新闻。

# 第 8 章 红帽 Linux 中的多媒体

一旦你拥有了 RealPlayer，就可以访问相关网站获取内容并在 RealPlayer 上播放。我建议先从 RealGuide (http://realguide.com) 开始。这是一个关于可以在 RealPlayer 上播放的互联网音频视频指南。该指南包含指向正在直播的节目和活动的链接。还有使用该技术的特殊新闻报道，以及指向音乐、节目、体育、科学/技术、社会、财经和购物网站的链接。

## 使用 gPhoto 使用数字相机
