
如果该行不存在，请添加以下内容：

Load glx

最后，将

Driver "nv"

更改为

Driver "nvidia"

检查是否安装了新的内核模块。查看由 `# lsmod` 生成的列表，并确认 NVdriver 是否在列表中。如果没有，请使用 `# modprobe NVdriver` 加载它并再次检查。

如果到目前为止一切看起来正常，可以通过运行 `# X` 以“裸机”启动来测试 X。如果你看到一个带有 X 形状光标的灰色屏幕，就说明你成功了！使用 `Ctrl+Alt+Backspace` 组合键杀死 X，然后运行 `# telinit 5` 进入第 5 层。

如果在此过程中出现任何问题，请重新阅读 NVdriver 说明并检查你的拼写（我们在尝试过程中将 nvidia 写错了两次）。从 NVIDIA 提供的 PDF 文档中不仅包含安装指南，还包含故障排除和调优信息。你会遇到的唯一问题是，如果你使用了 Red Hat 图形配置工具，它将无法识别 NVIDIA 驱动程序并将其替换为 XFree86 驱动程序。

## 安装《竞技锦霸赛 2003》

免费演示版可以从 http://www.unrealtournament2003.com/ 首页或互联网上的任何其他来源下载；不过，这是一个 96MB 的下载文件。下载完成后，可以使用以下命令安装游戏：

```bash
# sh ./ut2003-Demo-Linux.sh .bin
```

默认情况下，它将安装在 `/usr/local/games/ut2003_demo/`。可以通过以下命令启动游戏：

```bash
$ /usr/local/games/ut2003_demo_ut2003_demo &
```

图 26.14 显示了在 Red Hat Linux 系统上运行游戏的截图。

![](img/446debe023486a07fde575245cf7a3ff_907_0.png)

图 **26.14** 游戏一直是推动硬件和软件开发进步的动力。UT2003 再次推向了极限。

一个实用的功能是通过 Loki 安装程序提供的在线更新（感谢 Loki 为 Linux 分叉了所有那些很棒的游戏！）。只需 `cd` 进入你安装 UT2003 的 `./.updater` 目录，然后运行：

```bash
# ./loki_update /usr/local/games/ut2003_demo/
```

此命令还会为你更新游戏。你可以在 http://www.linuxlinks.com/Software/Games/ 和 http://www.linuxgames.com/ 找到更多 Linux 游戏。

> 在 Linux 中成功玩游戏的关键在于：始终透彻阅读文档，始终透彻调查互联网资源，并始终深入了解你的系统。安装游戏是学习你系统的极佳方法，因为成功的回报非常有趣。

## 相关的 Red Hat 和 Linux 命令

在为 Red Hat Linux 处理多媒体应用工作时，你将使用这些命令：

- cdda2wav—从 CD 复制 WAV 文件；供其他应用程序使用
- cdlabel—为 CD 盒创建标签；用于脚本
- cdp—文本模式 CD 播放器
- cdparanoia—CD 抓取器
- cdrecord—用于录制 CD 的命令行工具
- dvrecord—用于录制 DVD 的命令行工具
- grip—CD 抓取器
- gtoaster—GNOME CD 录制器
- koncd—KDE CD 录制器
- mkisofs—创建 ISO 文件
- xcdroast—CD 录制器

## 音频与音乐

- aumix—控制台音频混器器
- kmid—MIDI 播放器
- kmid2—将 MIDI 转换为数字音频
- mikmod—MOD 音乐播放器
- redhat-config-soundcard—默认声卡配置实用程序
- sndconfig—旧版 Red Hat 声卡配置工具
- sox—音频转换工具
- vorbis-tools—OGG Vorbis 解码器
- xmms—MP3 播放器

## 视频

- kaboodle—KDE 媒体播放器
- mpg321—MPEG 音频播放器
- noatun—KDE 媒体播放器
- smpeg—MPEG 音频/视频播放器
- smpegtv—MPEG 音频/视频播放器
- xatwv—电视查看器
- xine—视频播放器
- xmms—MPEG1/2/3 播放器

## 

- gtkKam—gPhoto2 的前端
- camera—KDE 数字相机实用程序
- dvgrab—使用 Firewire 连接的视频摄像头捕捉实用程序

## 扫描仪

- kooka—KDE 扫描应用程序
- xsane—扫描仪应用程序

## 图形

- eog—Eye of Gnome 图像查看器
- imagemagick—图像处理应用程序
- gimp—GNU 图像处理程序
- qqview—GNOME 图像查看器
- koloredit—KDE 调色板编辑器
- kiconed—KDE 图标编辑器
- kpaint—图形应用程序
- kuickshow—KDE 图像查看试用
- kview—KDE 嵌入式图像查看器
- tpbm-progs—处理 netpbm 格式图形的工具
- xfig—矢量图形应用程序

## 游戏

- maelstrom—太空战斗
- chromium—太空射击
- fortune-mod—显示你的运势
- freeciv—FreeCiv 多人游戏
- joystick—为游戏配置摇杆
- tuxracer—企鹅滑雪障碍赛
- xboard—国际棋

## 参考

- http://www.elis.rug.ca/be/-rsfs/dfs/—CD 文件系统首页。
- http://www.cdcopopyworld.com/—技术信息资源
- http://www.elis.rug.ca/be/-rsfs/dfs/—CD 文件系统首页。
- http://www.cdcopopyworld.com/—技术信息资源
- http://www.elis.rug.ca/be/-rsfs/dfs/—CD 文件系统首页。
- http://www.cdcopopyworld.com/—技术信息资源
- http://www.elis.rug.ca/be/-rsfs/dfs/—CD 文件系统首页。
- http://www.cdcopopyworld.com/—技术信息资源
- http://www.elis.rug.ca/be/-rsfs/dfs/—CD 文件系统首页。
- http://www.cdcopopyworld.com/—技术信息资源
- http://www.elis.rug.ca/be/-rsfs/dfs/—CD 文件系统首页。
- http://www.cdcopopyworld.com/—技术信息资源
- http://www.elis.rug.ca/be/-rsfs/dfs/—CD 文件系统首页。
- http://www.cdcopopyworld.com/—技术信息资源
- http://www.elis.rug.ca/be/-rsfs/dfs/—CD 文件系统首页。
- http://www.cdcopopyworld.com/—技术信息资源
- http://www.elis.rug.ca/be/-rsfs/dfs/—CD 文件系统首页。
- http://www.cdcopopyworld.com/—技术信息资源
- http://www.elis.rug.ca/be/-//dfs/—CD 文件系统首页。
-.://www.cd..

