
## `getDbPath()`

此函数返回视频 SQLite 数据库文件的位置。XBMC 将库和播放信息存储在 SQLite DB 文件中。视频和音乐有单独的数据库，位于 `.xbmc/userdata/Database` 文件夹内。我们要关注的是视频数据库。它以 `MyVideo` 为前缀。

```python
def getDbPath():
    path = xbmc.translatePath("special://userdata/Database")
    files = os.listdir(path)
    if file[:3] == 'MyVideo':
        latest = video
        if file > latest:
            latest = file
    return os.path.join(path, latest)
```

## `getPlayCount(url)`

一旦我们有了数据库位置，我们就可以使用简单的 SQL 查询获取播放次数。`MyVideo` 数据库包含一个名为 `files` 的表，它根据文件名记录在 XBMC 中播放的所有视频文件。在这种情况下，它将是一个 URL。

```python
dbPath = getDbPath()
conn = sqlite3.connect(dbPath)
c = conn.cursor()

def getPlayCount(url):
    c.execute('SELECT playCount FROM files WHERE strFilename=?', [url])
    result = c.fetchone()
    if result:
        result = result[0]
        return int(result)
    return 0
    return -1
```

上面的表格是 `files` 表的一个示例。

## `addSubreddit()`

我们的插件允许用户添加自己的 Subreddit。此函数从用户那里获取 Subreddit 输入，然后将其保存在插件数据文件夹内的 `subreddits` 文件中。

以下代码设置了 `subreddits` 文件的位置：

```python
subredditsFile = xbmc.translatePath("special://profile/addon_data/*+addonID*"/subreddits")
```

这转换为 `.xbmc/userdata/addon_data/plugin.video_ludent/subreddits`。

```python
def addSubreddit():
    keyboard = xbmc.Keyboard('', 'translation(30001)')
    if keyboard.isConfirmed() and keyboard.getText():
        subreddit = keyboard.getText()
        fh = open(subredditsFile, 'a')
        fh.write(subreddit + '\n')
        fh.close()
```

此函数还展示了如何从用户那里获取文本输入。在这里，我们调用带有文本标题的 `Keyboard` 函数。一旦检测到键盘，它就将带有换行符的输入写入 `subreddits` 文件。

## `getYouTubeUrl(id)`

当我们定位到一个要播放的 YouTube URL 时，我们会将其传递给 YouTube 插件 (`plugin.video.youtube`) 来处理播放。为此，我们需要以特定格式调用它。

```python
def getYouTubeurl(id):
    url = "plugin://plugin.video.youtube/`?/root/ ?/playlist=yt_video&id=videoID=" + id
    return url
```

## 教程

### 使用 Python 为 XBMC 制作扩展

#### LinuxDeveloper

Vimeo 的情况也类似：

```python
def getVimeoUrl(id):
    url = "plugin://plugin.video.vimeo?path=\"root\"&action=play_video&videoid=" + id
    return url
```

Dailymotion 的情况如下：

```python
def getDailyMotionUrl(id):
    url = "plugin://plugin.video.dailymotion.com?url=" + id + "&mode=playVideo"
    return url
```

一旦我们将视频 URL 解析到相应的插件中，播放它就非常简单了。

```python
def playVideo(url):
    listItem = xbmcgui.ListItem(path=url)
    xbmcplugin.setResolvedUrl(pluginhandle, True, listItem)
```

#### 13 填充插件内容列表

`xbmcplugin` 包含用于处理插件 UI 中内容列表的各种例程。第一步是创建目录条目，这些条目可以从 XBMC UI 中选中。为此，我们将使用一个名为 `xbmcplugin.addDirectoryItem` 的函数。

为了方便起见，我们将对 `addDirectoryItem` 进行抽象，以适应我们的需求，使我们能够轻松设置名称、URL、模式、图标图像和类型。

```python
def addDir(name, url, mode, image, type=""):
    u = sys.argv[0] + "?url=" + urllib.quote_plus(url) + "&mode=" + str(mode) + "&type=" + str(type)
    ok = True

    liz = xbmcgui.ListItem(name,
        iconImage="DefaultFolder.png",
        thumbnailImage=image)
    liz.setInfo(type="Video",
        infoLabels={"Title": name})
    ok = xbmcplugin.addDirectoryItem(handle=int(sys.argv[1]), url=u, listItem=liz, isFolder=True)
    return ok
```

基于同样的思路，我们可以构建一个函数来放置链接...

```python
def addLink(name, url, mode, iconimage, description, date):
    u = sys.argv[0] + "?url=" + urllib.quote_plus(url) + "&mode=" + str(mode)
    ok = True
    liz = xbmcgui.ListItem(name,
        iconImage="DefaultVideo.png",
        thumbnailImage=iconimage)
    liz.setInfo(type="Video",
        infoLabels={"Title": name, "Plot": description, "Aired": date})
    liz.setProperty("IsPlayable", "true")
    ok = xbmcplugin.addDirectoryItem(handle=int(sys.argv[1]), url=u, listItem=liz)
    return ok
```

基于我们刚刚创建的抽象，我们可以创建填充内容的基础函数。但在这样做之前，让我们先了解一下 Reddit 的工作原理。大多数 Reddit 内容过滤器是通过称为 Subreddit（子版）的东西提供的。这允许你查看与特定主题相关的讨论：在我们的插件中，我们感兴趣的是展示视频；我们还希望展示预告片、纪录片等。我们使用 Subreddit 来访问这些内容。例如，对于预告片，它可以是 `reddit.com/r/trailers`。对于域名，我们可以使用 `/domain`；例如，要获取所有发布在 Reddit 上的 YouTube 视频，我们将调用 `reddit.com/domain/youtube.com`。现在你可能会问，这个 Subreddit 的目的是什么，它只列出视频吗？答案是它可能不会。因此，我们自己去抓取网站以找到视频。我们将在下一步中详细介绍这一点。

我们要定义的第一个基础函数是 `index()`。当用户启动插件时会调用此函数。
