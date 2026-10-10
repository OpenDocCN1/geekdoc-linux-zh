
## 附录 D：iTunes 资料库 XML 格式

### 简介

iTunes 使用一种称为 XML 的结构化格式来存储其音乐资料库。本附录概述了 iTunes 资料库格式。

你可以通过打开 iTunes 偏好设置并切换到“高级”选项卡来查找资料库文件的位置。你可以选择“文件 ⇄ 导出资料库”来创建资料库的副本。在对你自己的资料库文件进行任何修改之前，务必使用此“导出”命令创建副本。

由于 XML 文件只是文本文件，你可以使用任何文本编辑器查看资料库，或者使用 XML 编辑器，例如 Mac OS X 中的属性列表编辑器（Property List Editor）。图 D-1 显示了 Windows 版 Internet Explorer 6 所显示的资料库文件的一部分。图 D-2 显示了 Mac OS X 上属性列表编辑器中显示的相同信息。

### 文件头

资料库的前几行提供了关于 XML 文档类型的信息：

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE plist PUBLIC "-//Apple
  Computer//DTD PLIST 1.0//EN"
  "http://www.apple.com/DTDs/PropertyList-
  1.0.dtd">
<plist version="1.0">
```

`<!DOCTYPE>` 语句包含了指向 Apple 的 XML 文件文档类型定义（DTD）的链接。

文件的其余部分都被包裹在 `<dict>` 标签中。

### Library.xml

![在 Windows 版 Internet Explorer 中显示的资料库部分](img/f481d8a0ca491080698039f72bf96e1b_299_0.png)
**图 D-1.** 在 Windows 版 Internet Explorer 中显示的资料库部分。

![在 Mac OS X 的属性列表编辑器中显示的资料库部分](img/f481d8a0ca491080698039f72bf96e1b_299_1.png)
**图 D-2.** 在 Mac OS X 的属性列表编辑器中显示的资料库部分。

### 创建者和资料库信息

文件的下一节包含提供正在使用资料库的 iTunes 应用程序的版本号以及资料库文件位置的键：

```xml
<key>Major Version</key><integer>1</integer>
<key>Minor Version</key><integer>1</integer>
<key>Application Version</key><string>4.2</string>
<key>Music Folder</key>
<string>file:///localhost/Users/scott/Music/iTunes/iTunes%20Music</string>
```

### 曲目和播放列表

下一节列出了资料库中的所有曲目。整个部分都包裹在 `<dict>` 标签中，每个单独的曲目也是如此。每个曲目的信息以其曲目 ID 键开始，并包含关于该曲目的所有其他详细信息，如下面的示例所示：

```xml
<key>Track ID</key><integer>1165</integer>
<key>Name</key><string>Born Fighter</string>
<key>Artist</key><string>Nick Lowe</string>
<key>Composer</key><string>Nick Lowe</string>
<key>Album</key><string>16 All-Time Lowes</string>
<key>Grouping</key><string>classics</string>
<key>Genre</key><string>Rock</string>
<key>Kind</key><string>MPEG audio file</string>
<key>Size</key><integer>3039019</integer>
<key>Total Time</key><integer>189779</integer>
<key>Start Time</key><integer>71000</integer>
<key>Stop Time</key><integer>142000</integer>
<key>Disc Number</key><integer>1</integer>
<key>Disc Count</key><integer>1</integer>
<key>Track Number</key><integer>1</integer>
<key>Track Count</key><integer>16</integer>
<key>BPM</key><integer>100</integer>
<key>Date Modified</key><date>2004-03-15T01:33:12Z</date>
<key>Date Added</key><date>2004-02-20T01:03:44Z</date>
<key>Bit Rate</key><integer>128</integer>
<key>Sample Rate</key><integer>44100</integer>
<key>Equalizer</key><string>Rock</string>
<key>Comments</key><string>Awesome liver version</string>
<key>Rating</key><integer>60</integer>
<key>Normalization</key><integer>1767</integer>
<key>Compilation</key><true/>
<key>File Type</key><integer>1297106739</integer>
<key>File Creator</key><integer>1397375309</integer>
<key>Location</key><string>file://localhost/Users/scott/Music/
iTunes/iTunes%20Music/Compilations/16%20All-Time%20Lowes/
01%20Born%20Fighter.mp3</string>
<key>File Folder Count</key><integer>4</integer>
<key>Library Folder Count</key><integer>1</integer>
```

在曲目列表之后，会出现播放列表，它们包裹在 `<dict>` 标签中。资料库本身也在此部分中作为播放列表列出。每个播放列表都包含其所含曲目的数组。这是一个普通播放列表的示例：

```xml
<key>Name</key><string>favorites</string>
<key>Playlist ID</key><integer>19338</integer>
<key>Playlist Persistent ID</key><string>F43F2BCA0A367E80</string>
<key>All Items</key><true/>
<key>Playlist Items</key>
<array>
    <dict>
        <key>Track ID</key><integer>1191</integer>
        <key>Track ID</key><integer>1230</integer>
        <key>Track ID</key><integer>1257</integer>
        <key>Track ID</key><integer>1380</integer>
    </dict>
</array>
```

智能播放列表包含略有不同的信息，包括创建播放列表所需的编码数据：

```xml
<key>Name</key><string>not recently played</string>
<key>Playlist ID</key><integer>12525</integer>
<key>Playlist Persistent ID</key><string>7E8BE57B647388FC</string>
<key>All Items</key><true/>
<key>Smart Info</key>
<data>
AQEAAAwAAAAIAAAAZAAAAA...AAAAAA
</data>
<key>Smart Criteria</key>
<data>
U0xzdAABAAAEAAAABAAAAAAAALAAAAAAAALAAAAAAAALAAAAAA
</data>
<key>Playlist Items</key>
<array>
<dict>
<key>Track ID</key><integer>1165</integer>
</dict>
<dict>
<key>Track ID</key><integer>1167</integer>
</dict>
<dict>
<key>Track ID</key><integer>1169</integer>
</dict>
<dict>
<key>Track ID</key><integer>1171</integer>
</dict>
<dict>
<key>Track ID</key><integer>1180</integer>
</dict>
<dict>
<key>Track ID</key><integer>1182</integer>
</dict>
<dict>
<key>Track ID</key><integer>1184</integer>
</dict>
<dict>
<key>Track ID</key><integer>1192</integer>
</dict>
</array>
```

计算机在解析 XML 文件方面比大多数人都擅长。你可以在 codetriangle.com/iTunesXmlParser 找到一个将 iTunes 资料库转换为数组的 PHP 脚本。对于另一种方法以及有关 PHP 的更多信息，请参见 developer.apple.com/internet/opensource/php.html。想了解更多乐趣，请访问 www.itunesregistry.com，这是一个 iTunes 用户可以使用其资料库文件来报告他们正在听什么的地方。

## 索引

- AA 电池，18
- AAC。另见高级音频编码文件，233
- 格式，172
- 绝对引用和相对引用，252
- 账户信息，查看或更改，229
- 适配器，57
- 地址簿，22
- 高级音频编码（AAC），172
- 高级电池信息，63
- 高级选项屏幕，89
- AIFF，173
- AirPort，161
- AirPort Express，162
  - 工作原理，165
- AirTunes
  - 功能，164
  - 局限性，164
- 闹钟
  - 应用程序，147
  - 功能，29
- 专辑，9
- 专辑封面，131, 209, 219
- 使用 Google 查找专辑封面。另见专辑封面
- All Recorder 实用程序，185
- Apple 账户信息屏幕，229
- Apple 和 iPod 新闻与传闻
  - CNET，262
  - Crazy Apple Rumors，263
  - Google 新闻，262
  - Mac Rumors，263
  - MacMinute，262
  - MacNN，262
  - MacSlash，262
  - SlashDot，262
  - SpyMac，263
  - Think Secret，263
  - TidBITS，262
  - Wired，262
  - Yahoo 新闻，262
- 处理 Apple 的 iPod 脚本，13
- AppleScript，133
- AppleScript 功能
  - 清除所有备注，31
  - 剪贴板到备注，31
  - 弹出 iPod，30
  - 列出备注，31
  - MacCentral，31
  - 适合打印，31
- AppleScript Studio 软件，201
- AppleScript 技术，30
- Aqua 用户界面，70
- 在商店周围获取信息，223
- art4iTunes，132
- 艺术家，9, 191
  - 获取信息，235
- A11 Remote Wonder II，166
- 有声书
  - 自定义功能，34
  - 下载，13, 34
  - 功能，34
  - 收听，233
- Audio Hijack，184
- Audio Hijack Pro，184
- 音频 CD 作为备份策略，208
- 自动调整所有列大小，218
- 自动化 CD 抓轨，171, 175
- 自动滚动，112
- B
  - 备用电池包，19
  - 基站。另见通过 WiFi 播放音乐
  - iTunes 中的基本音乐播放功能
    - 播放列表，103
  - 电池图标，恢复，53
  - 电池更换
    - 步骤，62
    - 手术，61
  - Belkin 用于 iPod 的数码相机链接，18
  - Belkin 媒体阅读器，16
  - Belkin 的录音机，14
  - 最佳硬件，177
  - 排行榜
    - 功能，228
    - 局限性，228
  - 比特率列，124
  - 从 iPod 启动，21, 166, 168
  - 广播 iTunes，159
  - 浏览音乐链接
    - 专辑，226
    - 艺术家，226
    - 流派，226
  - 使用浏览器查找音乐，226

