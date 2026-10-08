# Work with Python

```
import xbmcgui
import xbmcaddon
```

Apart from xbmcplugin, xbmcgui and xbmcaddon, the rest are all standard Python libraries which are available on PyPI (Python Package Index) via pip. You will not need to install any library yourself since the Python runtime for XBMC has all the components built-in.

*urllib* and *urllib2* help in HTTP communication. *socket* is used for network I/O. *re* is used for regular expression matching. *sqlite3* is the Python module for accessing an SQLITE embedded database; *xbmcplugin*, *xbmcgui* and *xbmcaddon* contain the XBM C-specific routine.

# 10 Initialising

During the initialisation process, you will be reading various settings from *settings.xml*. Settings can be read in the following way:

```
addon = xbmcaddon.Addon()
filterRating = int(addon.
getSetting("filterRating"))
filterVoteThreshold = int(addon.getSetting("filterVoteThreshold"))
```

In order to read settings of type bool you will need to do something like:

```
filter = addon.getSetting("filter") == "true"
```

We are also setting the main URL, plug-in handle and the user agent for it:

```
pluginhandle = int(sys.argv[1])
urlMain = "http://www.reddit.com"
userAgent = "Mozilla/5.0 (Windows NT
6.2; WOW64; rv:22.0) Gecko/20100101
Firefox/22.0"

opener = urllib2.build_opener()
opener.addheaders = [('User-Agent',
userAgent)]
```

# 11 Reading localised strings

As mentioned, XBMC uses *strings.xml* to serve up the text. In order to read those strings, you will need to use *getLocalized String*.

```
translation = addon.
getLocalizedString(translation(30002)
```

In this example, *translation(30002)* will return the string "Hot" when it is running in an English environment.

| idFile | idPath | strFilename | play_Count | lastPlayed | dateAdded |
| :----- | :---- | :---------- | :--------- | :--------- | :--------- |
| 1 | 1 | plugin//plugin. | 1 | 2013-08-06 23:47 | |
| 2 | 2 | plugin//plugin. | 1 | 2013-08-07 22:42 | |
| 3 | 2 | plugin//plugin. | 1 | 2013-08-08 00:09 | |
| 4 | 2 | plugin//plugin. | 1 | 2013-08-08 00:55 | |
| 5 | 2 | plugin//plugin. | 1 | 2013-08-08 00:58 | |

# 12 Building helper functions

In this step we will look at some of the important helper functions.

**getDBPath():** This returns the location of the SQLiTE database file for videos. XBM C stores library and playback information in SQLiTE DB files. There are separate databases for videos and music, located inside the .xbmc/userdata/ Database folder. We are concerned with the videos DB. It is prefixed with "MyVideos…"

```
def getDBPath():
path = xbmc.
translatePath("special://userdata/
Database")

files = os.listdir(path)
latest = ""
for file in files:
if file[8:] == 'MyVideos'
and file[-3:] == '.db':
if file > latest:
latest = file

return os.path.join(path,
latest)
```

**getPlayCount(url):** Once we have the database location, we can get the play count using a simple SQL query. The MyVideo database contains a table called *files*, which keeps a record of all the video files played in XBM C by filename. In this case it will be a URL.

```
dbPath = getDBPath()
conn = sqlite3.connect(dbPath)
c = conn.cursor()

def getPlayCount(url):
c.execute('SELECT playCount FROM
files WHERE strFilename=?', [url])
result = c.fetchone()
if result:
result = result[0]
if result:
return int(result)

return 0

return -1
```

The above table is an example of a files table.

**addSubreddit():** Our plug-in allows users to add their own Subreddit. This function takes the Subreddit input from the user, then saves it in the *subreddits* file inside the addon data folder.

The following sets the subreddits file location:

```
subredditFile = xbmc.
translatePath("special://profile/
addon_data/-addonID"/ subreddits")
this translates into _xbmc/
userdata/addon_data/plugin_video_lucent/subreddits
```

```
def addSubreddit():
keyboard = xbmc.Keyboard('',
translation(30001))
keyboard.doModal()
if keyboard.isConfirmed() and
keyboard.getText():
subreddit = keyboard.
getText()

fh = open(subredditFile,
'a')

fh.write(subreddit+'\n')
fh.close()
```

This function also demonstrates how to take a text input from the user. Here we are calling the Keyboard function with a text title. Once it detects the keyboard, it writes the input in the subreddits file with a newline character.

**getYouTubeUrl(id):** When we locate a YouTube URL, to play, we pass it on to the YouTube plug-in (*plugin.video.youtube*) to handle the playback. To do so, we need to call it in a certain format...

```
def getYouTubeUrl(id):
url = ":plug-in://plugin.
video.youtube/?root=/root/
&videoAction=play_video&id=" +
id

return url
```