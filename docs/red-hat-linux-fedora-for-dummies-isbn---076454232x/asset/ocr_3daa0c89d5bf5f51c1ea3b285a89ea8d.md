One good source for audio streams is `www.shoutcast.com`. Click any of the Tune In! buttons and Mozilla downloads several playlists and launches MPlayer to play the music via the playlists.

*Playlists* are files that store the locations of one or more audio and video streams. For example, if you click any of the Shoutcast streams (at `www.shoutcast.com`), Mozilla saves the playlist to the `/tmp` directory, starts MPlayer, and directs it to play the playlists. The playlist MIME type, `x-scpls`, was inserted into Mozilla as a helper application when you installed the MPlayer packages.

Alternatively, you can click the Save to disk button and save the playlist to your home directory. You can then manually start MPlayer from a terminal emulator window or the Run Program utility with the command `mplayer -playlist playlist.pls`.

![](bbox=[0.13, 0.3, 0.21, 0.38])

You can use MPlayer to play music files too. Suppose that you use *grip* in Chapter 11 to save some music to a file named `track1.wav`. Enter this command to play that file:

```
mplayer track1.wav
```

Press the Control key and then the C key (Ctrl-c) to end the session.

You can use MPlayer to listen to all sorts of streams. The entire world of Internet radio and — hopefully, soon — video broadcast is open to you. MPlayer will only become more versatile and useful.

MPlayer plays DVDs too! Use the command `grep -i dvd /var/log/dmesg` to locate the DVD device file. For example, your DVD device file should be something like `/dev/hdd`. Next, create a *soft link file* so that MPlayer knows where to find the DVD drive: `ln -s /dev/hdd /dev/dvd`. Start MPlayer, right-click the MPlayer - Video window and choose Open->Play DVD. The DVD plays.

![](bbox=[0.13, 0.59, 0.21, 0.66])

The first MPlayer RealAudio (using the RTSP protocol) plug-in was just recently released from `www.live.com/mplayer`. The plug-in is still too young for easy use, but soon will be. Keep an eye on this system. When the Live.com RTSP plug-in for MPlayer matures, you can listen to an outstanding interview with The Man himself — Linus Torvalds — by opening this URL from gmplayer or MPlayer:

![](bbox=[0.13, 0.7, 0.21, 0.77])

```
rtsp://audio.npr.org/fa/20010604.fa.rm
```

In this clip, Terri Gross, from National Public Radio, conducts an interview during the summer of 2001 on her program, “Fresh Air.” Linus discusses the development of Linux, his life in Silicon Valley, and other matters. You can also use the commercial RealPlayer8 to listen to this or any RealAudio stream. The section in Chapter 11 about plugging in plug-ins describes where to obtain the RealPlayer8 RPM package.