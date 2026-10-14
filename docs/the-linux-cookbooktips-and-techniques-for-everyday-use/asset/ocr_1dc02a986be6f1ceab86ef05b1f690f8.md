The not lame encoder takes two arguments: the name of the input file and the name of the output file.

+   To encode an MP3 file from a WAV file called `september-wind.wav`, type:

```
$ notlame september-wind.wav september-wind.mp3 RET
```

It usually takes some time to encode an MP3 file; when not lame is encoding a file, it continually outputs the current percentage of completion.

> NOTE: Scripts on the download site show how to encode multiple WAV files and how to decode all of the tracks on an audio CD.

# 24.3.2 Converting MP3 to Another Format

```
@sf(Debian): 'sox'
@sf(Debian): 'mpg321'
@sf(WWW): http://home.sprynet.com/~cbagwell/sox.html
@sf(WWW): http://freshmeat.net/projects/mpg321/
```

To convert an MP3 file to another format, use mpg321 (or another command-line MP3 player) to play the file to the standard output, and then use sox to read the resultant raw audio and write it to another file with a specified input format.

+   To convert the MP3 file `remix.mp3` to a WAV file `remix.wav`, type:

```
$ mpg321 -b 10000 -s remix.mp3 | sox -t raw -r 44100 -s -w -c 2 - remix.wav RET
```

# 24.4 Other Tools for Sound Editing

Sound software in Linux is a fast-moving target, and it is impossible for a printed volume to keep up with it; you can stay abreast of the latest developments by checking out Dave Phillips's "Sound & MIDI Software for Linux" page at http://www.bright.net/~dlphilip/linuxsound/. This page is the most comprehensive and up-to-date list of Linux-related sound software available.

As with text editors, there are all manner of sound editors, ranging from simple editors to advanced environments. The following table lists a few of the most popular ones.