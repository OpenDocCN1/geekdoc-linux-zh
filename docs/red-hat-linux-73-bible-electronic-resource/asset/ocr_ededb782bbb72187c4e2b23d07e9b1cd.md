# Using MP3 audio players

One of the most popular, and controversial, audio formats is the MPEG layer 3 audio format (MP3). This format produces relatively small music files that can produce excellent sound quality for recorded music. MP3 is becoming the format of choice for high-quality music distribution on the Web.

An MPEG file is usually identifiable by the .mp3 suffix. For music, 1MB of MPEG sound plays about one minute of music. Files that play only spoken words can hold many more minutes of content per megabyte.

There are literally thousands of MPEG music files available on the Web. Because of the lawsuits from the music industry to stop copyright infringement, many sites that once promoted the free exchange of music files (such as MP3.com and Napster.com) are moving toward subscription/fee-based businesses. If you are okay with the fees, these services are a great way to get the songs you like in the time it takes to do a download.

For playing MP3 content in Red Hat Linux, I describe, in the following sections, the mpg321 command (text-based), the xmms player, and the freempp player (X Window-based). In general, mpg321 is the more reliable way to play an MP3 (or other MPEG format) audio file, while the xmms player has a great interface.

> **NOTE:** The RealPlayer, described later in this chapter, is also capable of playing MP3 audio files. Its primary function, however, is to play RealMedia files (.ram) and streaming video and audio.

# Playing MP3 with mpg321

The mpg321 player is a free version of the not-free mpg123 player. Besides playing MPEG layer 3 files (MP3), the mpg321 utility also plays MPEG layer 1 and layer 2 files. This utility runs at the command line, by entering the command and the name of the file (or files) you want to play. Here is an example:

```
$ mpg321 music_file.mp3
```

There are several options available with mpg321. You can test your MP3 file, without producing any output, using the `-t` option. There are also several options that allow you to decode or mix only selected channels. If you use the verbose option (`-v`), you can see the frame numbers being played and the elapsed time (and time remaining). The Verbose output looks similar to this:

```
$ mpg321 -v music_file.mp3
Frame# 2456 [3456), Time: 01:40.34 [01:23.52],
```

Output from mpg321 is usually directed to your sound card (usually /dev/audio or /dev/dsp). You can also direct output directly to the speaker (-o s), headphones (-o h), or the line-out connector (-o l). To play the output faster, use the `-d #` option, where # is