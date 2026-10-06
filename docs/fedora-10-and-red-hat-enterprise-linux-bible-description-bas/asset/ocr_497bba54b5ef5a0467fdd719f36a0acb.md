# Using ogg123, mpg321, and play command-line players

Command-line music players are convenient if you happen to be working from a shell (GUI) or if you want to play audio files from a script. Here are a few command-line players that might interest you:

+   - **ogg123** — The ogg123 is a good way to play Ogg Vorbis or FLAC files from the command line. From the command line, you can play a file (abc, ogg), a playlist containing multiple music files (--list=/tmp/mownlist), or an HTTP or FTP location (http://example.com/song.ogg). The following is an example of the ogg123 command playing an Ogg Vorbis file from the current directory:

```
$ ogg01-Rhapsody_in_Blue.ogg
Audio Device: PulseAudio

Playing: 01-Rhapsody_in_Blue.ogg
Ogg Vorbis stream: 2 channel, 44100 Hz
Title: Rhapsody in Blue
Artist: George Gershwin
Track number: 1
Total: 8
Album: Rhapsody in Blue
Genre: Instrumental
Time: 00:20.36 [15:29.65] of 15:50.01 (181.6 kbps) Output Buffer 96.9%
```

To stop ogg123 from playing a single song, press Ctrl+C. Do two Ctrl+C keystrokes to quit ogg123 when multiple tracks are queued up. This is part of the vorbistools package, which you can install with yum.

+   - **play** — The play command can be used to play any of the wide range of audio formats supported by sock. The syntax is `play file.xx`. To see what file formats can be played by the `play` command, type `-h` to see a list. The play command is useful if you are looking in directories of sound effects, voice content, or other audio files that aren't your typical multimedia audio types. (You need the sock package installed, which comes with Fedora and RHEL, to be able to play.)

+   - **mpg321** — This is similar to ogg123, but it's used (as you might guess) to play MP3 files. Like ogg123, you can play a file [abc.mp3], a playlist containing multiple music files (--list=/tmp/mownlist), or an HTTP or FTP location (http://example.com/song.mp3). Unlike mpg321 doesn't come with Fedora or RHEL. You can get the mpg321 package from the Livna.org site.

# Using MIDI audio players

MIDI stands for Musical Instrument Digital Interface. MIDI files are created from synthesizers and other music devices. MIDI files tend to be smaller than other kinds of audio files, because of storing the content they contain the notes played. The MIDI player reproduces the notes to sound like a variety of MIDI instruments.