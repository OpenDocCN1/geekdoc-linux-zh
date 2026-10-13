
![](img/d9230b719dc0efd80851f363d8c6f571_210_0.png)

1. 读取相机说明并使用相机的菜单选项将 USB 设置为 Mass Storage。

如果相机不支持 USB Mass Storage，你无法使用此过程访问照片。

2. 使用相机自带电缆将数码相机连接到 USB 端口并打开相机。

3. 输入以下命令挂载相机存储介质：

```
mount /mnt/camera
```

相机图标出现在 GNOME 桌面上。

5. 双击 GNOME 桌面的相机图标。

相机的内容出现在 Nautilus 文件管理器中。你可以双击文件夹找到包含照片的文件夹。通常这些数字照片是带有 `.jpg` 扩展名的 JPEG 文件。在默认视图下，Nautilus 显示照片的缩略图，所以你不需要担心加密文件名。

6. 点击选择照片将其复制到硬盘。

你也可以在终端中使用 `cp` 命令将所有或部分图像复制到硬盘上的目录。例如，为了将所有 JPEG 照片复制到当前目录，输入

```
cp /camera/*.jpg
```

# 185 多媒体应用

3. 要查看相机是否被检测，输入以下命令：

```
cat /proc/bus/devices
```

输出显示相机为质存储设备。从第二个 T: 行开始的所有行都涉及 Nikon Coolpix 2500 相机。你可以在输出中看到一些细节，如制造商名称和相机型号。

+ 7. 当照片下载完成后，右键点击 GNOME 桌面上的相机图标，并在弹出菜单中选择“卸载卷”（Unmount Volume）。

Linux 会将相机从 `/mnt/camera` 目录中卸载，删除 `/mnt/camera` 目录，并删除添加到 `/etc/fstab` 文件中的那行行。

+ 8. 关闭相机电源并将 USB 线从电脑上拔掉。

既然你可以像访问任何其他存储设备一样访问相机，谁还需要 gtcam 呢！

### 播放音频 CD

GNOME 和 KDE 都带有 CD 播放器应用程序。要播放音频 CD，你需要一张声卡，并且该声卡必须配置为可在 Linux 下工作。

如果你正在使用 GNOME 桌面，可以使用 GNOME CD 播放器应用程序播放音频 CD。通过选择“主菜单→音频与视频→CD 播放器”来启动 GNOME CD 播放器。图 4-2 显示了该 CD 播放器正在播放音频 CD 中的一个曲目。

![](img/d9230b719dc0efd80851f363d8c6f571_212_0.png)

GNOME CD 播放器显示 CD 标题和当前曲目的名称。freedb.org。GNOME CD 播放器从 freedb.org 获取歌曲 —— 这是互联网上的一个开源 CD 数据库（端口 888 的 freedb.freed.org）。你需要连接互联网以便 CD 播放器从 CD 数据库下载歌曲信息。CD 播放器下载特定 CD 的信息后，会将这些信息缓存在本地数据库中以备后用。CD 播放器的用户界面非常直观，你可以轻松学会。一个很好的功能是你可以根据标题选择曲目，如图 4-3 所示。

如果你使用 KDE 作为桌面，可以在 KDE 中找到类似的音频 CD 播放器。通过选择“主菜单→音频与视频→KsCD”启动 CD 播放器。

# 多媒体应用 187

![](img/d9230b719dc0efd80851f363d8c6f571_213_0.png)

图 4-3：

在

GNOME CD

播放器中，

你

选择

一个特定的

音频曲目

进行播放。

第二卷

第四章

核心应用

探索 Fedora

# 播放音频文件

你可以使用 Rhythmbox 或 XMMS 打开并播放音频文件。拥有大型 MP3 音乐库的用户喜欢 Rhythmbox，但 Fedora Core 自带的版本不包含 MP3 功能。XMMS 默认不安装，但你可以在以 root 身份登录时，通过按照以下步骤从伴随 DVD 中安装它：

+ 1. 挂载本书的伴随 DVD。

将 DVD 插入 DVD 驱动器，并在终端窗口中输入 `mount /mnt/cdrom`（如果 DVD 驱动器是系统上的第二个 CD/DVD 驱动器，你可能需要将 `cdrom` 改为 `cdrom1`）。

+ 2. 安装 XMMS RPM。

在终端窗口中输入以下命令（假设 DVD 驱动器已挂载在 `/mnt/cdrom`）：

```
cd /mnt/cdrom/Fedora/RPMS
rpm -ivh xmms*
```

XMMS 可以播放许多类型的音频文件，包括 Ogg Vorbis、FLAC（自由无损音频编码，一种类似于 MP3 的音频格式）和 Windows WAV。你可以在 Linux 系统的 `/usr/share/sounds` 目录下播放许多 WAV 音频文件 —— 这些文件通常以 `.wav` 扩展结尾。

## 188 多媒体应用

你还可以使用 `cda2wav` 命令行音频从音频 CD 曲目创建 WAV 音频文件。例如，要将音频 CD 的第二个曲目转换为 WAV 文件，请输入以下：

```
cda2wav -D /dev/cdrom -t2 -Owav
```

`cda2wav` 将曲目保存为名为 `audio.wav` 的 WAV 文件。你可以在 XMMS 中播放该 WAV 文件。但要注意——音频 CD 的每个曲目在 wav 格式下通常占用约 60MB 的磁盘空间。

由于法律原因，Fedora Core 中的 XMMS 版本不包含播放 MP3 的代码，因此在播放它们之前，你必须将 MP3 转换为 WAV 等支持的格式。你可以使用 Ogg Vorbis 格式压缩音频文件，因为 Ogg Vorbis 是一种免专利且免版税的格式。

从 GNOME 或 KDE 桌面启动 XMMS，选择“主菜单：声音：音频播放器”。XMMS 具有简单的用户界面。要打开音频文件，选择“窗口菜单：播放”或按 L 键从加载对话框中选择 `.wav` 或 `.ogg` 文件。选择文件并点击 OK。XMMS 将播放音频文件。图 4-4 显示了 XMMS 在播放音频文件时的典型窗口。

媒体播放器

你可以在 XMMS 中播放不同类型的音频文件。

![](img/d9230b719dc0efd80851f363d8c6f571_214_0.png)

如果你收到来自 XMMS 的错误消息，选择“窗口菜单：选项：偏好”并选择 ALSA 作为输出插件。

当然，许多音乐文件是 MP3 格式。能让 XMMS 播放 MP3 音乐就好了吧？嗯，要在 XMMS 中播放 MP3 文件，你必须下载 XMMS 的源码并从头开始编译。我在第六卷第四章中提供了说明。

### 刻录 CD

Fedora Core 包含了 X-CD-Roast，这是一类功能丰富的图形化 CD 刻录应用程序。它可以创建数据 CD 和音频 CD。你还可以从音频 CD 将音乐提取（复制）到硬盘上的文件，并将其刻录到新的音频 CD 上。在接下来的章节中，我将要说明如何使用 X-CDRoast。如果你想了解更多，请访问 www.xdcroast.org。

X-CDRoast 在本书的伴随 DVD 上，但它并非默认安装。要安装 X-CDRoast，请在 root 身份登录时遵循以下步骤：

# 1. 挂载本书的伴随 DVD。

将 DVD 插入 DVD 驱动器，并在终端窗口中输入 `/mnt/cdrom`（如果驱动器是系统上的第二个 CD/DVD 驱动器，你可能需要将 `cdrom` 改为 `cdrom1`）。

# 2. 安装 xcdroast RPM。

在终端窗口中输入以下命令（假设驱动器已挂载在 `/mnt/cdrom`）：

```
cd /mnt/cdrom/Fedora/RPMS
rpm -ivh xcdroast*
```

X-CDRoast 依赖许多外部程序来完成工作。如果这些程序不存在，X-CDRoast 功能将无法使用。虽然 Fedora Core 提供了 X-CDRoast，但某些程序并未包含其中。例如，X-CDRoast 需要 mpg23 程序来处理音频。Fedora Core 不带 mpg23 程序，以便你可以将音频录制到 CD。在刻录 CD 之前，你需要一个 CD 刻录器，这种刻录器可以是外部的。内部刻录器通常是 IDE（也称为 ATAPI）设备连接到电脑的。外部 CD-RW 驱动器通常连接到电脑的 USB 端口。如果你使用 CD-RW 驱动器并将其连接到 USB 端口，X-Roast 会自动识别该设备。

要启动 X-Roast，请从 GNOME 或 KDE 桌面选择“主菜单：系统：CD 刻录机”（该菜单在安装 xcdroast RPM 后出现）。如果你没有以 root 身份登录，将提示输入 root 密码。X-Roast 会扫描 CD/DVD 设备并将显示在对话框中。点击 OK 继续。X-Roast 允许

![](img/d9230b719dc0efd80851f363d8c6f571_215_0.png)

![](img/d9230b719dc0efd80851f363d8c6f571_215_1.png)

第二卷

第四章

核心应用

探索 Fedora

## 190 多媒体应用
