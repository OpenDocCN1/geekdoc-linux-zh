Next, you can use the Pause/Resume, Stop, Play, Fast motion, Slow motion, or Eject buttons to work with video. You can also use the Previous and Next buttons to step to different tracks. The controls are very similar to what you would expect on a physical CD or DVD player.

To select individual files, or to put together your own list of content to play, you can use the Playlist feature.

# Creating playlists with Xine

Click the Playlist button on the left side of the xine control window. A Playlist Editor appears, showing the files on your current playlist. You can add and delete content from this list, and then save the list to call on later. Here’s how you use the Xine Playlist Editor:

+   - **CDA, DVD, or VCD** — Click any of the buttons that represent a particular CD or DVD. All content from that CD or DVD is added to the playlist.
+   - **Add** — Click the Add button to see the MRL Browser window. From that window, click File to choose a file from your Linux file system to add to the list. Click Select to add that file to the Playlist Editor.
+   - **Move up/Move down** — Use the Move up selected MRL and Move down selected MRL buttons to move up and down the playlist.
+   - **Delete** — Click the Delete Selected MRL button to remove the current selection.
+   - **Delete all** — Click the Delete All Entries button to clear the whole playlist.
+   - **Save** — Click the Save button to save the playlist to your home directory (\$HOME/\ .xine/playlist .t ox or give it another name).
+   - **Load** — To read in the playlist you saved, click the Load button.

The Xine content is identified as media resource locators (MRLs). Each MRL is identified as a file, DVD, or VCD. Files are in the regular file path (//path/ file or preceded by file:/, fifo:/, or stdin://. DVDs and VCD are preceded by dvd and vcd, respectively (for example, vcd://01).

To play your playlist, click the Play button (arrow key) on the Playlist Editor.

# Xine tips

Getting video and audio to work properly can sometimes be a tricky business. Here are a few quick tips to using Xine:

+   - **Xine won’t start.** To work best, Xine needs an X driver that supports xvid. If there is no xvid support for your video card in X, Xine will shut down immediately when it tries to open the default Xv driver. If this happens to you, try starting the xine command with the X11 video driver (which is slower, but should work) as follows:

```
xine -V XShm
```