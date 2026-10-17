
`button.png`
文件 编辑 视图 帮助
`<- [ ] [ ] [ ] [ ]`
`100 x 42` 像素 `4.6 kB` `100%` `1/8`

![](img/7b6ecabd34062cd153290258f3b9cd5b_116_2.png)

## 模拟 Photoshop

`GIMP` 应用是一个很棒的，但许多熟悉 `Adobe Photoshop` 的人认为其默认界面并不友好![](img/7b6ecabd34062cd153290258f3b9cd5b_117_0.png)

然而，可以使用自定义主题替换默认的 `GIMP` 配置文件夹以模拟 `Photoshop` 的视觉效果。用于此目的流行的 `GimpPs` 主题可以在 `GitHub` 仓库获取，这需要在系统中安装 `Git` 软件包才能克隆 `GimpPs` 主题。原始 `GIMP` 配置文件夹的备份、`Git` 软件包的安装以及 `GimpPs` 主题的克隆可以通过 `Linux Terminal` 中的命令轻松实现：

`GimpPs` 主题支持 `GIMP 2.8`，在其他版本上可能失败。安装说明在编写时是正确的，但可能会发生变化。可以在 `github.com/doctormo/GimpPs` 找到更多详情。

- 点击**菜单、管理、终端 (Menu, Administration, Terminal)** 启动命令行“终端”窗口

- 在提示处，精确地输入此命令重命名 `GIMP` 配置文件夹 – 并创建备份 `mv ~/gimp-2.8 ~/gimp-2.8-backup`

- 接下来，输入此命令安装 `Git` 软件包 `sudo apt-get install git-all`

### 续

输入您的密码，然后在被问及时按 `Y` 键并按回车继续安装![](img/7b6ecabd34062cd153290258f3b9cd5b_118_0.png)

完成后，精确地输入此命令从 `GitHub` 仓库克隆主题文件夹

```
sh - c "$curl -fSL https://raw.githubusercontent.com/doctormo/GimpPS/master/tools/install.sh"
```

这里的反斜杠字符仅允许命令继续到下一行![](img/7b6ecabd34062cd153290258f3b9cd5b_118_1.png)

```
mike@linuxpc:~$ sh - c "$curl -fSL https://raw.githubusercontent.com/doctormo/GimpPS/master/tools/install.sh"
Cloning Gimps...
Cloning into /home/make/gimp-2.8...
remote: Counting objects: 81, done.
remote: Compressing objects: 100% (78/78), done.
remote: Indexing objects: 100% (delta 1)
Unpacking objects: 100% (81/81), done.
Gimps successfully installed
```

克隆会创建一个配置文件夹。可以使用两个命令恢复备份

`rm - r ~/gimp-2.8`

`mv ~/gimp-2.8-BAK ~/gimp-2.8`

点击“菜单、图形、GNU图像处理程序”启动 `GIMP` 应用 – 看到窗口布局和感觉现在模拟了 `Photoshop`

## 观看电影

许多 `Linux` 发行版都包含一个快速、轻级的媒体播放器应用 (`xplayer`)，它可以播放许多文件格式的音频和视频内容，包括 `AVI`、`MPG`、`WMV`、`WAV`、`MP3` 等。在 `Google Play` 商店中，该应用甚至被名为“全格式视频播放器”。在 `Mint` 中，它是音频或视频文件播放的默认媒体播放器：

![](img/7b6ecabd34062cd153290258f3b9cd5b_119_0.png)

- 1 点击“菜单”、“音频视频”、“媒体播放器”来启动应用

- 2 点击“文件”、“打开”来启动“选择电影或播放列表”对话框，显示您的“视频”文件夹中的内容

媒体播放器还支持字幕——点击“查看”、“字幕”、“下载电影字幕”，然后选择语言并点击“查找”按钮来搜索字幕文件。

| 选择电影或播放列表 | | | | |
|---|---|---|---|
| 主页 | | 大小 | 修改日期 |
| `mike` | | | |
| `Destrec` | | | |
| `Documents` | | `HOW TO TRAIN YOUR DRAGON.mp4` | | |
| `Images` | | | | |
| `Pictures` | | | | |
| 支持的文件 | | | | |
| 取消 | 添加目录 | | | |

![](img/7b6ecabd34062cd153290258f3b9cd5b_119_1.png)

- 3 选择电影，然后点击“添加”按钮使其立即在显示区域开始播放

点击“音量”按钮并拖动弹出滑块来调整音量级别。

| `HOW TO TRAIN YOUR DRAGON 3.mp4` | | |
|---|---|---|
| 文件 编辑 查看  声音 帮助 | |
| 火龙总动员 | 隐藏的世界 | |
| 官方预告片 | | |
|  进/暂停 | 音量 全屏 播放列表 | |
| `0:05/2:38` | | |

...续

- 点击**暂停**按钮停止播放

- 拖动窗口角来更改其大小——查看显示区域中电影周围出现的边界区域

![](img/7b6ecabd34062cd153290258f3b9cd5b_120_0.png)

> 您可以通过拖动滑块来快进暂停的电影，或者将光标置在显示区域上并滚动鼠标轮。

- 点击**查看，放大**以使电影适应显示区域宽度

- 点击**播放**按钮恢复播放

![](img/7b6ecabd34062cd153290258f3b9cd5b_120_1.png)

> 点击**文件，属性**可以有关当前电影文件的详细信息。

- 点击**编辑，截屏**将当前电影帧的图像放置在您的“图片”文件夹中

## 播放音乐

`Rhythmbox` 音乐播放器非常适合播放音乐文件，它还是播客聚合器——以及互联网电台调谐器：

- 点击“菜单”、“音频视频”、“Rhythmbox”来启动 `Rhythmbox` 应用

- 在“库”面板中选择“音乐”，然后点击工具栏上的“导入”按钮

![](img/7b6ecabd34062cd153290258f3b9cd5b_121_0.png)

![](img/7b6ecabd34062cd153290258f3b9cd5b_121_1.png)

播放按钮在播放期间将变为暂停按钮。

使用下拉菜单选择包含音乐文件的文件夹，例如您的“音乐”文件夹内的子文件夹

![](img/7b6ecabd34062cd153290258f3b9cd5b_121_2.png)

右键点击音目并选择“删除”将其从播放列表中删除。

![](img/7b6ecabd34062cd153290258f3b9cd5b_121_3.png)

![](img/7b6ecabd34062cd153290258f3b9cd5b_121_4.png)

您也可以右键点击音乐文件图标并选择“打开方式”，使用 `Rhythmbox` 来播放它。

- 查看 `Rhythmbox` 列出所选文件夹内的音乐文件为“轨道”，

- 点击列表中的轨道以进行选择，点击“导入已选轨道”按钮创建播放列表

...续

点击播放按钮从“轨道 1”开始播放，或双击列表中的任何轨道来播放该轨道

![](img/7b6ecabd34062cd153290258f3b9cd5b_122_0.png)

当开始播放音乐、播客或电台时，系统托盘中会添加一个图标。您可以关闭 `Rhythmbox` 窗口，播放将继续。点击 `F` 图标并使用出现面板上的控件来控制播放，或点击 `X` 退出播放。

![](img/7b6ecabd34062cd153290258f3b9cd5b_122_1.png)

在“库”面板中选择“播客”，然后点击工具栏上的“添加”按钮并按主题搜索播客

![](img/7b6ecabd34062cd153290258f3b9cd5b_122_2.png)

![](img/7b6ecabd34062cd153290258f3b9cd5b_122_3.png)

在“库”面板中选择“电台”，然后双击列表中的电台文件来开始播放它

![](img/7b6ecabd34062cd153290258f3b9cd5b_122_4.png)

## 流媒体内容

`VLC` 播放器是一个强大的跨平台媒体播放器，它还是互联网电台调：器：`Linux` 发行版中可以播放许多文件格式的音频和视频内容

![](img/7b6ecabd34062cd153290258f3b9cd5b_123.png)

- 通过在终端中运行命令来获取您的 `IP` 地址

- 点击“媒体”、“流”来打开对话框

![](img/7b6ecabd34062cd153290258f3b9cd5b_124.png)

- 您的 `IP` 地址可能与示例中的不同
