
# 收集器

## 图 2：Asunder 允许你为你的音乐收藏选择格式。

情况，但通常在将大型 WAV 文件编码为 OGG 或 MP3 文件后，它会删除这些大 WAV 文件。保留 WAV 文件让你在以后决定是否更倾向于使用提供更好质量的另一种编码。

通过检查未识别曲目的指纹来获取元数据。在开始刻录之前，先确保你处于在线状态要容易得多。

根据你的选择，你可以使用任何媒体播放器来欣赏你的 MP3。

作者：Hans-Georg Eeger

- [1]: https://sourceforge.net/projects/grip/
- [2]: Asunder: http://littlesvr.com/asunder/
- [3]: lame: https://lame.sourceforge.io/
- [4]: Gnubid: https://gnubid.org/howto.php

## 图 3：Asunder 正在刻录 CD。这只需要几分钟，你就可以继续其他操作。

![](img/ef948bfad2ff49ba16960a53d116bb79_30_0.png)

```
sudo apt install lame
```

在更改设置之前，你实际上需要安装该包；Asunder 会立即检查它是否能找到 `lame` 二进制文件。

## 刻录

当你对设置满意时，检查“偏好”（`Preferences`）并点击“刻录”（`Rip`）。进度对话框显示了 Asunder 如何刻录和编码（图 3）；在快速机器上，刻录文件进行编码需要更长时间。编码器可能在 CD 刻录完成后还需要完成。

完成后，Asunder 将显示成功创建了 X 个文件。然后你可以取出 CD，插入下一张并重新开始。刻录比播放回滚要快得多，因此刻录整张专辑可能需要几分钟。

如果你的 Linux 未连接，请连接到 Gnu 在线音乐数据库。然后它将音频文件存储在“艺术家/未知专辑/”文件夹中，曲目将命名为 `未知艺术家 - 曲目 - 1.mp3` 等。你使用像 `MusicBrainz Picard`（下文）这样的工具来查找并添加。

## 查找你的设备

Asunder 期望你有一个 `dev/symlink` 名称对应到 CD-ROM 设备名称。你可能必须在 Asunder 选项中手动创建符号链接更改。但首先你需要找到设备名称。在许多情况下，Ubuntu 系统上的 `what/dev` 将是 `dev/sdb`。使用

```
lsblk -d -o NAME,TYPE,MODEL,SIZE,SIZE | grep 'sd'
dev/s0 loop Virtual CD-ROM Data Drive 5,7G
dev/s1 disk 500G HDD Drive SE-SCBA
```

此列表包含两个驱动器；在虚拟虚拟机环境的测试中，你有一个来自三星的 USB 驱动器，被识别为东芝 (TOSHI)。设备名称为 `dev/s1`，因为有一个内部驱动器 `dev/sdb`。选择你想要用于刻录的某一个。

如果你想创建一个符号链接，可以使用以下命令：

`ln -s /dev/s1 /dev/cd`

并将 `/dev/s1` 替换为正确的设备名称。（注意，当你只有一个设备时，这应该是不必要的）。

与其更改符号链接，你也可以倾向于 Asunder 中的“偏好”（`Preferences`），并在第一次（常规）时将设备名称设置为 CD-ROM 设备字段。

酷炫 Linux 技巧 - 2025 版

31

## 识别艺术家和标题

当你刻录收藏时出现了一些错误，现在你留下了显示为 `Artist - Track 1.mp3` 的未标记歌曲。这有一个解决方法！

你可能知道像 Shazam 这样的应用可以识别音乐以及艺术家和标题，但你也可以用你的 MP3 收藏做到这一点并自动完成。用于此目的的方便工具是 `MusicBrainz Picard` [1]，它适用于 Windows。在 Ubuntu 上，通过 APT 安装 `picard` 软件包将让你获得该应用程序的入口，如果你已经开始了处理过程，可以将 MP3 文件拖到左侧，然后在列表中选择“未分类文件”（`Unclassified Files`），并点击“扫描”（`Scan`）。该程序将随后生成指纹以搜索数据库。在右侧窗格中，`Picard` 显示了它找到的这些曲目所属的专辑。点击三角形打开专辑并查看曲目。

为了更新 MP3 文件的元数据，按 `Ctrl+A` 选择所有条目，然后点击“保存”（`Save`）。`Picard` 显示你正准备覆盖任何旧元数据，在点击“确定”（`OK`）后，它就会执行。在我的测试中，当我给一个属于流流派的专辑时，该工具正确识别了几首歌，并正确识别了大部分其他歌曲。你可以通过悬停在选项上来影响这一点，导航到“元数据偏好”（`Metadata Preferences`）并更改“专辑”（增加它）和“合集”（减少它）的滑块。`MusicBrainz Picard` 让你生成你的 MP3 文件的指纹并搜索元数据。

## 修改文件名

添加元数据不会更改文件名。你可以使用 `EasyTAG` 元数据编辑器自动化更改命名的过程。
