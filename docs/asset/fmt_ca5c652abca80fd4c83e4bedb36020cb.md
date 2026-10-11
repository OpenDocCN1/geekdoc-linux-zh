
# cdcd2wav -D 0,1,0

```
```

这指定音频 CD 位于 SCSI 驱动器上，总线 0 上的 ID 为 1。按下回车后，你将看到以下内容：

```text
135168 bytes buffer memory requested, 4 buffers, 13 sectors

Read TOC CD Ttext failed (probably not supported).

cdcd2wav version schily0.6_linux2.2.13-2m&swm; 1696 1696 real time sched.

soundcard support

AUDIOTrack pre-emphasis copy-permitted tracktype channels

1-11 no no audio 2

Table of Contents: total tracks:11, (total time 52:17.40)

1.( 4:46.56), 2.( 6:16.64), 3.( 5:05.50), 4.( 4:40.22), 5.( 5:41.62)

6.( 4:23.46), 7.( 3:39.18), 8.( 4:12.33), 9.( 4:13.62), 10.( 5:05.13)

11.( 4:09.64)

Table of Contents: starting sectors

1.( 0), 2.( 21506), 3.( 49770), 4.( 72695), 5.( 93717)

6.( 119354), 7.( 139125), 8.( 155568), 9.( 174501), 10.( 193538)

11.( 216426), lead-out( 235165)

CDDB discid: 0xae0c3f0d
```

## DVD 就在眼前？

尽管美国电影行业在破解数字视频光盘（DVD）加密方面进行了无趣的操控，但 Linux 用户可能很快就能合法地播放和享受 DVD 电影。虽然你仍然可以从互联网上的许多站点下载、构建和安装 DeCSS 解密包及相关程序，但一家名为 InterVideo 的公司宣布，在 2000 年初，将在六个月后开发和发布一个廉价的、仅限二进制（当然）的 Linux 驱动程序。请访问 http://www.intervideo.com/ 获取最新详情。

如果你的 PC 有一张 Creative Labs Dxr2 DVD 卡，你可以从 http://opensource.creative.com/ 下载驱动程序。请注意，Creative 的产品是硬件 DVD 解码器，不能用于笔记本！

CD-Text：未检测到
CD-Extra：未检测到
采样文件大小将为 50582156 字节。
正在录制 286.07466 秒的立体声，16 位 @ 44100.0 Hz -> 'audio.wav'...
percent_done: 100%
轨道 1 录制成功

如你所见，除了音乐之外，音频 CD 上还有许多信息！`cdcd2wav` 命令在读取和保存音乐时会使用你音频 CD 的目录和轨道信息。你可以使用该命令的 `track` 选项来指定要录制的一个轨道范围或系列。请注意，生成的 `.wav` 文件每分钟歌曲长度将超过 10MB，因此如果你抓取音频 CD 上的所有轨道，可能会迅速占满较小的分区。

然后可以使用 MPEG 编码器将生成的 `.wav` 文件转换为 `.mp3` 格式，例如使用 `bladenc` 命令。使用该命令及 `.wav` 文件的名称，如下所示：

```
$ bladenc audio.wav
```

按下回车键后，你将看到以下内容：

```
BladeEnc 0.82 (c) Tord Jansson Homepage: http://www.bladenc.cjb.net

==========================================================

BladeEnc is free software, distributed under the Lesser General Public License.

See the file COPYING, BladeEnc's homepage or www.fsf.org for more details.

Files to encode: 1

Encoding: audio.wav

Input: 44.1 kHz, 16 bit, stereo.

Output: 128 kbit, stereo.

Status: 18.0% done, ETA 00:09:10 BATCH: 18.0% done, ETA 00:09:10
```

注意，即使在 300MHz Pentium 计算机上，对于一首 5 分钟的歌，这个过程也可能花费 10 分钟或更长时间！但是，你最终会得到一个文件，它提供大约 1 分钟的数字音频对应每分钟的音频——与使用 `.wav` 格式相比，压缩比为 10:1！通过简单的计算，这意味着你大约可以在不到 600MB 的硬盘存储空间中存储 10 张一小时音频 CD。

### XMMS 规则！

毫无疑问，Linux 和 X11 上最好的 `.mp3` 播放器之一是 `xmms` 客户端。该程序使用文件播放列表进行播放，提供均衡器控制以微调声音，并可以折叠到一个精美的、超小的控制面板，这肯定会让任何希望最大化屏幕空间的移动 Linux 用户满意。

虽然你可以使用命令行来创建 `.mp3` 文件，但将音频 CD 读取为 `.mp3` 格式的一个更简单的方法是使用图形界面客户端，它会自动构建必要的命令行，并通过几次鼠标点击保存你的文件。

### 使用 Krabber 客户端

转换音频 CD 为 `.mp3` 文件的最易用的图形客户端之一是 `krabber` KDE 客户端。该程序使用各种已安装的读取器和编码器，提供设置选项，如质量和每个轨道的名称。另一个很棒的功能是，如果你有活动的 Internet 连接，`krabber` 在从远程服务器检索后会自动保存并使用你的音频 CD 的标题、艺术家和轨道信息！

要开始使用，请将音频 CD 插入你笔记本电脑的 CD-ROM 驱动器。然后，像这样从 X11 终端窗口中的命令启动 `krabber` 客户端：

```
$ krabber &
```

注意，如果你希望自动命名你的文件，你也应该有活动的 Internet 连接。当 `krabber` 在你的计算机上第一次启动时，它会检查所需的文件，如读取器和编码器实用程序。程序启动后，你将看到图 18.13 中显示的窗口。

选择设置，CDDB 设置。在 Krabber 配置对话框中，选择 CDDB 选项卡。点击 Enable Remote CDDB 项，选择一个 CDDB 远程服务器，点击 Update，然后点击 OK。（注意，此对话框与图 18.10 中显示的非常相似。）

接下来，点击按钮 1 来选择你的音乐。你将看到轨道列表。要读取整个 CD，点击 Take All 按钮。然后 `krabber` 客户端显示你的轨道，查询远程 CD 数据库服务器，然后显示 CD 的名称以及 CD 上每个轨道的名称，如图 18.14 所示。

![](img/70d85e6f4d1ff2750ca2a98ba3d9855c_430_0.png)
图 18.15 Krabber KDE 客户端使将音频 CD 读取为 `.mp3` 文件变得轻而易举！

![](img/70d85e6f4d1ff2750ca2a98ba3d9855c_430_1.png)
图 18.16 Krabber 客户端使用远程服务器信息来命名你 CD 上的每个轨道。

点击按钮 2 来指定目录；如果需要，再点击按钮 3 来命名你的文件。在你点击按钮 4 开始读取 CD 之前，使用 krabber 的对话框控制来设置质量、错误检查、采样率以及最重要的 CPU 优先级（根据你的系统的需求和资源，使过程变慢或变快）。完成后，点击按钮 4 开始过程。你将看到进度对话框，如图 18.15 所示。

![](img/70d85e6f4d1ff2750ca2a98ba3d9855c_431_0.png)
**图 10.15** *Krabber 客户端提供一个进度对话框，帮助你估计读取你的 CD 需要多长时间。*

#### 写入 CD-ROM

在戴尔计算机（Dell Computer）发布更新的笔记本型号之前，很少有（如果没有）笔记本电脑提供内置的 CDRW 驱动器。移动 Linux 用户复制、创建或在 CD-ROM 上收集音频轨道和数据的最常见方式是使用带有 PCMCIA 接口的外部 CDRW 驱动器。不幸的是，当前的市场在挑选外部 CDR 或 CDRW 驱动器时，提供了广泛且可能令人困惑的选择。这些外部驱动器在质量、性能、价格和尺寸上差异很大。你会发现来自知名制造商的瘦身版、PCMCIA 端口供电版本（它们可能或不与 Linux 兼容），到笨重的、做工粗糙的无名废品，这些只会产生一次性光盘。

幸运的是，你可以查看 CD-Writing HOWTO 以获取适用于 Linux 的驱动器的最新列表。浏览到
