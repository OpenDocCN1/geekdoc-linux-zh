

## 使用 Python

License.txt：此文件包含分发插件的许可证。XBMC 项目建议皮肤使用 Creative Commons Attribution-ShareAlike 3.0 许可证，插件使用 GPL 2.0。然而，大多数 copyleft 许可证都可以使用。

**注意：** 为打包目的，扩展/插件/主题/插件是相同的。

## 07 为插件提供设置

设置可以通过文件 resources/settings.xml 提供。这些非常适合用户可配置的选项。

**部分：resources/settings.xml**

```xml
<settings>
<category label="30109">
<setting id="filter" type="bool" label="30101" default="false" />
<setting type="sep" />
<setting id="showunwatched" type="bool" label="30106" default="false" />
<setting id="shownwatched" type="bool" label="30107" default="true" />
<setting id="showunfinished" type="bool" label="30108" default="false" />
<setting type="sep" />
<setting id="viewMode" type="bool" label="30102" default="true" />
<setting id="viewMode" type="number" label="30103" default="504" />
</category>
<category label="30110">
<setting id="cat_hot" type="bool" label="30002" default="true" />
<setting id="cat_new" type="bool" label="30003" default="true" />
</category>
</settings>
```

这里，label 定义了语言 id 字符串，该字符串随后将被用于显示标签。它定义了将用于程序化访问的名称，type 定义了你想要收集的数据类型；它也会影响为该元素显示的 UI。default 定义了设置的默认值。你应该在可能的情况下始终使用默认值，以提供更好的用户体验。

以下是你可以使用的一些重要设置类型...

**text:** 用于基本输入。
**ipaddress:** 用于选择正确的 ip 地址。
**number:** 允许你输入一个数字。XBMC 还将为输入提供屏幕上的数字键盘。
**slider:** 这提供了一种优雅的方式来收集整数、浮点数和百分比值。你可以以下列格式获取 slider 设置：

```xml
<setting label="21223" type="slider" id="sideinput" default="10" range="1,1,10" option="int" />
```

在上面的示例中，我们创建了一个滑块，最小范围为 1，最大范围为 10，步长为 1。在 option 字段中我们说明了我们感兴趣的数据类型——我们也可以将 option 设置为 "float" 或 "percent"。

**bool:** 以开或关的形式提供布尔选择。
**file:** 提供输入文件路径的方式。XBMC 将提供文件浏览器以便选择文件。如果你希望为特定类型的文件进行选择，你可以使用 audio、video、image 或 executable 代替 file。

**folder:** 提供浏览文件夹的方式...

**示例：**

```xml
<setting label="12001" type="folder" id="folder" source="auto" option="writeable"/>
```

这里，source 设置文件夹的起始位置，而 option 设置应用程序的写入参数。

**sep & lsep:** sep 用于在设置对话框中绘制水平线；lsep 用于绘制带文本的水平线。它们不收集任何输入，但用于构建更好的用户界面元素...

```xml
<setting label="21212" type="lsep" />
```

## 08 语言支持

语言支持以位于 resources/languages/[language name] 中的 strings.xml 文件形式提供。这种方法与许多大型软件项目非常相似，包括 Android，其中静态字符串永远不会被重用。

**resource/language/english/string.xml 示例：**

```xml
<?xml version="1.0" encoding="utf-8" standalone="yes"?>
<strings>
<string id="30001">Add subreddit</string>
<string id="30002">Hot</string>
<string id="30003">New</string>
<string id="30004">Top</string>
<string id="30005">Controversial</string>
<string id="30006">Hour</string>
<string id="30007">Day</string>
<string id="30008">Week</string>
<string id="30009">Month</string>
<string id="30010">Year</string>
</strings>
```

正如你在 settings.xml 示例中看到的，所有标签都引用了字符串 id。你也可以有许多其他语言。根据 XBMC 运行的语言，正确的语言文件将自动加载。

在 XBMC Frodo 12.1 之后，strings.xml 将被弃用。Frodo 之后，XBMC 将迁移到基于 GNU gettext 的翻译系统；gettext 使用 PO 文件。你可以使用名为 xbc-mxl2po 的工具将 strings.xml 转换为等效的 PO 文件。

## 09 构建 default.py

由于我们的插件很小，它将包含在 default.py 中。如果你正在开发更复杂的插件，那么你可以在同一目录中创建支持文件。如果你的库依赖于第三方库，你有两种方法。你可以将第三方库放入 resources/lib 文件夹；或将库本身打包到插件中，然后在 addon.xml 文件中将该插件添加为依赖项。

我们的插件使用 reddit.tv。这是从 Reddit 提供的网站，其中包含其读者分享的热门视频。发布在 Reddit 上的视频实际上来源于 YouTube、Vimeo 和 Dailymotion。

我们将使用以下导入开始 default.py：

```python
import urllib
import urllib2
import xbmcplugin
```
