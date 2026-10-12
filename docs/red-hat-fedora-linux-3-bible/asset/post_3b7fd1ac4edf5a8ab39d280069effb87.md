
### Playing Music with Rhythmbox Audio Player

-   - **2** — Quit (Stop Music, Exit, and Eject)
-   - **1** — Back 15 Seconds
-   - **0** — Exit (Continue Music and Exit)
-   - **.** — Help (Press the period key)

The cdp display also lets you enter the names of the artist, CD, and each song. Because this information is saved, you can see it each time you play the CD. Type these commands while the cdp display is showing to edit information about the CD currently playing:

-   - **a** — Edit the Artist Name and press Enter.
-   - **c** — Edit the CD Name and press Enter.
-   - **Enter** — Edit the title of the current song and press Enter again.

> **CAUTION**: If you try to edit a song name and cdp crashes, type eject to stop the CD from playing. Editing the song name seems to work better if you pause the song first.

The arrow keys are also pretty handy for controlling CDs in cdp. The up arrow is for pause/play, and the left arrow is to go back a track. The right arrow is to go forward a track, and the down arrow is to eject.

Rhythmbox provides the GNOME music player that lets you do everything, at least according to the Rhythmbox documentation. You can play music files, import music from CDs, and play Internet radio stations, all from one interface.

The first time you run Rhythmbox, the program displays a set-up wizard. You can tell Rhythmbox where you store your music files with the wizard dialog shown in Figure 8-3.

![](img/b22364e57409c2481ba806e4e6b9309c_309_0.png)

Figure 8-3: Defining where you store your music.

After you’ve gone through the setup wizard, you’ll see the main music library interface (see Figure 8-4). Rhythmbox makes it easy to organize even large collections of music files.

![](img/b22364e57409c2481ba806e4e6b9309c_310_0.png)

**Figure 8-4: Viewing a music library with Rhythmbox.**

> **NOTE.** The Red Hat or Fedora versions of Linux do not include support for playing MP3 files, due to patent issues. You can download updates for Rhythmbox at `rpm.livna.net`. You want the package `gstreamer-plugins-mp3`.

In addition to playing music files, Rhythmbox can launch Sound Juicer to rip CDs (see the section on Ripping CDs with Grip for more on ripping CD audio). Rhythmbox can also play Internet radio stations. The easiest way to do this is to find a streaming radio station (you want to look for Shoutcast PLS files, usually with a .pls extension). Save the PLS file, and then double-click on the file in the Nautilus file browser. Nautilus comes configured to launch Rhythmbox for playing audio. Figure 8-5 shows Rhythmbox with three Internet radio stations.

![](img/b22364e57409c2481ba806e4e6b9309c_311_0.png)

Figure 8-5: Rhythmbox playing Internet radio.

> **TIP:** The site www.d1.fm lists a number of free Internet radio channels.

## Playing music with XMMS Audio Player

The XMMS (X Multimedia System) Audio Player provides a graphical interface for playing music files in MP3, Ogg Vorbis, WAV, and other audio formats. XMMS has some nice extras too, which include an equalizer, a playlist editor, and the ability to add more audio plugins. If the player looks familiar to you, that’s because it is styled after the Windows winamp program.

> **NOTE:** Red Hat removed all software that does MP3 encoding or decoding due to patent concerns related to MP3 format. Although the XMMS player was designed to play MP3 files, the XMMS plug-in required to actually decode MP3 is not included with Fedora Core. To add MP3 support back into Fedora Core, you can get and install an MP3 plugin. One place to get RPM packages that support MP3 decoding is http://rpm.livna.org. They are also available from other sources, including www.xmms.org and www.gurulabs.com/downloads.html.

You can start the XMMS Audio Player by selecting Sound & Video → Audio Player or by typing the xmms command from a Terminal window. Figure 8-6 consists of the XMMS Audio Player with the associated equalizer (below) and the Playlist Editor (to the right).

> NOTE: Although the default theme is one that matches the Fedora Blue Curve theme, you can change the look of the player by right-clicking on XMMS and selecting Options → Skin Browser. The theme shown in Figure 8-6 is called BrushedMetal_Xmms.

![](img/b22364e57409c2481ba806e4e6b9309c_312_0.png)

Figure 8-6: Play Ogg Vorbis and other audio files from the XMMS playlist.

As noted earlier, you can play several audio file formats. Supported audio file formats include the following:

-   MP3 (with added plugin)
-   Ogg Vorbis
-   WAV
-   AU
-   CD Audio
-   CIN Movies

You can get many more audio plugins from `xmms.org`. The XMMS Audio Player can be used in the following way:

1.  Obtain music files by either:
    -   Ripping songs from a CD or copying them from the Web so that they are in an accessible directory.
    -   Inserting a music CD in your CD-ROM drive. (xmms expects the CD to be accessible from /dev/cdrom.)
2.  From the Applications menu, select Sound & Video → Audio Player. The X Multimedia System player appears.
3.  Click the Eject button. The Load files window appears.
4.  If you have inserted a CD, the contents of /media/cdrecorder appear in the Files pane. Select the files you want to add to your Playlist and click the Add Selected Files or the Add all Files in Directory button to add all songs from the current directory. To add audio files from your file system, browse your files and directories and click the same buttons to add the audio files you want. Select Close.
5.  Click the **Play List** button (the tiny button marked **PL**) on the console. A Playlist Editor window appears.
6.  Double-click the music file, and it starts to play.
7.  With a file selected and playing, here are a few actions you can take:
    -   **Control play** — Buttons for controlling play are what you may expect to see on a physical CD player. From left to right, the buttons let you go to a previous track, play, pause, stop, go to the next track, or eject the CD. The eject button opens a window, allowing you to load the next file.
    -   **Adjust sound** — Use the left slider bar to adjust the volume. Use the right slider bar to change the right-to-left balance.
    -   **Display time** — Click in the elapsed time area to toggle between elapsed time and time remaining.
    -   **View file information** — Click the button in the upper-left corner of the screen to see the XMS menu. Then select View File Info. You can often find out a lot of information about the file: title, artist, album, comments, and genre. For an Ogg file, you can see specific information about the file itself, such as the format, bit rate, sample rate, frames, file size, and more. You can change or add to the tag information and click Save to keep it.
8.  When you are done playing music, click the Stop button to stop the current song. Then click the X in the upper-right corner of the display to close the window.

Special features of the XMS Audio Player let you adjust high and low frequencies using a graphic equalizer and gaffer and play songs using a Playlist Editor. Click the button marked EQ next to the balance bar on the player to open the Equalizer. Click the button marked PL next to that to open the Playlist Editor.

## Using the Equalizer

The Equalizer lets you use slider bars to set different levels to different frequencies played. Bars on the left adjust lower frequencies, and those on the right adjust higher frequencies. Click the EQ button to open the Equalizer. Here are tasks you can perform with the Equalizer:

-   If you like the settings you have for a particular song, you can save them as a Preset. Set each frequency as you like it and click the Preset button. Then choose Save \rightarrow Preset. Type a name for the preset and click OK.
-   To reload a preset you created earlier, click the Preset button and select Load \rightarrow Preset. Select the preset you want and click OK to change the settings.
