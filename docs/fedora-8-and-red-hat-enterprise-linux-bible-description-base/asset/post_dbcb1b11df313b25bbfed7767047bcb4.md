
Ripping songs from a CD or copying them from the Web so that they are in an accessible directory.

Inserting a music CD in your CD-ROM drive. (xmms expects the CD to be accessible from `/dev/cdrom`.)

From the Applications menu, select Sound & Video → Audio Player. The X Multimedia System player appears.

Click the Eject button. The Load files window appears.

If you have inserted a CD, the content of that CD appears in the Files pane. (If it doesn’t, change to `/dev/cdrom`, `/media/cdrom` or `/media/cdrecorder`, as appropriate.) Select the files you want to add to your Playlist and click the Add Selected Files or the Add All Files in Directory button to add all songs from the current directory. To add audio files from your file system, browse your files and directories and click the same buttons to add the audio files you want. Select Close.

Click the Play List button (the tiny button marked PL) on the console. A Playlist Editor window appears.

Double-click the music file and it starts to play.

With a file selected and playing, here are a few actions you can take:

- **Control play** — Buttons for controlling play are what you would expect to see on a physical CD player. From left to right, the buttons let you go to a previous track, play, pause, stop, go to the next track, or eject the CD. The Eject button opens a window, allowing you to load the next file.
- **Adjust sound** — Use the left slider bar to adjust the volume. Use the right slider bar to change the right-to-left balance.
- **Display time** — Click in the elapsed time area to toggle between elapsed time and time remaining.
- **View file information** — Click the button in the upper-left corner of the screen to see the XMMS menu. Then select View File Info. You can often find out a lot of information about the file: title, artist, album, comments, and genre. For an Ogg file, you can see specific information about the file itself, such as the format, bit rate, sample rate, frames, file size, and more. You can change or add to the tag information and click Save to keep it.

When you are done playing music, click the Stop button to stop the current song. Then click the X in the upper-right corner of the display to close the window.

Special features of the XMMS Audio Player let you adjust high and low frequencies using a graphic equalizer and gather and play songs using a Playlist Editor. Click the button marked EQ next to the balance bar on the player to open the Equalizer. Click the button marked PL next to that to open the Playlist Editor.

### Using the Equalizer

The Equalizer lets you use slider bars to set different levels to different frequencies played. Bars on the left adjust lower frequencies, and those on the right adjust higher frequencies. Click the EQ button to open the Equalizer. Here are tasks you can perform with the Equalizer:

- If you like the settings you have for a particular song, you can save them as a Preset. Set each frequency as you like it and click the Preset button. Then choose Save → Preset. Type a name for the preset and click OK.
- To reload a preset you created earlier, click the Preset button and select Load → Preset. Select the preset you want and click OK to change the settings.

The small window in the center/top of the Equalizer shows the sound wave formed by your settings. You can adjust the Preamp bar on the left to boost different levels in the set range.

### Using the Playlist Editor

The Playlist Editor lets you put together a list of audio files that you want to play. You can add and delete files from this list, save them to a file, and use them again later. Click the PL button in the XMMS window to open the Playlist Editor.

The Playlist Editor allows you to:

- **Add files to the playlist** — Click the Add button. The Load Files window appears. Select the directory containing your audio files (it’s useful to keep them all in one place) from the left column. Then either select a file from the right column and click Add selected files or click Add all files in the directory. Click OK. The selected file or files appear in the playlist. You can also drag music files from the nautilus file manager onto the playlist window to add the files to the playlist.
- **Select files to play** — To select from the files in the playlist, use the previous track and next track buttons in the main XMMS window. The selected file is highlighted. Click the Play button to play that file. Alternatively, you can double-click on any file in the playlist to start it playing.
- **Delete files from the playlist** — To remove files from the playlist, select the file or files you want to remove (next/previous track buttons), right-click the playlist window, and click Remove → Selected. The selected files are removed.
- **Sort files on the playlist** — To sort the playlist in different ways, click and hold the Misc button and move the mouse to select Sort List. Then you can select Sort List to sort by Title, Filename, Path and Filename, or Date. You can also randomize or reverse the list.
- **Save the playlist** — To save the current playlist, hold the mouse button down on the List button and then select Save. Browse to the directory you want, and then type the name you want to assign to the playlist and click OK.
- **Load the playlist** — To reload a saved playlist, click the List button. Select a previously saved playlist from the directory in which you saved it and click OK.

There is also a tiny set of buttons on the bottom of the Playlist Editor screen. These are the same buttons as those on the main screen used for selecting different tracks or playing, pausing, stopping, or ejecting the current track.

### Using ogg123, mpg321, and play command-line players

Command-line music players are convenient if you happen to be working from a shell (no GUI) or if you want to play audio files from a shell script. Here are a few command-line players that might interest you:

- **ogg123** — The `ogg123` command is a good way to play Ogg Vorbis or FLAC audio files from the command line. From the command line, you can play a file (`abc.ogg`), a playlist containing multiple music files (`--list=/tmp/myworld`), or an HTTP or FTP location (`http://example.com/ogg.ogg`). The following is an example of the `ogg123` command playing an Ogg Vorbis file from the current directory:

```
$ ogg123 01-Rhapsody in Blue.ogg
Audio Device:    Advanced Linux Sound Architecture (ALSA) output
Playing: 01-Rhapsody in Blue.ogg
Ogg Vorbis stream: 2 channel, 44100 Hz
Title: Rhapsody in Blue
Artist: George Gershwin
Track number: 1
Track total: 8
Album: Rhapsody in Blue
Genre: Instrumental
Time: 00:20.36 [15:29.65] of 15:50.01 (181.6 kbps) Output Buffer   96.9%
```

To stop ogg123 from playing a single song, press Ctrl+C. Do two Ctrl+C keystrokes to quit ogg123 when multiple tracks are queued up.

- **play** — The `play` command can be used to play any of the wide range of audio formats supported by sox. The syntax is simply `play file.xx`. To see what file formats can be played by the `play` command, type `sox -h` to see a list. The `play` command is useful if you are looking in directories of sound effects, voice content, or other audio files that aren’t your typical mainstream multimedia audio types. (You need the sox package installed, which comes with Fedora and RHEL, to be able to use `play`.)
- **mpg321** — This is similar to the `ogg123` command, but it’s used (as you might guess) to play MP3 audio files. Like `ogg123`, you can play a file (`abc.mp3`), a playlist containing multiple music files (`--list /tmp/Myworld`), or an HTTP or FTP location (`http://example.com/ogg.ogg`). Unlike `ogg123`, `mpg321` doesn’t come with Fedora or RHEL. You can get the `mpg321` package from the Livna.org site.

### Using MIDI audio players

MIDI stands for Musical Instrument Digital Interface. MIDI files are created from synthesizers and other electronic music devices. MIDI files tend to be smaller than other kinds of audio files because, instead of storing the complete sounds, they contain the notes played. The MIDI player reproduces the notes to sound like a huge variety of MIDI instruments.

There are lots of sites on the Internet for downloading MIDI files. Try the fini MIDI Music site (www.ifinimidi.com), which contains songs by the Beatles, Led Zeppelin, Nirvana, and others organized by album. Most of the MIDI music is pretty simple, but you can have some fun playing with it.

Fedora and RHEL come with the kmid MIDI player. Kmid is not installed by default (find it in the kdemultimedia package on the DVD). Kmid provides a GUI interface for midi music, including the ability to display karaoke lyrics in real time. There is also the timidity MIDI Player (from the timidity++ package on the DVD), which lets you run MIDI audio from a Terminal window.

> **NOTE:** Use the timidity MIDI player if your sound card doesn't include MIDI support (install the timidity++ package). It can convert MIDI input into WAV files that can play on any sound card. To start timidity, type `timidity file.mid` at the command-line prompt.

To start kmid, type `kmid &` from a Terminal window.

### Converting audio files with SoX

If you have a sound file in one format, but you want it to be in another format, Linux offers some conversion tools you can use to convert the file. The sox utility can translate to and from any of the audio formats listed in Table 8-1.

**Table 8-1: Sound Formats Supported by the sox Utility**

| File Extension or Pseudonym | Description | File Extension or Pseudonym | Description |
| :--- | :--- | :--- | :--- |
| `.8svx` | 8SVX Amiga musical instrument description format. | `.aiff` | Apple IIF/IFF and SGI AIFF files. May require a separate archiver to work with these files. |
| `.au, .snd` | Sun Microsystems AU audio files. This is a popular format. | `.avr` | Audio Visual Research format, used on the Mac. |
| `.cdr` | CD-R files used to master compact discs. | `.cvs` | Continuously variable slope delta modulation, which is used for voice mail and other speech compression. |
