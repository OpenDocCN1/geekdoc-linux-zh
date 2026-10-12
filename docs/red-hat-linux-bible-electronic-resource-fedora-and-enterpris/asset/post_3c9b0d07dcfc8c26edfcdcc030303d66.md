
debugging level, among other things. The information about options for your Webcam driver can be useful later if you want to tune the behavior of your Webcam or track down a problem.

## Running GnomeMeeting

To start GnomeMeeting from a Terminal window, type **gnomemeeting&**. If it is not installed, you can install the gnomemeeting package from the second Red Hat installation CD (CD #2). The first time you run GnomeMeeting, the GnomeMeeting Configuration Assistant starts. The assistant lets you enter the following information:

- **Personal Data** — Your first name, last name, e-mail address, comment, and location. You can also select whether or not you want to be listed in the GnomeMeeting ILS directory.

- **Connection Type** — Indicate the speed of your Internet connection (56K modem, ISDN, DSL/Cable, 10/100 LAN or Custom).

Figure 8-6 shows the GnomeMeeting window with the history log to the right and the address book behind.

In the GnomeMeeting window that opens you can click on the book icon to open a search window (shown to the upper right in Figure 8-6). The search window enables you to connect to an ILS directory. By typing a name into the search filter, you can search for people who might be connected to that server by first name, last name, e-mail address, or location. Select a person from the list that appears and, if he or she accepts your call, you can begin video-conferencing.

Tabs beneath the video window let you adjust your audio levels and video appearance. The History tab shows a log of your activities.

![](img/27a85d56d393921ced6412ae6e8336bf_307_0.png)

**Figure 8-6:** Connect to ILS servers to video-conference with GnomeMeeting.

## Playing Video

Although several fairly high-quality video players are available for Linux, none are included in the Red Hat Linux distribution. Legal issues surrounding the playing of encoded DVD movies in Linux might be responsible for keeping players such as the Mplayer (freshmeat.net/mplayer), Ogle (http://www.dtek.chalmers.se/groups/dvd), and Xine (xine.sourceforge.net) video players out of this distribution.

By most accounts, however, if you don't download and use the DeCSS (software for decrypting DVD movies), you can get and use these video players to play a variety of video content for personal use. The following sections provide descriptions of video applications to use with Red Hat Linux.

> **CROSS-REFERENCE:** The mplayer video player, along with various tools for creating your own videos and TV recordings in Red Hat Linux, are available with the book *Linux Toys* by Christopher Negus and Chuck Wolber from Wiley Publishing. Those tools are described for making simple home video archive, television recorder, and streaming media projects.

### Watching Video with Xine

The xine player is an excellent application for playing a variety of video and audio formats. You can get xine from xine.sourceforge.net or by downloading RPMs from freshrpms.net.

You can start the xine player by typing `xine&` from a Terminal window. Figure 8-7 shows an example of the xine video player window and controls.

![](img/27a85d56d393921ced6412ae6e8336bf_308_0.png)

**Figure 8-7:** Play video CDs, MP3s, Quicktime, and other video formats with xine.

> **NOTE:** When you try to install xine, it will tell you if you need any additional packages. If your xine player fails to start, see the "Xine tips" section later in this chapter.

Xine supports a bunch of video and audio formats, including:

- MPEG (1, 2, and 4)
- Quicktime (see "Xine tips" if your Quicktime content won't play)
- Motion JPEG
- MPEG audio (MP3)
- AC3 and Dolby Digital audio
- DTS audio
- Ogg Vorbis audio

Xine can understand different file formats that represent a combination of audio and video. These include .mpg (MPEG program streams), .ts (MPEG transport streams), .mpv (raw MPEG audio/video streams), .avi (MS AVI format), and .asf (Advanced Streaming format). While xine can play Video CDs and DVDs, it can't play encrypted DVDs or Video-on-CD hybrid format as xine is delivered (because of the legal issues mentioned earlier related to decrypting DVDs).

### Using xine

With xine started, right-click in the xine window to see the controls. The quickest way to play video is to click one of the following buttons, then press the Play button (right arrow or play, depending on the skin you are using):

- VCD (looks for a video CD)
- DVD (looks for a DVD in /dev/dvd)
- CDA (looks for a music CD in /dev/cdaudio)

Next, you can use the Pause/resume, Stop, Play, Fast motion, Slow motion, or Eject buttons to work with video. You can also use the Previous and Next buttons to step to different tracks. The controls are very similar to what you would expect on a physical CD or DVD player.

To select individual files, or to put together your own list of content to play, you can use the Playlist feature.

### Creating playlists with xine

Click the Playlist button on the left side of the xine control window. A Playlist Editor appears, showing the files on your current playlist. You can add and delete content from this list, then save the list to call on later. Here's how you use the xine Playlist Editor:

- CDA, DVD, or VCD — Click any of the buttons that represent a particular CD or DVD. All content from that CD or DVD is added to the playlist.

- **Add** — Click the Add button to see the MRL Browser window. From that window, click File to choose a file from your Linux file system to add to the list. Click Select to add that file to the Playlist Editor.

- **Move up/Move down** — Use the Move up selected MRL and Move down selected MRL buttons to move up and down the playlist.

- **Delete** — Click the Delete Selected MRL button to remove the current selection.

- **Delete all** — Click the Delete All Entries button to clear the whole playlist.

- **Save** — Click the Save button to save the playlist to your home directory (`$HOME/.xine/playlist`).

- **Load** — To read in the playlist you saved, click the Load button.

The xine content is identified as media resource locators (MRLs). Each MRL is identified as a file, DVD, or VCD. Files are in the regular file path (`/path/file`) or preceded by a file:/, fifo:/, or stdin:/. DVDs and VCD are preceded by dvd and vcd, respectively (for example, `vcd://01`).

To play your playlist, click the Play button (arrow key) on the Playlist Editor.

### Xine tips

Getting video and audio to work properly can sometimes be a tricky business. Here are a few quick tips if you are having trouble getting xine to work properly (or at all):

- **Xine won't start** — To work best, xine needs an X driver that supports OpenGL. If there is no OpenGL support for your video card in X, xine will shut down immediately when it tries to open the default Xv driver. If this happens to you, try starting xine with the X11 video driver (which is slower, but should work) as follows:

```
$ xine -vXSHM
```

- **Xine playback is choppy** — If playback of files from your hard disk is choppy, there are a couple of settings you can check: 32-bit IO and DMA. (If these two features are supported by your hard disk, they will generally improve hard disk performance.)

> **CAUTION:** Improper disk settings can result in destroyed data on your hard disk. Do this procedure at your own risk. This procedure is only for IDE hard drives (NO SCSI)! Also, be sure to have a current backup and no activity on your hard disk if you change DMA or IO settings as described below.

First, test the speed of hard disk reads. To test the first IDE drive (`/dev/hda`), type:

```
# hdparm -t /dev/hda
Timing buffered disk reads: 64 MB in 19.31 seconds = 3.31 MB/sec
```

To see your current DMA and IO settings, as root user type:

```
# hdparm -c -d /dev/hda
/dev/hda:
  I/O support  = 0 (default 16-bit)
  using_dma  = 0 (off)
```

This shows that both 32-bit IO and DMA are off. To turn them on, type:

```
# hdparm -c 1 -d 1 /dev/hda
/dev/hda:
  I/O support  = 1 (32-bit)
  using_dma  = 1 (on)
```

With both settings on, test the disk again:

```
# hdparm -t /dev/hda
Timing buffered disk reads: 64 MB in 2.2 seconds = 28.83 MB/sec
```

As you can see from this example, buffered disk reads of 64 MB went from 19.31 seconds to 2.2 seconds after changing the parameters described. Playback should be much better now.

- **Xine won't play particular media** — Messages such as "no input plug-in" mean that either the file format you are trying to play is not supported or it requires an additional plug-in (as is the case with playing DVDs). If the message is "maybe x.yx is a broken file," the file may be a proprietary version of an otherwise supported format. For example, I had a Quicktime video fail that required an SVQ3 codec (which is currently not supported under Linux), though other Quicktime files will play fine.

> **NOTE:** The CrossOver Plugin (described in Chapter 9) can be used to play a variety of content, including the version of Quicktime just mentioned.

### Using RealPlayer

A tremendous amount of content is available on the Internet in the RealMedia and RealAudio formats. You can see and hear video clips of popular musicians and comics. You can view live events, such as conferences, news stories, and concerts. You can also listen to your favorite radio stations when you are out of town.

To play RealMedia and RealAudio content you need, as you may have guessed, the RealPlayer. Real Networks (www.real.com) is a leader in streaming media on the Internet. More than 50 million unique users have registered with Real Networks and their Web site, downloading more than 175,000 files per day. And that’s not even the good news. The good news is that a RealPlayer is available to run in Red Hat Linux.

The RealPlayer for Linux is available via the Linux area of download.com or tucoms.com. Or, try this site: http://proforma.real.com/real/player/unix/unix.html. This player is not supported by Real Networks directly.
