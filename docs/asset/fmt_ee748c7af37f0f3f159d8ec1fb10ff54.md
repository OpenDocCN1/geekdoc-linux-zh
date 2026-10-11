
<?xml version="1.0" encoding="UTF-8"?>

<!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">

```
<!DOCTYPE 语句包含了指向 Apple 其 XML 文件的文档类型 (DTD)。文件的其余部分在 <dict> 标签中。
```

# 附录 D — iTunes 库格式

## 创建者和库信息

文件的下一个部分包含使用库的应用版本号以及库文件的位置：

```xml
<key>Major Version</key><integer>1</integer>
<key>Minor Version</key><integer>1</integer>
<key>Application Version</key><string>4.2</string>
<key>Music Folder</key>
<string>file://localhost/Users/scott/Music/iTunes%20/</string>
```

## 歌曲和播放列表

下一个部分列出了库中的所有歌曲。整个部分封装在 `<dict>` 标签中，每条歌曲都以其歌曲 ID 键开始，并包含有关歌曲的所有其他细节，如下：

```xml
<key>ID</key><integer>1165</integer>
<key>Name</key><string>Born Fighter</string>
<key>Artist</key><string>Nick Lowe</string>
<key>Composer</key><string>Nick Lowe</string>
<key>Album</key><string>16 All-Time Lowes</string>
<key>Grouping</key><string>classics</string>
<key>Genre</key><string>Rock</string>
<key>Kind</key><string>MPEG audio file</string>
<key>Size</key><integer>303019</integer>
<key>Total Time</key><integer>189779</integer>
<key>Start Time</key><integer>71000</integer>
<key>Stop Time</key><integer>142000</integer>
<key>Disc Number</key><integer>1</integer>
<key>Disc Count</key><integer>1</integer>
<key>Track Number</key><integer>1</integer>
<key>Track Count</key><integer>16</integer>
<key>BPM</key><integer>100</integer>
<key>Date Modified</key><date>2004-03-15T01:31:12Z</date>
<key>Date Added</key><date>2004-02-20T01:03:44Z</date>
<key>Bit Rate</key><integer>128</integer>
<key>Sample Rate</key><integer>44100</integer>
```

### 第三部分 — 附录

```xml
<key>Rating</key><integer>60</integer>
<key>Normalization</key><integer>1767</integer>
<key>Compilation</key><key>true</key>
<key>File Type</key><integer>1297106739</integer>
<key>File Creator</key><integer>1397375309</integer>
<key>Location</key><string>/local/Users/scott/Music/iTunes%20Music/Compilations/16%20All-Time%20Lowes/01%20Born20Fighter.mp3</string>
<key>File Folder Count</key><integer>4</integer>
<key>Library Folder Count</key><integer>1</integer>
```

在列表列表之后，播放列表出现在被 `<dict>` 标签包围的地方。库本身也作为一个列表列在本节中。每个播放列表都包含一个其所包含的曲目数组。这里是一个普通播放列表的示例：

```xml
<key>Name</key><string>favorites</string>
<key>Playlist ID</key><integer>19338</integer>
<key>Playlist Persistent ID</key><string>F43F2BCA0A367E80</string>
<key>All Items</key><key>true</key>
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

智能播放列表可能包含略不同的信息，包括播放列表的编码数据：
```xml
<key>Name</key><string>not recently played</string>
<key>Playlist ID</key><integer>12525</integer>
<key>Playlist Persistent ID</key><string>7E8BE57B647388FC</string>
<key>All Items</key><key>true</key>
<key>Smart Info</key>
```

```xml
<data>
AQEAAAAAAAAIAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA
</data>
```

## 附录 D — iTunes 库 XML 格式

```xml
<key>Smart Criteria</key>
<data>
U0xzAABAEAAABAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA
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
