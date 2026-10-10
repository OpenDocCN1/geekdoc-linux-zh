
Preferences to select to have columns of that information appear on your Rhythmbox window.

- **Play music tracks** — With your music available, you can play it by double-clicking an album (to play the whole album), artist (to play the artist's first album you have), or track (to start with that track). Buttons at the top of Rhythmbox let you play/pause or go forward or backward a track. Select Shuffle or Repeat boxes on the bottom of Rhythmbox to randomly play the songs in the album or play the same album repeatedly. Use the slider to move ahead or back in a song and select the speaker icon to adjust volume.

- **Play Internet radio** — Rhythmbox can also play Internet radio stations. The easiest way to do this is to find a streaming radio station (you want to look for Shoutcast PLS files, usually with a `.pls` extension). Save the PLS file, right-click the file in the Nautilus file browser, and then select Open with Music Player. Nautilus comes configured to launch Rhythmbox for playing audio. The sites `http://www.di.fm` and `http://www.shoutcast.com` list a number of free Internet radio channels.

If you are looking for new music, selections under Stores on the Rhythmbox window let you connect to Magnatune and Jamendo online music services. Select either of those services to see lists of music you can try out for free. You can also search those services for music that interests you.

Magnatune makes money by licensing the music of the artists it represents for use in movies, Web sites, commercials, or other media. You can also purchase a whole album or physical music CD through those services. Jamendo provides the music of its artists for free, to help promote the music to a world-wide audience. In either case, those services provide a way for you to explore different kinds of music.

## Playing music with XMMS Audio Player

The XMMS (X Multimedia System) Audio Player provides a graphical interface for playing music files in MP3, Ogg Vorbis, WAV, and other audio formats. XMMS has some nice extras, too, which include an equalizer, a Playlist Editor, and the ability to add more audio plug-ins. If the player looks familiar to you, that's because it is styled after the Windows winamp program.

**NOTE:** Because XMMS is not a GStreamer application, the MP3 support you can get from Fluendo doesn't work with XMMS. You can get MP3 support by installing the lame package from the rpmfusion.org repository.

The *xmms* package is available from the Fedora repository (type `yum install xmms` to install the *xmms* package). Start the XMMS Audio Player from the Applications menu by selecting Sound & Video → Audio Player or by typing the *xmms* command from a Terminal window. Figure 7-5 consists of the XMMS Audio Player with the associated equalizer (above) and the Playlist Editor (to the right).

**Part II: Using Fedora**

**NOTE:** Although the default theme is one that matches the Fedora blue color scheme, you can download different themes from `http://www.xmms.org/skins.php`. Copy the skin's zip file to the `/usr/share/doc/xmms/Skins` directory. Then change the look of the player by right-clicking on XMMS and selecting Options → Skin Browser. The theme shown in Figure 7-5 is called UltrafrinaSE.

![Figure 7-5: XMMS Audio Player](img/c78bdcb5b7842a0d73dcc98921f872a2_291_0.png)

As noted earlier, you can play several audio file formats. Supported audio file formats include the following:

- MP3 (with added xmms-mp3 package)
- Ogg Vorbis
- FLAC (with added xmms-flac package)
- WAV
- AU
- CD Audio
- CIN Movies

You can get many more audio plug-ins from the Fedora repository or directly from `http://www.xmms.org`. The XMMS Audio Player can be used in the following way to play music files:

1. Obtain music files by either:
   - Ripping songs from a CD or copying them from the Web so that they are in an accessible directory.
   - Inserting a music CD in your CD-ROM drive. (xmms expects the CD to be accessible from `/dev/cdrom`.)
2. From the Applications menu, select **Sound & Video → Audio Player**. The X Multimedia System player appears.
3. Click the **Eject** button. The **Load files** window appears.
4. If you have inserted a CD, the content of that CD appears in the **Files** pane. (If it doesn’t, change to `/dev/cdrom`, `/media/cdrom`, or `/media/cdrecorder`, as appropriate.)
   - Select the files you want to add to your **Playlist** and click the **Add Selected Files** or the **Add All Files in Directory** button to add all songs from the current directory. To add audio files from your file system, browse your files and directories and click the same buttons to add the audio files you want. Select **Close**.
5. Click the **Play List** button (the tiny button marked **PL**) on the console. A **Playlist Editor** window appears.
6. Double-click the music file and it starts to play.
7. With a file selected and playing, here are a few actions you can take:
   - **Control play** — Buttons for controlling play are what you would expect to see on a physical CD player. From left to right, the buttons let you go to a previous track, play, pause, stop, go to the next track, or eject the CD. The **Eject** button opens a window, allowing you to load the next file.
   - **Adjust sound** — Use the left slider bar to adjust the volume. Use the right slider bar to change the right-to-left balance.
   - **Display time** — Click in the elapsed time area to toggle between elapsed time and time remaining.
   - **View file information** — Click the button in the upper-left corner of the screen to see the **XMMS** menu. Then select **View File Info**. You can often find out a lot of information about the file: title, artist, album, comments, and genre. For an **Ogg** file, you can see specific information about the file itself, such as the format, bit rate, sample rate, frames, file size, and more. You can change or add to the tag information and click **Save** to keep it.
8. When you are done playing music, click the **Stop** button to stop the current song. Then click the **X** in the upper-right corner of the display to close the window.

Special features of the XMMS Audio Player let you adjust high and low frequencies using a graphic equalizer and gather and play songs using a Playlist Editor. Click the button marked **EQ** next to the balance bar on the player to open the Equalizer. Click the button marked **PL** next to that to open the Playlist Editor.

### Using the Equalizer

The Equalizer lets you use slider bars to set different levels to different frequencies played. Bars on the left adjust lower frequencies, and those on the right adjust higher frequencies. Click the **EQ** button to open the Equalizer. Here are tasks you can perform with the Equalizer:

- If you like the settings you have for a particular song, you can save them as a Preset. Set each frequency as you like it and click the Preset button. Then choose Save → Preset. Type a name for the preset and click OK.
- To reload a preset you created earlier, click the Preset button and select Load → Preset. Select the preset you want and click OK to change the settings.

The small window in the center/top of the Equalizer shows the sound wave formed by your settings. You can adjust the Preamp bar on the left to boost different levels in the set range.

### Using the Playlist Editor

The Playlist Editor lets you put together a list of audio files that you want to play. You can add and delete files from this list, save them to a file, and use them again later. Click the PL button in the XMMS window to open the Playlist Editor.

The Playlist Editor allows you to:

- **Add files to the playlist** — Click the Add button. The Load Files window appears. Select the directory containing your audio files (it's useful to keep them all in one place) from the left column. Then either select a file from the right column and click Add selected files or click Add all files in the directory. Click OK. The selected file or files appear in the playlist. You can also drag music files from the Nautilus file manager onto the playlist window to add the files to the playlist.
- **Select files to play** — To select from the files in the playlist, use the previous track and next track buttons in the main XMMS window. The selected file is highlighted. Click the Play button to play that file. Alternatively, you can double-click on any file in the playlist to start it playing.
- **Delete files from the playlist** — To remove files from the playlist, select the file or files you want to remove (next/previous track buttons), right-click the playlist window, and click Remove → Selected. The selected files are removed.
- **Sort files on the playlist** — To sort the playlist in different ways, click and hold the Misc button and move the mouse to select Sort List. Then you can select Sort List to sort by Title, Filename, Path and Filename, or Date. You can also randomize or reverse the list.
- **Save the playlist** — To save the current playlist, hold the mouse button down on the List button and then select Save. Browse to the directory you want, and then type the name you want to assign to the playlist and click OK.
- **Load the playlist** — To reload a saved playlist, click the List button. Select a previously saved playlist from the directory in which you saved it and click OK.
