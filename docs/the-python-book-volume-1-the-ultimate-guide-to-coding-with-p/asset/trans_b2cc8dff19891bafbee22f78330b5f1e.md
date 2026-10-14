
```
def listVideos(url):
    currentUrl = url
    xbmcplugin.setContent(pluginHandle, "episodes")
    content = opener.open(url).read()
    spl = content.split("content")
    for i in range(0, len(spl), 1):
        entry = spl[i]
        try:
            match = re.compile("title": "(.*?)", re.DOTALL).findall(entry)
            title = match[0].replace("&amp;", "&")
            match = re.compile("description": "(.*?)", re.DOTALL).findall(entry)
            description = match[0]
            match = re.compile("created_utc": "(.*?)", re.DOTALL).findall(entry)
            downs = int(match[0].replace(")", ""))
            rating = int(ups*100/(ups+downs))
            if filterRating and (ups+downs) > filterVoteThreshold and rating < filterRating:
                continue
            title = title + " ("+str(rating)+"%)"
            match = re.compile("num_comments": "(.*?)", re.DOTALL).findall(entry)
            comments = match[0]
            description = dateTime() + " | " + str(ups+downs)+" votes: " + str(rating)+"% Up | " + comments + " comments\n"+description
            match = re.compile("thumbnail_url": "(.*?)", re.DOTALL).findall(entry)
            thumb = match[0]
            matchYoutube = re.compile("url": "http://www.youtube.com/watch?v=(.*?)", re.DOTALL).findall(entry)
            matchVimeo = re.compile("url": "http://vimeo.com/(.*?)", re.DOTALL).findall(entry)
            url = ""
            if matchYoutube:
                url = getYoutubeUrl(matchYoutube[0])
            elif matchVimeo:
                url = getVimeoUrl(matchVimeo[0].replace("#", ""))
            if url:
                addLink(title, url, 'playVideo', thumb, description, date)
        except:
            pass
    match = re.compile("after": "(.*?)", re.DOTALL).findall(entry)
    xbmcplugin.endOfDirectory(pluginHandle)
    if forceViewMode:
        xbmc.executebuiltin("Container.SetViewMode("+viewMode+")")
```

## 14 填充剧集视图（列出视频）

此时我们已经获得了返回 JSON 数据的 URL；现在我们需要从中提取出对我们有意义的数据。

通过查看 JSON 数据，你可以发现这里存在大量有趣的信息。例如，url 被设置为 youtube.com/watch?v=n4rTzTVxBE，title 被设置为 ‘The Counselor – Official Trailer’。此外还有许多我们将会用到的其他数据位，比如 ups、downs、num_comments、thumbnail_url 等等。为了筛选出我们需要的数据，我们将使用正则表达式。

还有一点需要注意：由于我们不再呈现目录，而是准备放置内容，因此必须将 xbmcplugin.setContent 设置为剧集模式。

在左侧列出的代码中，我们打开了 URL，然后基于正则表达式匹配来获取位置、标题、描述、日期、ups、downs 和评分。我们还查找视频缩略图，并将它们传递给 XBMC。

在代码的后面部分，我们还尝试将 URL 匹配到视频提供商。我们的插件支持 YouTube、Vimeo 和 Dailymotion。如果成功检测到，我们会调用辅助函数来查找基于 XBMC 插件的播放 URL。在整个解析过程中，如果抛出任何异常，整个循环将被忽略，并继续解析下一个 JSON 项。

## 15 安装并运行插件

你可以使用以下两种方法之一安装插件：

- 你可以将插件目录复制到 .xbmc/addons。
- 你可以通过 zip 文件安装插件。为此，请使用以下命令将插件文件夹压缩为 zip 文件：
  $ zip -r plugin.video.ludent.zip plugin.video.ludent

要从 zip 文件安装插件，请打开 XBMC，进入 System（系统），然后选择 Add-ons（插件），再点击 ‘Install from zip file（从 zip 文件安装）’。从 zip 文件安装的好处是，XBMC 会自动尝试安装所有依赖的插件。

插件安装完成后，你可以通过进入 XBMC 的 Videos Add-ons（视频插件）部分，选择 Get More…（获取更多…），然后点击 LUD Reddit Viewer 来运行它。

你可以通过右键点击 LUD Reddit Viewer，然后选择 ‘Add-on settings（插件设置）’ 来访问插件的设置对话框。

因此，你已经看到了 XBMC 的扩展系统是多么健壮和强大。在这个例子中，我们能够在 XBMC 内部充分利用 Python 的全部功能（包括那些神奇的正则表达式匹配）。XBMC 本身也提供了一个健壮的 UI 框架，使我们的插件看起来非常专业。

尽管它看起来功能强大，但我们只构建了一个视频插件。XBMC 的扩展系统还提供了一个框架，用于构建完整的程序（称为 Programs）。我们将在后面的文章中介绍这一点。
