
in Ubuntu because of licensing concerns. Even if you plan on using the Ogg Vorbis format in your future ripping and encoding endeavors, installing MP3 support is a good idea so as to cover all your audio bases. It’s also a very easy process.

The easiest way to install MP3 playback support is to double-click an MP3 file that you have on your hard disk. A window will appear, asking whether you want to search for the plug-ins necessary to play the file. Click Search, after which another window will appear, showing you what you need to install (Figure 14-1). Check both boxes in that window, click the Install button, and in the confirmation window that then appears, click Confirm. You will then be asked for your password, so provide it, and then just wait until the process is complete. Once done, you’ll be able to play not only your MP3 audio files but also MPEG and WMV videos.

![](img/f7cef0df22f9dba5a41777808c98eece_300_0.png)

Figure 14-1: Ubuntu helps you find the plug-ins you need.

If you prefer, you can download and install these plug-ins quite easily via the Ubuntu Software Center by doing a search for gstreamer and then installing gstreamer0.10-ffmpeg (GStreamer ffmpeg video plugin), gstreamer0.10-fluendo-mp3 (Fluendo mp3 decoder GStreamer plugin), and gstreamer0.10-plugins-ugly (GStreamer extra plugins).

As for MP3 encoding support, which enables you to rip CDs and create your own space-saving MP3 files, well, things aren’t so automatic. But it’s not much of a chore, either, because all you need to do is use the Ubuntu Software Center to search for and install gstreamer0.10-plugins-ugly-multiverse. If you also want to give yourself AAC encoding ability, you should install gstreamer0.10-plugins-bad-multiverse as well. You will then be ready for action, as described in the next section.

## Rhythmbox—Your Audio Player

The main audio player in Ubuntu is called Rhythmbox (see Figure 14-2), which seems to function pretty much like a simplified version of Apple’s iTunes application. It’s a relatively easy-to-use audio player that, despite some quirks in its early stages, has developed quite a following in the Linux world. To run Rhythmbox, just go to the Applications menu and select Sound & Video ▸ Rhythmbox Music Player.

![](img/f7cef0df22f9dba5a41777808c98eece_301_0.png)

Figure 14-2: The Rhythmbox audio player

## Adding Songs and Albums to the Rhythmbox Library

If you are familiar with Apple’s iTunes, then you should understand the Library in Rhythmbox too, because it is essentially the same concept. Rhythmbox should automatically import everything you have in your Music folder without any extra work on your part. If you prefer to add songs to the Rhythmbox library manually, you can open the preferences window (Edit ▸ Preferences), click the Music tab, and then uncheck the Watch my library for new files box. After that, you can add new albums to your Rhythmbox Library by going to the Music menu, selecting Import Folder, and then navigating to the folder for the new album you want to add. If you want to add a number of albums by the same artist, just navigate to and select the folder for that artist instead. If you want to add just a single audio file, you can also do that—select Music ▸ Import File, and then navigate to the song in question.

If you are not using the navigating type, you can also add files and folders by other means. The simplest way is to drag the folder or song you want to add to the Library into the right pane of the Rhythmbox window. You can also

add a song to the Library directly by right-clicking the file and selecting **Open with ▸ Open with Rhythmbox** in the pop-up menu that appears.

## Ripping Audio CDs with Rhythmbox

Like iTunes, Rhythmbox also allows you to rip songs directly from a CD; convert them to Ogg Vorbis, MP3, or other audio formats; and then add the ripped tracks to its music library. The steps are as follows:

- 1. Open the Preferences window (**Edit ▸ Preferences**), click the **Music** tab, and select the encoding format you want to use (**Ogg Vorbis** is the default). Once you’re done, click **Close**. Unless you change encoding formats often, you won’t have to do this more than once.
- 2. Select your audio CD in the left pane of the Rhythmbox window.
- 3. Click the **Copy to library** button in the upper-right part of the Rhythmbox window. The ripping and encoding process will then begin, and the progress will show in the bottom-right corner of the Rhythmbox window. Once done, the ripped songs will automatically appear in the Rhythmbox Library.

> **NOTE** *If you have not installed the gstreamer0.10-plugins-ugly-multiverse package, the MP3 option will not appear in the Output Format menu.*

## Browsing the Rhythmbox Library

The Rhythmbox Library, which you can make visible by clicking **Music** in the left pane of the Rhythmbox window, is a collection of all the music you add to it. This can prove to be a bit unwieldy as your collection grows. Fortunately, Rhythmbox has a nice browser function, like the one in iTunes, that can be toggled on and off by clicking the **Browse** button shown in Figure 14-3. This function allows you to see lists of the artists and albums in two separate panes above the main Library list. If you click a specific artist in the Artist pane, a list of albums by that artist will appear in the right pane. You can then double-click one of the albums in that right pane to play it. If you want to play all the albums you have by that artist, just double-click the artist’s name in the left pane. All in all, it’s a very handy feature.

![](img/f7cef0df22f9dba5a41777808c98eece_302_0.png)

Figure 14-3: The Browse button in Rhythmbox

If you want to add a layer of categorization to the browser, you can do so by adding a Genre pane. To do this, just go to the **Edit** menu, select **Preferences**, select the **General** tab of the window that appears, and then select **Genres, artists, and albums**. After clicking the **Close** button in the Preferences window, you will have a three-pane browser in Rhythmbox (Figure 14-4).
