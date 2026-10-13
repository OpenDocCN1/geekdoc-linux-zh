
```
cat /proc/bus/usb/devices
```

输出应显示你的相机为大容量存储设备。例如，当我将 Nikon Coolpix 2500 作为 USB 大容量存储设备连接时，我得到以下输出：

```
T:  Bus=01 Lev=00 Prnt=00 Port=00 Cnt=00 Dev#= 1 Spd=12 MxCh= 2
B:  Alloc= 0/900 us ( 0%), #Int= 0, #Iso= 0
D:  Ver=1.10 Cls=09(hub)  Sub=00 Prot=00 MxPS= 8 #Cfgs= 1
P:  Vendor=0000 ProdID=0000 Rev= 0.00
S:  Product=USB UHCI Root Hub
S:  SerialNumber=fc00
C:* #Ifs= 1 Cfg#= 1 Atr=40 MxPwr= 0mA
I:  If#= 0 Alt= 0 #EPs= 1 Cls=09(hub) Sub=00 Prot=00 Driver=hub
E:  Ad=81() Atr=03(Int.) MxPS= 8 Ivl=255ms
T:  Bus=01 Lev=01 Prnt=01 Port=01 Cnt= 1 Dev#= 2 Spd=12 MxCh= 0
D:  Ver=1.10 Cls=00(isc) Sub=00 Prot=00 MxPS=64 #Cfgs= 1
P:  Vendor=04D0 ProdID=0A08 Rev= 1.00
S:  Manufacturer=NIKON
S:  Product=Nikon Digital Camera E2500
S:  SerialNumber=00000336943
C:* #Ifs= 1 Cfg#= 1 Atr=c0 MxPwr= 0mA
I:  If#= 0 Alt= 0 #EPs= 2 Cls=08(stor.) Sub=06 Prot=50 Driver=usb-storage
E:  Ad=04(0) Atr=02(Bulk) MxPS= 64 Ivl=0ms
E:  Ad=83(3) Atr=02(Bulk) MxPS= 64 Ivl=0ms
```

从第二个 `T:` 行开始的所有行都与 Nikon Coolpix 2500 相机有关。你可以在输出中看到一些详细信息，例如制造商名称和相机型号。

### 挂载与访问

4. 通过输入以下命令挂载相机的存储介质：

```
mount /mnt/camera
```

GNOME 桌面上会出现一个相机图标。

5. 双击 GNOME 桌面上的相机图标。

相机的内容会出现在 Nautilus 文件管理器窗口中。你可以双击文件夹并找到包含照片的文件夹。通常，这些数码照片是带有 `.jpg` 扩展名的 JPEG 文件，文件名很隐晦。在默认视图中，Nautilus 显示照片的缩略图，因此你不必担心隐晦的文件名。图 5-3 显示了 GNOME 桌面，其中有相机图标和 Nautilus 窗口，显示了我 Nikon Coolpix 2500 的照片。

6. 单击以选择照片并将其复制到你的硬盘。

你也可以在终端窗口中输入 `cp` 命令，将所有或选定的图像复制到硬盘上的目录。例如，要将相机中的所有 JPEG 照片复制到当前目录，请输入：

```
cp /mnt/camera/*.jpg .
```

Figure 5-3: 你可以将数码相机中的数码照片作为 USB 大容量存储设备访问。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_219_0.png)

7. 下载完照片后，在 GNOME 桌面上右键单击相机图标并从弹出菜单中选择 卸载卷。

这会导致 Red Hat Linux 将相机从 `/mnt/camera` 目录卸载，删除 `/mnt/camera` 目录，并删除添加到 `/etc/fstab` 文件中的行。

8. 关闭相机电源并从 PC 上断开 USB 电缆。

当你可以像访问任何其他存储设备一样访问相机时，还需要 `gtkam` 吗！

## Playing audio CDs

GNOME 和 KDE 都附带 CD 播放器应用程序。要播放音频 CD，你需要一个声卡，并且该声卡必须配置为在 Red Hat Linux 中工作。

如果你使用的是 GNOME 桌面，你可以使用 GNOME CD Player 应用程序播放音频 CD。通过选择 主菜单→声音和视频→CD 播放器 启动 GNOME CD Player。图 5-4 显示了该 CD 播放器正在播放音频 CD 中的曲目。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_220_0.png)

GNOME CD Player 显示 CD 的标题和当前曲目的名称。GNOME CD Player 从 Compact Disc Database（CDDB）获取歌曲标题——互联网上的一个 CD 数据库（`freedb.freedb.org`）。这意味着 CD 播放器需要从 CD 数据库下载歌曲信息，因此需要一个活动的互联网连接。CD 播放器下载特定 CD 的信息后，会将其缓存在本地数据库中以供将来使用。CD 播放器的用户界面直观，易于学习。一个不错的功能是你可以按标题选择曲目，如图 5-5 所示。

如果你使用 KDE 作为桌面，你会在 KDE 中找到一个类似的音频 CD 播放器。通过选择 主菜单→声音和视频→KsCD 启动 KDE CD 播放器。

Figure 5-5:

在 GNOME CD Player 中，你可以选择特定的音频曲目进行播放。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_221_0.png)

## Playing sound files

你可以使用 X 多媒体系统（XMMS）打开和播放声音文件。XMMS 可以播放多种类型的声音文件，包括 Ogg Vorbis 和 Windows WAV。你会在 Red Hat Linux 系统的 `/usr/share/sounds` 目录中找到许多 WAV 声音文件——这些文件通常以 `.wav` 扩展名结尾。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_221_1.png)

你还可以使用 `cdda2wav` 命令行应用程序从音频 CD 曲目创建 WAV 声音文件。例如，要将音频 CD 中的第二首曲目转换为 WAV 文件，请输入以下命令：

```
cdda2wav -D /dev/cdrom -t2 -O wav
```

`cdda2wav` 将曲目保存在名为 `audio.wav` 的 WAV 文件中。然后你可以在 XMMS 中播放该 WAV 文件。不过要注意——音频 CD 的每首曲目在 WAV 格式下通常占用约 60MB 的磁盘空间。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_221_2.png)

Red Hat 已从 XMMS 中移除了播放 MP3 文件所需的代码，因此在播放 MP3 文件之前，你必须将其转换为 WAV 等受支持的格式。Red Hat 建议你对压缩音频文件使用 Ogg Vorbis 格式，因为 Ogg Vorbis 是一种免专利和免版税的格式。

从 GNOME 或 KDE 桌面启动 XMMS，选择 主菜单→声音和视频→音频播放器。XMMS 具有简单的用户界面。要打开声音文件，选择 窗口菜单→播放文件，或按 L 从加载文件对话框中选择 `.wav` 或 `.ogg` 文件。选择文件并单击确定。XMMS 开始播放声音文件。图 5-6 显示了 XMMS 播放声音文件时的典型窗口。

图 5-6：您可以在 XMMS 中播放许多不同类型的声音文件。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_222_0.png)

如果 XMMS 出现错误消息，选择 窗口菜单→选项→首选项，然后将 OSS 驱动程序选为输出插件。如果您想调整音量或其他声音属性，通过选择 主菜单→声音和视频→音量控制 启动音频混音器。音量控制窗口出现（图 5-7）。拖动滑块以调整音量、低音、高音和其他声音属性。

图 5-7：您可以在此窗口中调整声音的音量和其他属性。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_222_1.png)

![](img/a7eec43a54473e95dc5ea333fecf1bd7_222_2.png)
