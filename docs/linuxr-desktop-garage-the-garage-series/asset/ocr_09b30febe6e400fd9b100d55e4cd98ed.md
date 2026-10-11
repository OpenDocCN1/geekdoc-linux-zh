# An Ode to iTunes

I used to be normal and listened to my music without thinking about how it was arranged or where I got it. Then I used iTunes. My digital music world changed. I cared about my ID3 tags. I wanted Smart Playlists and easy online purchase of songs, albums, and audio books. I was forever spoiled for normal MP3 listening. Rhythmbox makes up for my loss in many features, but it is like giving methadone to a heroin addict. The pool of needy, potential iTunes users in Linux isn't large enough yet to convince Apple to make a Linux version. There is hope, though. I read that someone got iTunes for Windows to work in Crossover Office (more on that program in Topic 13, “Running Windows Applications”). I won’t stop begging Apple for a Linux version of iTunes, but I will try this hopeful alternative.

XMMS arranges its windows and menus differently than other programs. You can access XMMS menus by right-clicking almost anywhere in any of the windows, just not in the list part of the Playlist window. Most of the menu options are for doing playback control and toggling the three window options in and out of view. In the Options menu, you can adjust many settings and change which skin XMMS displays. The Visualization menu has options for showing visualizer displays. Visualizations are digital light shows that often move with the beat of the music you play. There are a few built-in patterns and more available to download online.

# Add Mp3 Support to XMMS in Fedora

Read the beginning of ToolKit 11.2 to find out why you even need to mess with this. Fortunately, adding MP3 support to XMMS is cake.

+   1. You simply need to install the package named xmms-mp3. You should be able to do that from FreshRpm’s.net’s repository using Apt or Yum. You can also get the package from Guru Labs (see [http://www.gurulabs.com/downloads.html](http://www.gurulabs.com/downloads.html)).
+   2. Update Apt like normal:
+   3. Install the xmms-mp3 package that XMMS needs for MP3 support:
+   4. Open XMMS, and you should be ready to go.

```
# apt-get update
```

```
#apt-get-install xmms-mp3
```