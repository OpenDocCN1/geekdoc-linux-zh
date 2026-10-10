
## Part II: Using Fedora

If you have a video file on your hard disk and you’d like to know what type of content it contains, you can use the `file` command. Here’s an example of the `file` command for checking the contents of a movie trailer:

```
$ file movie.avi
movie.avi: RIFF (little-endian) data, AVI, 640 x 272, 23.98 fps, video: DivX 3, audio: MPEG-1 Layer 3 (stereo, 44100 Hz)
```

This example shows that the file contains DivX 3 video and MPEG-1 Layer 3 audio. The size of the video is 640 x 272 pixels. Video was captured at 23.98 frames per second. This can lead you to the type of video player you need to install. Given that the right codecs are installed, MPlayer, Xine, VLC, or several other players would be able to play this content.

### Watching video with Xine

At the base of the Xine video player (www.xine-project.org) is the xine-lib core engine. While Xine has its own xlib-based user interface, you can choose different video player front-ends to use with the core engine instead (including Totem, Kaffeine, and axine). You can also use Xine as a Mozilla plug-in, to have videos play in a browser window.

The xine player is an excellent application for playing a variety of video and audio formats. You can get Xine from www.xine-project.org/releases (which takes some work to get going). The basic Xine player is available in Fedora (xine-ui package). However, to get most of the codecs you need to make Xine useful, you need to download RPMs from http://rpmfusion.org. (See Chapter 5 for information on using rpmfusion.org and other software repositories for getting Fedora software. If yum is configured to point to one of those repositories, you should be able to install Xine by typing `yum install xine*`).

> **NOTE:** The Xine project offers the following disclaimer before you download or use its software:
> *Some parts of Xine (especially audio/video codecs) may be subject to patent royalties in some countries. If you provide pre-compiled binaries or intend to build derivable works based on the Xine source please consider this issue. The Xine project is not warranting or indemnifying you in any way for patent royalties. You are solely responsible for your own actions.*

You can start the Xine player by typing `xine&` from a Terminal window. Figure 7-12 shows an example of the Xine video player window and controls.

The Xine Setup window (shown to the right) lets you choose various settings for the video player, such as a different user interface, if one is available. Below the Xine window is the Xine controller, which has buttons that work like many physical DVD players. Right-click the main window to see a menu of options. Select Settings → Video to display another controller (shown at the bottom of Figure 7-12) that lets you adjust hue, saturation, brightness, and contrast.

![](img/c78bdcb5b7842a0d73dcc98921f872a2_318_0.png)

![](img/c78bdcb5b7842a0d73dcc98921f872a2_318_1.png)

![](img/c78bdcb5b7842a0d73dcc98921f872a2_318_2.png)

Figure 7-12: Play video CDs, MP3s, QuickTime, and other video formats with Xine.

Xine supports a bunch of video and audio file formats and codecs. However, not all of these codecs are distributed with Xine:

- MPEG (1, 2, and 4)
- QuickTime (see the section “Xine tips” later in this chapter if this content won't play)
- RealMedia (see the section “Xine tips” later in this chapter if this content won't play)
- WMV (see the section “Xine tips” later in this chapter if this content won't play)
- Motion JPEG
- MPEG audio (MP3)
- AC3 and Dolby Digital audio
- DTS audio
- Ogg Vorbis audio

Using the Xine controller, you can select to play content directly from a DVD, DVB, VCD, VCD0, or CD disk. If you are playing an audio CD (or any audio file), you can choose different visualizations (right-click, and then choose Audio → Visualization and select goom, oscope, fftscope, or fftgraph) to appear in the Xine windows as music plays.

Xine can understand different file formats that represent streaming audio and video. These include .mpg (MPEG program streams), .ts (MPEG transport streams), .mpv (raw MPEG audio/video streams), .avi (MS AVI format), and .asf (Advanced Streaming format). While Xine can play video CDs and DVDs containing other content, it can't play encrypted DVDs or video-on-CD hybrid format without adding other software (because of the legal issues mentioned earlier related to decrypting DVDs).

### Using Xine

With Xine started, right-click in the Xine window to see the controls. The quickest way to play video is to click one of the following buttons, and then press the Play button (right arrow or Play, depending on the skin you are using):

- VCD (looks for a video CD)
- DVD (looks for a DVD in `/dev/dvd`)
- CDA (looks for a music CD in `/dev/cdaudio`)
- DVB (looks for a DVB device supported by linuxtv drivers)

Next, you can use the Pause/Resume, Stop, Play, Fast motion, Slow motion, or Eject buttons to work with video. You can also use the Previous and Next buttons to step to different tracks. The controls are very similar to what you would expect on a physical CD or DVD player.

To select individual files, or to put together your own list of content to play, you can use the Playlist feature.

### Creating playlists with Xine

Click the Playlist button on the left side of the Xine control window. A Playlist Editor appears, showing the files on your current playing. You can add and delete content from this list, and then save the list to call on later. The following options are available in the Xine Playlist Editor:

- **CDA, DVD, or VCD** — Click any of the buttons that represent a particular CD or DVD. All content from that CD or DVD is added to the playlist.
- **Add** — Click the Add button to see the MRL Browser window. From that window, click File to choose a file from your Linux file system to add to the list. Click Select to add that file to the Playlist Editor.
- **Move up/Move down** — Use the Move up selected MRL and Move down selected MRL buttons to move up and down the playlist.
- **Delete** — Click the Delete Selected MRL button to remove the current selection.
- **Delete all** — Click the Delete All Entries button to clear the whole playlist.
- **Save** — Click the Save button to save the playlist to your home directory (`$HOME/.xine/playlist.txt`) or give it another name.
- **Load** — To read in the playlist you saved, click the Load button.

The Xine content is identified as media resource locators (MRLs). Each MRL is identified as a file, DVD, or VCD. Files are in the regular file path (`/path/file`) or preceded by `file:/`, `fifo:`, or `stdin:`. DVDs and VCD are preceded by `dvd` and `vcd`, respectively (for example, `vcd://01`).

To play your playlist, click the **Play** button (arrow key) on the Playlist Editor.

### Xine tips

Getting video and audio to work properly can sometimes be a tricky business. Here are a few quick tips to using Xine:

- **Xine won't start.** To work best, Xine needs an X driver that supports xvrd. If there is no xvrd support for your video card in X, Xine will shut down immediately when it tries to open the default Xv driver. If this happens to you, try starting the xine command with the X11 video driver (which is slower, but should work) as follows:

  ```
  $ xine -V Xshm
  ```

- **Don't run as root.** Run xine as a regular user, instead of as root. Once Xine is installed, you should be able to run it from the *Applications* menu on your panel by selecting **Sound & Video → Xine Media Player**. There have been recently discovered vulnerabilities of some open source media players related to streaming media. Although that problem was fixed, it again highlighted the fact that running applications as a regular user, whenever possible, is a good idea.

- **Run xine-check.** To get an idea of how happy Xine is running on your system, run the xine-check command (as the user who will be using Xine). It will tell you if there are problems running Xine on your current operating system, kernel, or processor, among other things.

- **Xine playback is choppy.** If playback of files from your hard disk is choppy, there are a couple of settings you can check: 32-bit IO and DMA. (If these two features are supported by your hard disk, they will generally improve hard disk performance.)

> **CAUTION:** Improper disk settings can result in destroyed data on your hard disk. Do this procedure at your own risk. This procedure is only for IDE hard drives (not SCSI)! Also, be sure to have a current backup and no activity on your hard disk if you change DMA or IO settings as described here.

First, test the speed of hard disk reads. To test the first IDE drive (in Fedora 7 and prior versions, it may appear as /dev/sda instead of /dev/hda), type:

```
# hdparm -t /dev/sda
Timing buffered disk reads: 64 MB in 19.31 seconds = 3.31 MB/sec
```

To see your current DMA and IO settings, as root user type:

```
# hdparm -c -d /dev/sda
/dev/sda:
    I/O support = 0 (default 16-bit)
    using_dma = 0 (off)
```
