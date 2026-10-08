
# 13 Populating plug-in content listing

**xbmcgui** contains various routines for handling the content listing inside the plug-in's UI. The first step is to create directory entries which can be selected from the XBMC UI. For this we will use a function called **xbmcplugin.addDirectoryItem**.

For our convenience we will be abstracting addDirectoryItem to suit our purpose, so that we can set name, url, mode, icon image and type easily.

```python
def addDir(name, url, mode, iconImage, type=""):
    u = sys.argv[0] + "?url=" + urllib.quote_plus(url) + "&mode=" + str(mode) + "&type=" + str(type)
    ok = True
    listItem = xbmcgui.ListItem(name, iconImage="DefaultFolder.png", thumbnailImage=iconImage)
    listItem.setInfo(type="Video", infoLabels={"Title": name, ...})
    xbmcplugin.addDirectoryItem(handle=int(sys.argv[1]), url=u, listItem=listItem)
    return ok
```

On the same line, we can build a function to place links as well...

```python
def addLink(name, url, mode, iconImage, description, date):
    u = sys.argv[0] + "?url=" + urllib.quote_plus(url) + "&mode=" + str(mode)
    ok = True
    listItem = xbmcgui.ListItem(name, ...)
    return ok
```

Based on the abstractions we have just created, we can create the base functions which will populate the content. But before we do that, let's first understand how Reddit works. Most of the Reddit content filters are provided through something called **Subreddits**. This allows you to view discussions related to a particular topic; in our plug-in we are interested in showing videos; we also want to show trailers, documentaries etc. We access these using Subreddits. For example, for trailers it would be **reddit.com/r/trailers**. For domains we can use **/domain**, for example, to get all the YouTube videos posted on Reddit, we will call **reddit.com/domain/youtube.com**. Now you may ask what is the guarantee that this Subreddit will only list videos? The answer is that it may not. For that reason we scrape the site ourselves to find videos. More on this in the next step.

The first base function will define is **index()**. This is called when the user starts the plug-in.

```python
def index():
    defaultItems = ["videos", "trailers", "documentaries", "music"]
    entries = defaultEntries[:]
    if os.path.exists(subredditFile):
        fh = open(subredditFile, "r")
        content = fh.read()
        fh.close()
        spl = content.split('\n')
        for i in range(0, len(spl), 1):
            if spl[i]:
                subreddit = spl[i]
                entries.append(subreddit)
            entries.sort()
            for entry in entries:
                if entry in defaultEntries:
                    addDir(entry.title(), ...)
                else:
                    addDir(entry.title(), ...)
            # ... and more logic for domains and translation ...
            xbmcplugin.endOfDirectory(pluginhandle)
```

Here, the **populateItems** takes a call to addSubreddit. ListSorting takes care of sorting out the data based on criteria such as Hot, New etc. It also calls in Reddit's JSON function, which returns easy-to-parse JSON data. We have created a setting entry for all the sorting criteria. Based on what is set, we go ahead and build out the sorted list.

```python
def listSubreddit(subreddit):
    if cat_hot:
        addDir(translation(30002), urlMain + "?subreddit=" + subreddit + "&sort=hot&count=100", "listVideos", "")
    if cat_new:
        addDir(translation(30003), urlMain + "?subreddit=" + subreddit + "&sort=new&count=100", "listVideos", "")
    # ... and more logic for top and translation ...
    xbmcplugin.endOfDirectory(pluginhandle)
```

Similarly for Vimeo:

```python
def getVimeoUrl(id):
    url = "plugin://plugin.video.vimeo/path=/root/video&action=play_video&vid=" + id
    return url
```

And for Dailymotion:

```python
def getDailymotionUrl(id):
    url = "plugin://plugin.video.dailymotion_com/?url=" + id + "&mode=playVideo"
    return url
```

Once we have the video URL resolved into the respective plug-in, playing it is very simple:

```python
def playVideo(url):
    listItem = xbmcgui.ListItem(path=url)
    xbmcplugin.setResolvedUrl(pluginhandle, True, listItem)
```

# Work with Python

```python
def listVideos(url):
    currentUrl = url
    xbmcplugin.setContent(pluginhandle, "episodes")
    content = opener.open(url).read()
    spl = content.split("data")
    for i in range(1, len(spl), 1):
        entry = spl[i]
        try:
            match = re.compile('"title": "(.+?)"', re.DOTALL).findall(entry)
            title = match[0].replace('&amp;', "&").replace('&quot;', '"')
            match = re.compile('"description": "(.+?)"', re.DOTALL).findall(entry)
            description = match[0]
            match = re.compile('"created_utc": (.+?),', re.DOTALL).findall(entry)
            downs = int(match[0].replace("'", ""))
            rating = int(ups*100/(ups+downs))
            if filter and (ups+downs) > filterVoteThreshold and rating < filterRating:
                continue
            title = title + " (%s" % str(rating) + "% Up | " + "%s" % str(ups+downs) + " votes)"
            match = re.compile('"num_comments": (.+?)', re.DOTALL).findall(entry)
            comments = match[0]
            description = dateTime + " | " + str(ups+downs) + " votes: " + str(rating) + "% Up | " + "comments:" + comments + "\n" + description
            match = re.compile('"thumbnail_url": "(.+?)"', re.DOTALL).findall(entry)
            thumb = match[0]
            matchYoutube = re.compile('"url": "http://www.youtube.com/watch\?v=(.+?)"', re.DOTALL).findall(entry)
            matchVimeo = re.compile('"url": "http://vimeo.com/.+?"', re.DOTALL).findall(entry)
            url = ""
            if matchYoutube:
                url = getYouTubeUrl(matchYoutube[0])
            elif matchVimeo:
                url = getVimeoUrl(matchVimeo[0].replace("&", ""))
            if url:
                addLink(title, url, "playVideo", thumb, description, date)
        except:
            pass
        match = re.compile('"after": "(.+?)"', re.DOTALL).findall(entry)
        xbmcplugin.endOfDirectory(pluginhandle)
        if forceViewMode:
            xbmc.executebuiltin("Container.SetViewMode('" + viewMode + "')")
```

In the code listed above, we are opening the URL, then - based on regular expression matches - we are discovering the location title, description, date, ups, downs and rating. We are also locating video thumbnails and then passing them on to XBMC.

Later in the code, we also try to match the URL to a video provider. With our plug-in we are supporting YouTube, Vimeo and DailyMotion. If this is detected successfully, we call the helper functions to locate the XBMC plug-in based playback URL. During this whole parsing process, if any exception is raised, the whole loop is ignored and the next JSON item is parsed.

# 14 Populating the episode view (listing videos)

At this point we have the URL in hand, which returns JSON data; now we need to extract the data out of which will make sense to us.

By looking at the JSON data, we can see there's a lot of interesting information present here. For example, url is set to youtube.com/watch?v=v-n4rZt6Vx; title is set to 'The Counselor - Official Trailer'. url has many other bits of data that we will use, such as ups, downs, num_comments, thumbnail_url and so on. In order to filter out the data that we need, we will use regular expressions.

There is one more thing to note: since we are not presenting directories any more but are ready to place content, we have to set the xbmcplugin.setContent to episodes mode.

# 15 Installing & running the add-on

You can install the add-on using one of the following two methods:

- You can copy the plug-in directory to .xbmc/addons.
- You can install the plug-in from the zip file. To do so, compress the add-on-folder into a zip file using the command:

```bash
$ zip -r plugin.video.ludent.zip plugin.video.ludent
```

To install the plug-in from the zip file, open XBMC, go to System then Add-ons, then click "Install from zip file". The benefit of installing from a zip file is that XBMC will automatically try to install all the dependent plug-ins as well.

Once you have the plug-in installed, you can run it by going to the Videos Add-ons section of XBMC, selecting Get More... and then clicking on LUD Reddit Viewer.

You can access the settings dialog of the plug-in by right-clicking the LUD Reddit Viewer, then selecting "Add-on settings".

So, you have seen how robust and powerful XBMC's extension system is. In this example, we were able to leverage the full power of Python (including those magical regular expression matches) from within XBMC. XBMC itself also offers a robust UI framework, which provides a very professional look for our add-on.

As powerful as it may seem, we have only built a simple plug-in. XBMC's extension system also provides a framework for building fully fledged programs (called Programs). We will cover this in a later issue.
