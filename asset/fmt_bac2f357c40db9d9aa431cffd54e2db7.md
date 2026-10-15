
在 Ubuntu 中由于许可问题而缺失。即使你计划在未来的抓取和编码工作中使用 Ogg Vorbis 格式，安装 MP3 支持也是一个好主意，以便覆盖你所有的音频需求。而且这也是一个非常简单的过程。

安装 MP3 播放支持最简单的方法是双击你硬盘上已有的 MP3 文件。会出现一个窗口，询问你是否要搜索播放该文件所需的插件。点击 `Search`，之后会出现另一个窗口，显示你需要安装的内容（图 14-1）。在该窗口中勾选两个复选框，点击 `Install` 按钮，然后在随后出现的确认窗口中点击 `Confirm`。你将被要求输入密码，请输入，然后只需等待过程完成。完成后，你不仅可以播放 MP3 音频文件，还可以播放 MPEG 和 WMV 视频。

![](img/f7cef0df22f9dba5a41777808c98eece_300_0.png)

图 14-1：Ubuntu 帮助你找到所需的插件。

如果你愿意，你也可以通过 Ubuntu 软件中心非常轻松地下载并安装这些插件，只需搜索 `gstreamer`，然后安装 `gstreamer0.10-ffmpeg`（GStreamer ffmpeg 视频插件）、`gstreamer0.10-fluendo-mp3`（Fluendo mp3 解码器 GStreamer 插件）以及 `gstreamer0.10-plugins-ugly`（GStreamer 额外插件）。

至于 MP3 编码支持，它使你能够抓取 CD 并创建自己的节省空间的 MP3 文件，情况就没那么自动了。但这也不是什么大麻烦，因为你只需使用 Ubuntu 软件中心搜索并安装 `gstreamer0.10-plugins-ugly-multiverse` 即可。如果你还想为自己添加 AAC 编码能力，也应同时安装 `gstreamer0.10-plugins-bad-multiverse`。这样你就可以准备就绪，如下一节所述。

## Rhythmbox—你的音频播放器

Ubuntu 中的主要音频播放器称为 Rhythmbox（见图 14-2），它似乎功能上与 Apple 的 iTunes 应用的简化版差不多。这是一款相对易于使用的音频播放器，尽管早期有些怪癖，但在 Linux 世界中已拥有相当多的追随者。要运行 Rhythmbox，只需进入 `Applications` 菜单并选择 `Sound & Video` ▸ `Rhythmbox Music Player`。

![](img/f7cef0df22f9dba5a41777808c98eece_301_0.png)

图 14-2：Rhythmbox 音频播放器

## 向 Rhythmbox 库添加歌曲和专辑

如果你熟悉 Apple 的 iTunes，那么你也应该理解 Rhythmbox 中的库，因为它本质上是相同的概念。Rhythmbox 应该会自动导入你在 `Music` 文件夹中的所有内容，无需你额外操作。如果你更喜欢手动将歌曲添加到 Rhythmbox 库，可以打开首选项窗口（`Edit` ▸ `Preferences`），点击 `Music` 选项卡，然后取消勾选 `Watch my library for new files` 框。之后，你可以通过进入 `Music` 菜单，选择 `Import Folder`，然后导航到你想要添加的新专辑的文件夹，来将新专辑添加到 Rhythmbox 库。如果你想添加同一艺术家的多张专辑，只需导航到并选择该艺术家文件夹即可。如果你只想添加单个音频文件，也可以这样做——选择 `Music` ▸ `Import File`，然后导航到相关歌曲。

如果你不使用导航类型，你也可以通过其他方式添加文件和文件夹。最简单的方法是将你想要添加到库中的文件夹或歌曲拖放到 Rhythmbox 窗口的右窗格中。你也可以直接通过右键单击文件并在出现的弹出菜单中选择 `Open with` ▸ `Open with Rhythmbox` 来将歌曲添加到库中。

## 使用 Rhythmbox 抓取音频 CD

与 iTunes 一样，Rhythmbox 也允许你直接从 CD 抓取歌曲；将其转换为 Ogg Vorbis、MP3 或其他音频格式；然后将抓取的曲目添加到其音乐库中。步骤如下：

1. 打开 `Preferences` 窗口（`Edit` ▸ `Preferences`），点击 `Music` 选项卡，并选择你想要使用的编码格式（`Ogg Vorbis` 为默认值）。完成后，点击 `Close`。除非你经常更改编码格式，否则你不必多次执行此操作。
2. 在 Rhythmbox 窗口的左侧窗格中选择你的音频 CD。
3. 点击 Rhythmbox 窗口右上方的 `Copy to library` 按钮。抓取和编码过程随后将开始，进度将在 Rhythmbox 窗口的右下角显示。完成后，抓取的歌曲将自动出现在 Rhythmbox 库中。

> **NOTE** *如果你尚未安装 `gstreamer0.10-plugins-ugly-multiverse` 包，输出格式菜单中将不会出现 MP3 选项。*

## 浏览 Rhythmbox 库

Rhythmbox 库，你可以通过点击 Rhythmbox 窗口左侧窗格中的 `Music` 使其可见，是你添加到其中的所有音乐的集合。随着收藏的增长，这可能会变得有点难以管理。幸运的是，Rhythmbox 具有一个不错的浏览器功能，像 iTunes 中的那样，可以通过点击图 14-3 所示的 `Browse` 按钮来切换开启或关闭。此功能允许你在主库列表上方两个单独的窗格中查看艺术家和专辑的列表。如果你点击艺术家窗格中的特定艺术家，该艺术家的专辑列表将出现在右窗格中。然后你可以双击该右窗格中的其中一张专辑来播放它。如果你想播放该艺术家的所有专辑，只需双击左侧窗格中的艺术家姓名即可。总的来说，这是一个非常方便的功能。

![](img/f7cef0df22f9dba5a41777808c98eece_302_0.png)

图 14-3：Rhythmbox 中的 Browse 按钮

如果你想为浏览器添加一层分类，你可以添加一个流派窗格。要做到这一点，只需进入 `Edit` 菜单，选择 `Preferences`，选择出现的窗口的 `General` 选项卡，然后选择 `Genres, artists, and albums`。在 Preferences 窗口中点击 `Close` 按钮后，你将在 Rhythmbox 中拥有一个三窗格浏览器（图 14-4）。

![](img/f7cef0df22f9dba5a41777808c98eece_303_0.png)

图 1.4-4：展开分类的 Rhythmbox 浏览器

## 在 Rhythmbox 中创建播放列表

当然，你可以进一步定制以匹配每种情况和你的每种心情。毕竟，有时你会觉得对 Adam Lambert 来说有点太 ethereal 了，而这真是万幸。为了应对这样的时刻，你可以创建播放列表，即按预定顺序播放的歌曲列表。只需把每个播放列表想成一个点播电台……而所有的点播请求都是你自己的。

要在 Rhythmbox 中创建播放列表，请选择 `Music` ▸ `Playlist` ▸ `New Playlist`。当播放列表图标出现在 Rhythmbox 窗口的左窗格中时，输入该列表的名称，然后只需将你想要的歌曲从 `Library` 窗格拖到播放列表图标即可。歌曲本身仍保留在 `Library` 中，所以你实际上并没有移动任何东西——只是创建了别名。

你也可以创建自动播放列表，即会自动扫描 `Library` 以查找符合你创建条件的歌曲的列表。你可以为 `Library` 中某位特定艺术家的所有歌曲或特定流派的歌曲创建一个列表。要做到这一点，只需选择 `Music` ▸ `Playlist` ▸ `New Automatic Playlist`。会出现一个窗口，你可以在其中指定列表应包含的内容。你甚至可以指定列表中想要多少首歌。

创建好列表后，你可以通过单击一次列表，然后单击窗口顶部附近的播放按钮来播放它（或直接双击列表）。

## 通过 Rhythmbox 在线音乐商店

虽然 iTunes 只有 iTunes 商店，但 Rhythmbox 为你提供了多种选择，所有这些都可以通过 Rhythmbox 窗口左窗格中的 `Stores` 标题访问。其中两个商店 Jamendo 和 Magnatune 提供由独立艺术家以 Creative Commons 或开放许可发布的音乐。另一个商店是 Ubuntu One Music Store，它提供来自 7digital 目录的主流艺术家的音乐。那里出售的歌曲不受从其他在线商店购买的许多歌曲中常见的数字版权管理（DRM）限制。

## Rhythmbox 中的其他酷功能

Rhythmbox 包含一些值得注意的酷功能。除了能够管理播客外，它还支持显示专辑封面艺术。如图 14-2 和 14-4 所示，只要你在 Rhythmbox 中播放曲目，该曲目的专辑封面艺术就会自动下载并显示在窗口的左下角（前提是 Rhythmbox 能在网上找到封面）。
