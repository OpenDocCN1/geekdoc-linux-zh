
## 11.4 Noatun: Skinning and General Usage

To play a song in Noatun, go to File > Open, find the file or directory you want to play, and then click OK. This adds the song to your playlist. If you don't have the playlist window open, click Settings > Show Playlist. There is also a toolbar icon for the playlist. Simply highlight a song and click the Play button on the toolbar or double-click the song in the playlist.

Skinning in Noatun is different than in other programs. Skins are added as plug-ins, and they can rearrange the whole program. Although the default skin is plain vanilla, you can find some very interesting skins on Noatun’s Web site at [http://noatun.kde.org](http://noatun.kde.org).

### Skin Noatun to Play Your CD in Style

Not as many skins are available for Noatun as there are for XMMS, but they do more fun stuff. Let’s add one of the K-folol set of skins.

- Open Noatun and then go to Settings > Configure Noatun.
- Go to Plug-ins. You might see a warning about your playlist stopping play, but you can click OK. You’ll see a list of interfaces, many of which you already have installed by default.
- Uncheck the default skin, Excellent, and then check K-folol.
- When you click Ok or Apply, your Noatun interface changes to use the new skin and looks something like Figure 11.6.

![](img/f2b5f4073f00f9ec5546d9acb9cc6448_288_0.png)

You can download new skins from the Noatun Web site and from KDE Look (see [http://www.kde-look.org](http://www.kde-look.org/)). You might have noticed that there was also an option for a WinAmp skin loader. This option lets you skin Noatun with any of the tons of WinAmp 2.x skins available online (see [http://winamp.com](http://winamp.com/)).

## XMMS

### Program Info

- **Menu**: Fedora/GNOME menu Sound & Video > Audio Player
- **Terminal command**: XMMS
- **Program URL**: http://www.xmms.org

This is the grandpa program of GUI digital audio players in Linux. XMMS has been around for a while but has stayed pretty popular throughout that time, just like the player that it is modeled after, WinAmp. As with many Linux programs, someone switched over from Windows, said, "I miss WinAmp," and made this version. XMMS is a solid little player that supports MP3, MOD, WAV, OGG, and others using plug-ins. There are plug-ins for some video support as well, but that function isn't very well developed for XMMS. This player is mode for music.

There are a few different window components to XMMS (see Figure 11.7). The three windows can be moved separately or together as a unit. The Main window contains the playback controls, volume control, progress slider, shuffle and repeat buttons, and playback display, which shows you information about the song you are playing. You can drag the Main window with your mouse and have the Equalizer and Playlist windows move with it. The Equalizer window has a graphic equalizer on it with several slider controls to adjust the spectrum of sound. The Playlist window lists the current playlist.

![](img/f2b5f4073f00f9ec5546d9acb9cc6448_289_0.png)
![](img/f2b5f4073f00f9ec5546d9acb9cc6448_289_1.png)

Also have written support for other portable players. The methods for how players sync with a given Linux program differ quite a bit, so do a quick search online for your particular player to find tutorials and reviews.

### An Ode to iTunes

I used to be normal and listened to my music without thinking about how it was arranged or where I got it. Then I used iTunes. My digital music world changed. I cared about my ID3 tags. I wanted Smart Playlists and easy online purchase of songs, albums, and audio books. I was forever spoiled for normal MP3 listening. Rhythmbox makes up for my loss in many features, but it is like giving methadone to a heroin addict. The pool of needy, potential iTunes users in Linux isn't large enough yet to convince Apple to make a Linux version. There is hope, though. I read that someone got iTunes for Windows to work in Crossover Office (more on that program in Topic 13, “Running Windows Applications”). I won’t stop begging Apple for a Linux version of iTunes, but I will try this hopeful alternative.

XMMS arranges its windows and menus differently than other programs. You can access XMMS menus by right-clicking almost anywhere in any of the windows, just not in the list part of the Playlist window. Most of the menu options are for doing playback control and toggling the three window options in and out of view. In the Options menu, you can adjust many settings and change which skin XMMS displays. The Visualization menu has options for showing visualizer displays. Visualizations are digital light shows that often move with the beat of the music you play. There are a few built-in patterns and more available to download online.

### Add MP3 Support to XMMS in Fedora

Read the beginning of ToolKit 11.2 to find out why you even need to mess with this. Fortunately, adding MP3 support to XMMS is cake.

- You simply need to install the package named `xmms-mp3`. You should be able to do that from FreshRpm’s.net’s repository using Apt or Yum. You can also get the package from Guru Labs (see [http://www.gurulabs.com/downloads.html](http://www.gurulabs.com/downloads.html)).
- Update Apt like normal:
  ```bash
  # apt-get update
  ```
- Install the `xmms-mp3` package that XMMS needs for MP3 support:
  ```bash
  # apt-get install xmms-mp3
  ```
- Open XMMS, and you should be ready to go.

## Watch Movies

### Xine

**Program Info**

| Terminal command | Program URL |
| :--- | :--- |
| xine | http://xine.sourceforge.net/ |

One of the most popular media players available for Linux is Xine (see Figure 11.8). Xine supports many media types, from simple MP3 files to DVDs, AVI, MPEG video, and more. Codecs are used to manage different media types, and plenty of codecs are available for Xine. Need to play a certain kind of file? Simple: Just find a codec that has been written for Xine for that media type, download it, and install the codec in Xine. In addition, many plug-ins are available for Xine to add more functionality to the program, such as new front-end modules that change the GUI for Xine's controls and codecs to play new media types. Unlike other Linux media players, Xine's GUI interface is installed by default, an added bonus for desktop users who like their mouse better than their terminal.

![](img/f2b5f4073f00f9ec5546d9acb9cc6448_291_0.png)

Totem is a front-end plug-in that runs on Xine's base (see Figure 11.9). Totem shares many attributes with Xine as a player but sports a simplified interface. The program is split between a video and an audio player. The video player seems to be the more useful half. The pared GUI in Totem might not be as shiny as Xine's interface, but the buttons and functions can be clearer and easier to find. Totem is the default player in GNOME 2.6 and is also the default player in Mandrake 10 for both KDE and Gnome. As a result, if you put in a DVD, you will likely have Totem pop up automatically and start playing it for you.

![](img/f2b5f4073f00f9ec5546d9acb9cc6448_292_0.png)

With Xine, as with other media players, there are many different ways to tweak the video and audio output to account for glitches and bugs. You can find a few of those tips online at Xine's FAQ page (see http://xinehq.de/index.php/faq). If you are simply playing small video files or regular DVDs, you most likely won't have to mess with tweaking options.

Features in Xine include the capability to play several supported file types, play DVDs with menu support, show a visualizer for use when playing audio files, and adjust TV tuner card configuration. There is also streaming playlist support, the capability to change aspect ratio and scale video, video quality controls, and screenshot capability.

### Play a Movie in Totem

If you don't have Totem installed in Fedora, you can grab it from the APT and Yum repositories on freshrpms.net.

#### The Quick Way

- Put your DVD into the drive.
- Open Totem. You can type in the command `totem`. In Mandrake, find Totem from the main menu, Multimedia > Video > Totem Movie Player. In Fedora, look in the main menu under Sound & Video.
