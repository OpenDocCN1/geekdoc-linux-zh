You can also create WAV sound files from audio CD tracks by using the `cdcd2wav` command-line application. For example, to convert the second track from an audio CD into a WAV file, type the following command:

```
```bash
cdd2wav -D /dev/cdrom -t2 -Owav
```
```

`cdd2wav` saves the track in a WAV file named `audio.wav`. You can then play the WAV file in XMMS. Watch out though — each track of an audio CD typically takes about 60MB of disk space in WAV format.

Because of legal reasons, the version of XMMS in Fedora Core does not include the code needed to play MP3 files, so you have to translate MP3s into a supported format such as WAV before you can play them. You can use the Ogg Vorbis format for compressed audio files because Ogg Vorbis is a patent- and royalty-free format.

To start XMMS from the GNOME or KDE desktop, choose Main Menu→Sound & Video→Audio Player. XMMS has a simple user interface. To open a sound file, choose Window Menu→Play File, or press L to select a `.wav` or `.ogg` file from the Load File dialog box. Select a file and click Ok. XMMS starts playing the sound file. Figure 4-4 shows a typical XMMS window when it’s playing a sound file.

If you get an **error** message from XMMS, choose Window Menu→Options→Preferences and then select ALSA as the Output Window.

Of course, many music files are in MP3 format. Wouldn’t getting XMMS to play MP3 music be nice? Well, to play MP3 files in XMMS, you have to download the source code for XMMS and build it from scratch. I provide the instructions in Book VI, Chapter 4.

# **Burning a CD**

Fedora Core includes X-CD-Roast, a graphical CD burner application with a lot of features. It can create both data CDs and audio CDs. You can also *rip*

![](bbox=[0.15, 0.58, 0.5, 0.71])