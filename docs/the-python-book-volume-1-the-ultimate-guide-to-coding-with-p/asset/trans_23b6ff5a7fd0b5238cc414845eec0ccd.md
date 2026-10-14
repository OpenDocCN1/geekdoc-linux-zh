

## 10 初始化

在初始化过程中，我们将从 settings.xml 读取各种设置。设置可以按以下方式读取：

```
addon = xbmcaddon.Addon()
filterRating = int(addon.getSetting("filterRating"))
filterVoteThreshold = int(addon.getSetting("filterVoteThreshold"))
```

为了读取类型为 bool 的设置，你需要做类似以下操作：

```
filter = addon.getSetting("filter") == "true"
```

我们同时设置了主 URL、插件句柄以及其用户代理：

```
pluginHandle = int(sys.argv[1])
urlMain = "http://www.reddit.com"
userAgent = "Mozilla/5.0 (Windows NT 6.2; WOW64; rv:22.0) Gecko/20100101 Firefox/22.0"
opener = urllib2.build_opener()
opener.addheaders = [('User-Agent', userAgent)]
```

## 11 读取本地化字符串

如前所述，XBMC 使用 strings.xml 来提供文本。为了读取这些字符串，你需要使用 getLocalizedString。

```
translation = addon.getLocalizedString(30002)
```

在此示例中，translation(30002) 在英文环境下运行时将返回字符串 "Hot"。

```
import xbmcgui
import xbmcaddon
```

除 xbmcplugin、xbmcgui 和 xbmcaddon 外，其余都是标准 Python 库，可通过 pip 在 PyPI（Python 包索引）上获取。由于 XBMC 的 Python 运行时已内置所有组件，因此你无需自行安装任何库。

urllib 和 urllib2 用于 HTTP 通信。socket 用于网络 I/O；re 用于正则表达式匹配；sqlite3 是访问 SQLite 嵌入式数据库的 Python 模块；xbmcplugin、xbmcgui 和 xbmcaddon 包含 XBMC 专用的例程。

| idFile | idPath | strFilename | playCount | lastPlayed | dateAdded |
| 1 | 1 | plugin://plugin. |  | 2013-08-06 23:47 |  |
| 2 | 2 | plugin://plugin. | 1 | 2013-08-07 22:42 |  |
| 3 | 2 | plugin://plugin. | 1 | 2013-08-08 00:09 |  |
| 4 | 2 | plugin://plugin. | 1 | 2013-08-08 00:55 |  |
| 5 | 2 | plugin://plugin. | 1 | 2013-08-08 00:58 |  |

## 12 构建辅助函数

在本步骤中，我们将查看一些重要的辅助函数。

上表是 files 表的示例。

getDbPath()：此函数返回视频 SQLite 数据库文件的位置，XBMC 将库和播放信息存储在 SQLite DB 文件中。视频和音乐有各自的数据库，位于 .xbmc/userdata/Database 文件夹内。我们关注的是视频数据库。其前缀为 MyVideos...

```
def getDbPath():
    path = xbmc.translatePath("special://userdata/Database")
    files = os.listdir(path)
    latest = ""
    for file in files:
        if file[8] == "MyVideos" and file[-3:] == ".db":
            if file > latest:
                latest = file
    return os.path.join(path, latest)
```

getPlayCount(url)：一旦我们获得了数据库位置，就可以使用简单的 SQL 查询获取播放次数。MyVideo 数据库包含一个名为 files 的表，它按文件名记录 XBMC 中播放的所有视频文件。在此情况下它将为 URL。

```
dbPath = getDbPath()
conn = sqlite3.connect(dbPath)
c = conn.cursor()
```

```
def getPlayCount(url):
    c.execute("SELECT playCount FROM files WHERE strFilename=?", [url])
    result = c.fetchone()
    if result:
        result = result[0]
        if result:
            return int(result)
    return -1
```

addSubreddit()：我们的插件允许用户添加自己的 Subreddit。此函数从用户处获取 Subreddit 输入，然后将其保存在 addon 数据文件夹内的 subreddits 文件中。

以下设置了 subreddits 文件位置：

```
subredditsFile = xbmc.translatePath("special://profile/addon_data/"+addonID+"/subreddits")
this translates into .xbmc/userdata/addon_data/plugin.video.ludent/subreddits
```

```
def addSubreddit():
    keyboard = xbmc.Keyboard('', translation(30001))
    keyboard.doModal()
    if keyboard.isConfirmed() and keyboard.getText():
        subreddit = keyboard.getText()
        fh = open(subredditsFile, 'a')
        fh.write(subreddit+'\n')
        fh.close()
```

此函数还演示了如何从用户处获取文本输入。在这里我们使用文本标题调用 Keyboard 函数。一旦检测到键盘，它就会将输入写入 subreddits 文件并加上换行符。

getYoutubeUrl(id)：当我们定位到要播放的 YouTube URL 时，我们会将其传递给 YouTube 插件（plugin.video.youtube）来处理播放。为此，我们需要以特定格式调用它...

```
def getYoutubeUrl(id):
    url = "plugin://plugin.video.youtube/?path=/root/video?action=play_video&videoid=" + id
    return url
```
