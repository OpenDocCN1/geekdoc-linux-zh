# # Chapter 7: Music, Video, and Images in Linux

There is also a tiny set of buttons on the bottom of the Playlist Editor screen. These are the same buttons as those on the main screen used for selecting different tracks or playing, pausing, stopping, or ejecting the current track.

# ## Using ogg123, mpg321, and play command-line players

Command-line music players are convenient if you happen to be working from a shell (no GUI) or if you want to play audio files from a shell script. Here are a few command-line players that might interest you:

+   *   **ogg123** — The `ogg123` command is a good way to play Ogg Vorbis or FLAC audio files from the command line (you may need to install the vorbis-tools package). From the command line, you can play a file (`abc.ogg`), a playlist containing multiple music files (`--list=/tmp/myownlist`), or an HTTP or FTP location (`http://example.com/Ogg Vorbis.ogg`). The following is an example of the `ogg123` command playing an Ogg Vorbis file from the current directory:

```
$ ogg123 01-Rhapsody in Blue.ogg
Audio Device:  Pulse@audi output

Playing: 01-Rhapsody in Blue.ogg
Ogg Vorbis stream: 2 channel, 44100 Hz
Title: Rhapsody in Blue
Artist: George Gershwin
Track number: 1
Tracktotal: 8
Album: Rhapsody in Blue
Genre: Instrumental
Time: 00:20.36 [15:29.65] of 15:50.01 (181.6 kbps) Output Buffer  96.9%
```

To stop `ogg123` from playing a single song, press Ctrl+C. Do two Ctrl+C keystrokes to quit `ogg123` when multiple tracks are queued up. This command is part of the vorbis-tools package, which you can install with `yum`.

+   *   **play** — The `play` command can be used to play any of the wide range of audio formats supported by sox. The syntax is simply `play file.xx`. To see what file formats can be played by the `play` command, type `sox -h` to see a list. The `play` command is useful if you are looking in directories of sound effects, voice content, or other audio files that aren't your typical mainstream multimedia audio types. You need the sox package installed, which comes with Fedora, to be able to use `play`.)

+   *   **mpg321** — This is similar to the `ogg123` command, but it's used (as you might guess) to play MP3 audio files. Like `ogg123`, you can play a file (`abc_song.mp3`), a playlist containing multiple music files (`-list /tmp/Myownlist`), or an HTTP or FTP location (`http://example.com/song.mp3`). Unlike `ogg123`, `mpg321` doesn't come with Fedora. You can get the `mpg321` package from the rpmfusion.org site.