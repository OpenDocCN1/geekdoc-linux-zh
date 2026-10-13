
![](img/ba0161b65b37e94cffc801ecbacaba5e_357_0.png)

## 第 21 小时

### FreeBSD 中的多媒体

虽然与 Windows 和 Macintosh 相比仍相差甚远，但 FreeBSD 的多媒体支持正在变好。例如，今天 FreeBSD 支持大多数流行的声卡，因此可以播放 MP3、音频 CD 等。在本小时中，你将学习：

- 如何在 FreeBSD 中配置声音支持
- FreeBSD 中用于播放媒体文件的各种应用程序
- 如何在 FreeBSD 中刻录（录制）CD
- 如何在 FreeBSD 中播放视频文件

### 在 FreeBSD 中配置声音支持

为 FreeBSD 添加声音支持需要做两件事。第一是重新编译内核并加入声音设备，因为默认情况下不包含它。第二是为声音系统创建设备节点。有关如何配置内核和构建新内核的详细信息，请参阅第 10 小时。需要在内核配置文件中添加以支持声音的行是

```
device pcm
```

pcm 设备支持大多数常见的声卡，并且还可以检测大多数声卡的位置。

在将 pcm 设备添加到内核配置并重建内核后，你需要创建声音支持的设备节点。这非常简单。 以 root 用户身份，切换到 /dev 目录（使用命令 cd /dev），然后完全按照所示输入以下命令：

```
./MAKEDEV snd0
```

请记住 FreeBSD 区分大小写，因此请确保完全按照所示输入。这将创建访问声卡所需的设备节点。一般来说，你无需担心此事，因为你不会直接与这些设备节点交互。它们只是由声音应用程序用来向声卡发送数据。然而，你确实需要确保声音设备节点存在。

### 声音应用程序

在 FreeBSD 中完成声音支持配置后，你就可以查看一些在 FreeBSD 中播放声音的应用程序了。当然，人们最常做的事情之一就是播放 MP3 文件。是的，FreeBSD 中有多种播放 MP3 的选项，包括命令行和图形 MP3 播放器。

### mpg123

mpg123 是一款流行、无花哨的命令行 MP3 播放器。它可在 FreeBSD ports 集合的 Audio 目录下获得。

安装 mpg123 后，你只需输入 mpg123 后跟要播放的 MP3 文件名即可播放 MP3。你也可以提供一个 MP3 文件列表，mpg123 将按列出顺序播放它们。该程序还接受通配符。例如，mpg123 *.mp3 将播放当前目录中的所有 MP3 文件。有关 mpg123 功能的更多信息，请参阅其手册页。

### XMMS

XMMS 是 X 下流行的 MP3 播放器。它基本上是 Winamp 的克隆，事实上它甚至支持使用 Winamp 皮肤。图 21.1 显示了 Winamp MP3 播放器。

XMMS 可在 ports 集合的 Audio 目录下获得。

图 21.1
XMMS MP3 播放器。过去使用过 Winamp 的 Windows 用户不会有任何问题来适应 XMMS。

![](img/ba0161b65b37e94cffc801ecbacaba5e_359_0.png)

### CD 播放器

KDE 也附带了一个 CD 播放器。CD 播放器支持 CDDB 系统，这意味着它可以自动从互联网下载专辑和曲目信息。图 21.2 显示了 KDE CD 播放器。

图 21.2
KDE CD 播放器。

![](img/ba0161b65b37e94cffc801ecbacaba5e_359_1.png)

### 混音器

FreeBSD 附带了一个可从命令行访问的混音器。要仅显示当前混音器设置，只需在命令提示符下输入 mixer，然后按 Enter。以下是 mixer 命令的一些示例输出：

```
Mixer vol   is currently set to 90:90
Mixer bass  is currently set to 75:75
Mixer treble is currently set to 75:75
Mixer synth is currently set to 75:75
Mixer pcm   is currently set to 75:75
Mixer speaker is currently set to 75:75
Mixer line  is currently set to 75:75
Mixer mic   is currently set to 32:32
Mixer cd    is currently set to 75:75
Mixer mix   is currently set to 0:0
Mixer igain is currently set to 75:75
Mixer ogain is currently set to 75:75
```

要更改其中一个设置，输入 mixer，后跟要更改的设置名称，再跟 1 到 100 之间的数字。例如，命令

```
mixer vol 50
```

将主混音器音量设置为 50%。如果要将左右电平设置得不同，请使用冒号分隔的两个数字。例如，

```
mixer vol 50:40
```

将左音量设置为 50，右音量设置为 40。

如果你不喜欢命令行混音器，KDE 也内置了一个混音器，可以从 K 菜单的多媒体子菜单中访问。图 21.3 显示了 KDE 声音混音器。

图 21.3

KDE 声音混音器。

![](img/ba0161b65b37e94cffc801ecbacaba5e_360_0.png)

### CD 刻录

如果你有一台 CD-R（可录 CD）或 CD-RW（可重写 CD）驱动器，你可以参与到当今计算机时代最受欢迎的多媒体消遣活动中：创建你喜欢混音的自己的音乐 CD。

然而，FreeBSD 中的 CD 刻录仍然是命令行操作。你安装的可录光驱很可能是一台 IDE/ATA 驱动器；如果是这样，你将使用的工具是 burned。（然而，如果你有一台 SCSI 驱动器，你将需要使用 cdrecord；由于如今 SCSI 刻录机远不如 IDE 刻录机常见，我们将在本小时的课程中重点介绍 burned。）

与我们在第 8 小时“存储系统和备份实用程序”中介绍的创建数据 CD 的过程不同，创建标准音频光盘 CD 不涉及两步过程。你不需要先使用 mkisofs 创建 ISO 磁盘映像。相反，你可以直接使用 burned 命令将 WAV 格式的音频文件写入光盘。

首先，将你想要刻录的歌曲转换为 WAV 格式。你可以使用 dagrab（可在 ports 的 /usr/ports/audio/dagrab 中获得）直接从音频 CD 中提取音频曲目到 WAV 格式。如果你的歌曲是 MP3 格式，你可以使用 XMMS 的“磁盘写入器”插件将其转换为 WAV 格式。

> 今天出版的许多音频 CD 都具有防止即使是光盘的合法所有者也无法将光盘内容“空间转移”到其他媒体（如软件 MP3 播放器或可录 CD）上的复制保护功能。如果使用 dagrab 实用程序无法从这些光盘中提取音频，这很可能是原因。

在将你想要刻录到 CD 上的所有歌曲转换为 WAV 文件后，你可以使用 burned 用单个命令将它们全部写入：

```
# burned -f /dev/ac0c0 audio track1.wav track2.wav track3.wav fixate
```

你可以在此命令行上列出任意多个文件，前提是它们的总播放时间不超过光盘上的空间。请记住，CD 可容纳 650MB 或 700MB 的数据；如果要刻录的 WAV 文件总和超过该容量，你必须删除一些。

-f 开关指定驱动器设备；fixate 关键字告诉 burned“关闭会话”，这意味着在过程完成后，CD 已完全刻录，可以在 FreeBSD 下作为磁盘挂载或在标准 CD 播放器中播放。

你还可以创建“MP3 CD”，可在日益增多的主流音频播放器中播放（包括汽车中控台播放器）。MP3 CD 只是一个包含多个压缩 MP3 文件的标准 ISO 9660 CD-ROM。你可以在 MP3 CD 上容纳比普通 CD 多约 12 倍的歌曲，或更多，具体取决于文件的压缩级别。

要刻录 MP3 CD，你需要按照通常用于创建数据 CD 的两步程序进行操作，正如我们在第 8 小时讨论的那样。首先，使用 mkisofs 从存储在特定目录中的 MP3 文件创建 ISO 磁盘映像：(/path/to/directory)

```
# mkisofs -o diskimage.iso -J -R /path/to/directory
```

此命令将从你指定的目录中的所有 MP3 音频文件创建 ISO 9660 磁盘映像；-J 和 -R 开关告诉 mkisofs 使光盘与 Windows（使用 Joliet 长文件名扩展）和 UNIX（使用 Rock Ridge 扩展）兼容。磁盘映像创建后，你可以使用 burned 刻录 CD：

```
# burned -f /dev/ac0c0 -s 4 data diskimage.iso fixate
```

-s 4 开关告诉 burned 以 4 倍速刻录；如果你的驱动器支持更高速度，你可以设置更高的数字。
