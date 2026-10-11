
![](img/577d3bff979ee86b07f9836e0df274ce_292_0.png)

Click that button to see a list of video formats you can download the video as (you can even download just the audio track if available). Click the format you desire, and the download begins. You can see the status of the download from the Firefox download status icon in the toolbar.

## Viewing Movie Files

With the popularity of digital video recorders, it's not uncommon to receive a video clip of your niece's ballet recital in an email, or from a file-sharing site (just be careful that the file-sharing site is legal). These files are often stored in a variety of video formats:

- **AVI:** Audio Visual Interleave format, a standard video format supported by most video software packages.
- **DivX:** A proprietary AVI video compression format that must be licensed to work in Linux.
- **MPG:** Moving Pictures Experts Group (mpeg) standard format. This includes both MPEG and MPG formats.
- **WMV:** Windows Media Video format, a proprietary Microsoft format.
- **RM:** The RealNetworks proprietary video format. This requires the RealOne video player.
- **MOV (and QT):** The proprietary Apple QuickTime video formats.

To watch these movies you need a video player application. A few different video players are available in Linux. Which player your Linux distribution uses by default depends mostly on your desktop, although there are some great video players that have versions for all desktops. This section walks through the most popular Linux video players.

## GNOME Videos

The default video file player in the GNOME 3 desktop environment is Videos. In Ubuntu you can start Videos either by double-clicking a saved video file, or start it from the application launcher by selecting its icon or typing its name in the Search text box.

As with the Firefox video plugins, due to licensing restrictions, the default Videos installation may be somewhat limited in the types of files it can play. If you selected the option to install third-party software during installation, Videos can play the popular MPEG4 video file type.

When you start a video, or just open the Videos window, the main viewing window appears, as shown in Figure 14-4.

![](img/577d3bff979ee86b07f9836e0df274ce_293_0.png)

If you just open **Videos** without specifying a video file, the **Videos** window displays a playlist showing icons of recently played videos. You add new videos to the playlist by clicking the **+** icon in the toolbar, which provides two options for loading movies into the **Videos** viewer:

- **Add Local Video**: Opens a file browser for you to find video files on your system to add to the playlist.
- **Add Web Video**: Displays a text box for you to enter the URL of a video found on the Internet.

You can change some of the settings used by **Videos** by clicking the **Menu** icon in the toolbar and selecting **Preferences**. There are three preference tabs:

- **General**: Enable using subtitles from external files, select the font to use for subtitles, and a button to enable/disable plugins.
- **Display**: Set the overall color features, such as brightness, contrast, saturation, and hue.
- **Audio**: Set the audio features, such as mono or stereo.

After you start a video, click the **Menu** button in the toolbar to view a list of options you can set as the video plays, such as setting the aspect ratio to view the video, and enabling or disabling subtitles for the video.

## KDE Dragon

The flagship video player application for the KDE Plasma desktop is **Dragon**. If your distribution didn’t install it by default, you can easily find it in the software repositories (see Chapter 15).

You can start **Dragon** from the **Applications** menu by choosing **Applications** :: Multi-media :: **Dragon**. Figure 14–5 shows the main **Dragon** window.

The left-hand navigation bar allows you to start videos from three types of sources:

- **Files**: Opens a file manager to navigate to the video file to play.
- **DVDs**: Attempts to detect the removable DVD location to play the DVD.
- **Streams**: Prompts for a URL to find the video to play from the Internet.

![](img/577d3bff979ee86b07f9836e0df274ce_295_0.png)

FIGURE 14-5: The KDE Dragon video player.

The playback toolbar in Dragon is located at the top, above the viewing area. Nothing too surprising here; just standard controls for playing or pausing your video. However, you can change what controls display in the playback toolbar by choosing Settings:: Configure Toolbars. Just select which controls appear!

## VLC

Chapter 13 discusses how to use the VLC multimedia player for playing audio files, but VLC also works great as a video player! The VLC project has created versions that work in just about every Linux graphical desktop environment, so it’s common to see it used across many Linux distributions (and it’s even the default video player in openSUSE).

The main VLC window, shown in Figure 14-6, isn’t all that exciting.

The Media menu option allows you to select a video file from several locations:

- Open a single file.
- Open multiple files simultaneously.
- Open all the files contained in a specified directory.
- Play a DVD disc.
- Open a network stream using a URL.
- Directly capture video from a connected device (such as a camcorder).

![](img/577d3bff979ee86b07f9836e0df274ce_296_0.png)

FIGURE 14-6: The main VLC viewing window.

After you've opened a video file, the controls at the bottom of the VLC window provide the standard controls for playing the video.

## Watchin' DVDs

Watching a DVD in Linux is a bit of a legal quagmire if you live in the United States. The Digital Millennium Copyright Act (DMCA) and other issues make it tricky for any open source program to navigate the licensing maze when it comes to movies that are encoded or protected in various fashions. However, not all DVDs have such countermeasures enabled: There are DVDs that Americans can watch under Linux with no trouble. (Note that I say *watch*, and not *copy* or *pirate*.)

![](img/577d3bff979ee86b07f9836e0df274ce_296_1.png)

DVDs created by video burning software such as K3b or Brasero don't include copy-right protection, and thus can be played just fine using the standard Linux video players mentioned here.

How you watch videos depends on your distribution:

- Ubuntu uses Videos. However, just like when viewing video files, you need to ensure the third-party software extensions are installed to be able to play commercial DVDs.
- KDE uses the Dragon video player. It provides a button to launch a video from a DVD, but it too requires third-party software extensions to be installed to play commercial DVDs.
- openSUSE uses the VLC multimedia player. After you insert a DVD, the Device Notifier prompts you to select what software to use to play the DVD. After you select VLC, the movie starts (assuming it’s not protected, and that you have the correct codec installed).

![](img/577d3bff979ee86b07f9836e0df274ce_297_0.png)

You may be tempted to use a Linux DVD burning software package such as Brasero or K3b to copy a commercial DVD — don’t. It’s illegal to copy a commercial DVD that includes copyright protection, even just for your own use.

# Creating and Modifying Graphics

The *GIMP* software package is a graphics program that’s considered in many ways equivalent to Adobe Photoshop. Many don’t consider GIMP the friendliest program on the planet, but at the very least, it has enough features to keep you busy experimenting for weeks! Because of its size and specialty use, most Linux distributions don’t install GIMP by default. You need to use one of the methods outlined in Chapter 15 to install GIMP in your Linux distribution.

After you start GIMP, a collection of one or more windows pops up containing the GIMP main window (see Figure 14-7) plus two additional tool windows. You can close the right-side window that contains the Paintbrush selector and Layers sections. The Toolbox window on the left-hand side and the main window are somewhat incorporated together.

![](img/577d3bff979ee86b07f9836e0df274ce_297_1.png)

> FIGURE 14-7: GIMP’s main window in Ubuntu.
