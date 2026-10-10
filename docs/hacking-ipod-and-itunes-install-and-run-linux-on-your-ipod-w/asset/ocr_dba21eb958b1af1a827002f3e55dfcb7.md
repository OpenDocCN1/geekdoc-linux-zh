song. You can use various other values, called *filters*, instead of “song”. Here’s the full set of available filters:

+   - song
+   - artist
+   - album
+   - playlist
+   - genre
+   - composer

You can combine filters to distinguish between different songs with the same name:

```
`<A HREF="ipod:music?song=Yesterday&artist=Bella Cooperman">Classic version</A>`
```

If you use a link that matches more than one song, all the matches are combined into a groovy temporary playlist. With judicious use of filters in song links, you can create playlists that even iTunes would envy. For example, you can grab a subset of an artist’s music:

```
`<a href="ipod:music?artist=Neil Young&genre=rock">Rock out</a>`
```

Because playing a single song is the most common use of this kind of link, it has a special shortcut syntax:

```
`<a href="song=Disappointing Show">Play it</a>`
```

When you click a song link, the iPod normally starts playing the song and goes to the Now Playing screen. You can keep the note on screen instead by using the “Now Playing” element in the tag:

```
`<A HREF="ipod:music?song=Trancey"&%NowPlaying=false">Listen</A>`
```

![](bbox=[0.07, 0.74, 0.15, 0.81])

> **Note** Due to a bug, the nowPlaying tag is ignored in iPod Software 2.1 and iPod Mini 1.0.

# Tips and ideas

+   - Try using song links to make your own *“Name That Tune”* game. Use AppleScript or another automated tool on your computer to select some songs, then build a note with links to the songs.
+   - You can only specify one value for each filter, which means you can’t create a playlist that combines multiple artists or albums, unfortunately.