

您可以直接按艺术家、专辑或歌曲标题在网站上查找信息。是否曾好奇过有多少首歌曲的标题中包含特定单词，例如“old”或“myxomatosis”？现在您可以找出答案了！方法如下：

- 1. 前往 Gracenote 网站 www.gracenote.com/music（图 6–2）。
- 2. 输入您要搜索的信息。您可以专门在艺术家、专辑或歌曲字段中查找，也可以选择在所有字段中搜索。
- 3. 为了避免包含将搜索词作为单词一部分的虚假结果（例如，搜索“old”却得到包含“hold”、“cold”等结果），请勾选“Exact Phrase”（精确短语）复选框。
- 4. 选择每次显示 10 个或 25 个结果。
- 5. 点击 Search（搜索）以获取第一组结果。

搜索结果中的每个条目都是指向该歌曲条目的链接。您可以点击一首歌曲以获取有关该歌曲的更多信息。

![](img/f481d8a0ca491080698039f72bf96e1b_165_0.png)

**图 6–2：Gracenote CBDB 搜索页面。**

![](img/f481d8a0ca491080698039f72bf96e1b_166_0.png)

要查看更多来自 Apple 的酷脚本，请参阅第 2 章中的*使用 Apple 的 iPod 脚本*。

### 勾选或取消勾选多个曲目

“Enable | Disable Selected Tracks”脚本可以让您开启或关闭所有已选中歌曲的复选框。iTunes 将复选框用作播放歌曲的一种主开关。如果播放列表中包含未勾选的歌曲，iTunes 将直接跳过它。当您为新智能播放列表设置规则时，可以指定是否允许包含未勾选的歌曲。要使用此脚本，请选中您要更改状态的歌曲，然后运行脚本。您将看到一个对话框，询问您对歌曲是表示赞成（启用）还是反对（禁用）（图 6-3）。

![](img/f481d8a0ca491080698039f72bf96e1b_166_1.png)

这里提供了一种无需脚本即可批量启用或禁用大量歌曲的方法。按住 Command 键并点击（在 Windows 上是 Ctrl+点击）任意歌曲的复选框。该播放列表中的所有歌曲的复选框都会被开启或关闭。

### 导出库列表

iTunes 包含一个内置命令（File ⇨ Export Library），用于将您的音乐库导出为 XML 文件。XML 是一种很棒的数据交换格式，但对人眼来说可读性不高。为了说明这一点，图 6-4 展示了一个导出的库 XML 文件的部分示例。

如果您希望生成一个面向人类而非计算机的库文本文件，请使用 Apple 的“Library Summary”脚本。此脚本为您提供多种格式的选择来生成摘要。要查看可用格式，请在运行脚本时点击“Set Prefs”按钮。您将看到图 6-5 中所示的列表。

选择格式后，脚本会审视您的库内容并生成一个显示所有音乐文件的简单文本文件。配套脚本“iPod Library Summary”为您的 iPod 执行相同的功能。

![](img/f481d8a0ca491080698039f72bf96e1b_166_2.png)

**图 6-3：“Enable | Disable Selected Tracks”脚本会显示此对话框。**

```xml
Library.xml

They\288ight\286iants/Robot\280Parade/Robot\280Parade\280Demo></string>

<key>File Folder Count</key><integer>6</integer>

<key>Library Folder Count</key><integer>1</integer>

</dict>

<key>36</key>

<dict>

<key>Track ID</key><integer>36</integer>

<key>Name</key><string>Deep Blue Something - Breakfast</string>

<key>Kind</key><string>MPEG audio file</string>

<key>Size</key><integer>4114480</integer>

<key>Total Time</key><integer>257097</integer>

<key>Date Modified</key><date>2004-02-21T22:01:52Z</date>

<key>Date Added</key><date>2004-02-20T01:03:02Z</date>

<key>Bit Rate</key><integer>128</integer>

<key>Sample Rate</key><integer>44100</integer>

<key>Normalization</key><integer>3350</integer>

<key>File Type</key><integer>1347174745</integer>

<key>File Creator</key><integer>1397375309</integer>

<key>Location</key><string>file:///localhost/Users/scott/Music/
iTunes/iTunes/280Music//291Library/280Music/iTuxp/Loss/285-17-03/Unknown/280Artist/
Unknown/280Album/Deep/280Blue/280Something/28-280Breakfas</string>

<key>File Folder Count</key><integer>6</integer>

<key>Library Folder Count</key><integer>1</integer>

</dict>

<key>38</key>

<dict>

<key>Track ID</key><integer>38</integer>

<key>Name</key><string>Robot Parade (Demo)</string>

<key>Artist</key><string>They Might Be Giants</string>

<key>Album</key><string>Robot Parade</string>

<key>Kind</key><string>MPEG audio file</string>

<key>Size</key><integer>452936</integer>

<key>Total Time</key><integer>28290</integer>

<key>Track Number</key><integer>1</integer>

<key>Date Modified</key><date>2004-03-14T23:55:11Z</date>

<key>Date Added</key><date>2004-02-20T01:03:32Z</date>

<key>Bit Rate</key><integer>128</integer>

<key>Sample Rate</key><integer>44100</integer>

<key>Normalization</key><integer>2476</integer>
```

**图 6-4：** iTunes 将库文件导出为 XML。

您可以使用 XML 导出功能将播放列表传输到新计算机。有关详情，请参阅第 5 章中的[将您的播放列表移动到另一台计算机](https://example.org/move-playlists)。

## 杂项快速技巧

Apple 脚本集中的几个脚本仅提供快捷方式，用于实现那些可以通过其他更繁琐但较不“黑客”方式达成的功能。这些包括“Open Scripts folder”、“Play Random Track”和“Set Genre to Specific EQ”。我将在本节中逐一描述它们。

![](img/f481d8a0ca491080698039f72bf96e1b_168_0.png)

**图 6-5：** 为您的库摘要选择多种格式。

如果您想查看 iTunes 脚本文件夹，可以导航到 Finder（访达），找到您的 Home（主）目录，然后深入找到 iTunes Scripts 文件夹。但使用 iTunes 中的“Open Scripts folder” AppleScript 快捷得多。此脚本会切换到 Finder 并在新窗口中打开该文件夹。

您可以使用“Play Random Track”脚本快速查找并播放您库中的任意曲目。当然，您可以通过进入库、闭上眼睛并在歌曲列表中双击某处来达成相同结果，但该脚本更好，因为当您闭眼点击时，可能会点错位置，不小心启动导弹或发生其他糟糕的事情。使用此脚本的另一个优点是，它不会让您离开当前的播放列表。

“Set Genre to Specific EQ”脚本对于确保例如所有爵士乐曲目都设置了爵士均衡器非常有用。要使用该脚本，您只需选择一个播放列表、一个流派和一个均衡器设置。其工作原理如下：

- 1. 从 Scripts（脚本）菜单中选择“Set Genre to Specific EQ”。
- 2. 您可以决定是将特定均衡器设置应用于整个库中特定流派的所有曲目，还是仅应用于选定的播放列表（图 6-6）。点击您想要的选项。

![](img/f481d8a0ca491080698039f72bf96e1b_168_1.png)

**图 6-6：** 选择是更改特定流派所有歌曲的均衡器设置，还是仅更改特定播放列表中的设置。

- 3. 如果您在第 2 步中选择了“playlist”（播放列表），脚本会要求您选择所需的播放列表。
- 4. 接下来，您将获得所有可能流派的列表。选择您要查找的那个。
- 5. 在下一步中，您选择要应用的均衡器预设。
- 6. 选择均衡器预设后，脚本在遍历您的歌曲并应用所选设置时，会显示一个进度对话框。

![](img/f481d8a0ca491080698039f72bf96e1b_169_0.png)

> 只需多几步操作，就可以将任意一组曲目设置为相同的均衡器设置。首先，选中所有您要设置的曲目。然后选择 File（文件） > Get Info（获取信息），进入 Options（选项）选项卡。从均衡器预设下拉菜单中选择您想要的设置，点击 OK（确定），即可完成。

## Doug 的 iTunes AppleScripts

iTunes 脚本网站上无可争议的王者是位于 http://www.malcolmadams.com/itunes/ 的 Doug's AppleScripts for iTunes。这个受欢迎网站的站长是 Doug Adams，他自 2001 年初以来一直撰写、收集并发布 iTunes 脚本。该网站现在包含超过 260 个脚本。许多脚本巧妙且非常有用，其中一些达到了“没有它我可怎么办？”的程度。这些脚本免费提供，如果您使用并喜欢它们，可以在网站上进行捐款以帮助网站维持运行，我非常推荐这种做法。

在本节中，我将讨论来自 Doug's AppleScripts 的一些最出色的脚本。该网站非常活跃，新脚本不断涌入，因此您应该经常回来查看最新内容。

### 处理重复曲目

随着您的数字音乐收藏增长，您不可避免地要处理重复曲目的问题。有时您会忘记自己抓取了哪些 CD，或者将音乐从一个磁盘移到另一个磁盘，甚至可能购买了一首您已经抓取过的曲目。您可以使用本节描述的一组实用脚本来帮助清理重复项。

#### 移除重复项

此脚本只是查看选定的播放列表中同一曲目的多个副本。如果发现重复项，它会从播放列表中删除多余的副本。要被视为重复项，两个（或多个）播放列表条目必须指向完全相同的曲目：即磁盘上的同一个文件。因此，具有相同歌曲名称但不同的曲目，或者甚至具有相同名称和艺术家但位于不同专辑（例如“精选集”）的曲目，都不被视为重复项。Remove Duplicates 完成后会提供一份报告，如图 6–7 所示，但它不会在您删除重复项之前给您预批准其工作的机会——您只能信任它。

