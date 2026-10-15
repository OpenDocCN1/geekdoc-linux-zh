
![](img/e464b828c497c99e41f61d4c55f1c0db_246_0.png)

**FIGURE 10.7** Sound Juicer at work, seen here after retrieving data from the Internet.

## What Is Mono?

If you hang around long enough in the Linux world, you will frequently come across something called Mono. Nope, this term does not relate to mono-aural sound but rather to a development framework that takes the best parts of Microsoft's .Net applications development environment and allows them to run under Linux. For more information on the mono project you should head on over to http://www.mono-project.org.

By default Gnome opens Sound Juicer when you insert an audio disc, but it is easy to change this to Banshee by using the Removable Drives & Media tool in the Preferences menu. Under the Multimedia tab, change Sound Juicer to Banshee, which will mean that whenever you insert an audio disc now, Banshee will automatically load, ready for you to import the disc to Ubuntu.

Importing itself is very easy—once Banshee has retrieved any track listing, simply click the Import CD button as seen in Figure 10.8. Banshee will start to encode the audio data into your preferred codec and will store the files in the `~/music` directory.

## Music Players

Ubuntu provides access to various music players. One of the most popular is Xmms, a Winamp clone, which in the full version can play not only music, but MPEG1/2/3 video as well. Xmms (see Figure 10.9) supports a number of plug-ins that can add dancing, lighted oscilloscope-like displays, redirect its output to other devices, support unusual file formats, sync animations to the music, and otherwise increase its geek appeal exponentially. Xmms used to be included in the base Ubuntu distribution, but has now been shifted to Extras, so you will need to use yum to install it.

![](img/e464b828c497c99e41f61d4c55f1c0db_247_0.png)

**FIGURE 10.8** Banshee is a relatively new application, and can easily handle ripping CDs to your hard drive.

![](img/e464b828c497c99e41f61d4c55f1c0db_247_1.png)

**FIGURE 10.9** The ever-popular Xmms music player, seen here playing a local MP3 file.

The default music player is Rhythmbox, which is designed to play music files from playlists and Internet radio stations much like Xmms. It is found in the Sound & Video menu as the Music Player menu item. You can also use it to subscribe to podcasts available through the Internet. Figure 10.10 shows Rhythmbox working with podcasts.

As mentioned earlier, Banshee can be used to handle your music library. It could be classed as an Apple iTunes lookalike, but it does not have access to the iTunes Music Store. Within Banshee you can store cover art for your CDs, create playlists and burn them to CDs. Although a fairly new application, it already has a raft of features and is sure to be expanded in future.

![](img/e464b828c497c99e41f61d4c55f1c0db_248_0.png)

**FIGURE 10.10** Rhythmbox can handle podcasts, Internet radio stations, CDs, and local sound files.

![](img/e464b828c497c99e41f61d4c55f1c0db_248_1.png)

**FIGURE 10.11** The new kid on the block, Banshee makes quick work of music management.

## Streaming Audio

Streaming audio is for playing games, listening to Internet radio, and other online audio content. Streaming audio is designed to produce an uninterrupted sound output, but it requires the system to perform a content juggling act. Essentially, the system’s audio buffer is continually filled with audio information, which is fed to the buffer through the system’s Internet connection. Because of server and connection capabilities, the rate of input might vary. Because audio is used at a constant rate, the trick to managing streaming audio is to always keep the buffer full, although you might not be able to fill it at a constant rate.

Streaming audio is handled in Ubuntu in the .m3u format. The MPEG formats are also used for streaming audio. Although Xmms supports streaming audio, another popular application is the Real Player, available from http://www.real.com/linux/. An excellent resource for music and sound in Linux is http://linux-sound.org/. The Network Audio section of that website contains an extensive list of streaming audio applications.

The Icecast application, not provided with Ubuntu, is a popular streaming audio server. You can use Icecast to serve your MP3 music collection over your home LAN. You can learn more about Icecast at http://www.icecast.org/. A nice tutorial on Icecast is available at http://www.linuxnetmag.com/en/issue4/m4icecast1.html.

**TIP**

You can also read Chapter 22, "File and Print," to see how to use the Network File System (NFS) to mount a remote directory of music files over your network.

## Viewing TV and Video

You can use Ubuntu tools and applications to view movies and other video presentations on your PC. This section presents some TV and motion picture video software tools included with the Ubuntu distribution you received with this book.

In addition to the information you read here, you should review Chapter 3, "Installing Ubuntu," and Chapter 6, "The X Window System," to learn more about installing and configuring your video graphics card.

## TV and Video Hardware

To watch TV and video content on your PC, you must install a supported TV card or have a video/TV combo card installed. A complete list of TV and video cards supported by Ubuntu is at http://www.exploits.org/v4l/. See the Gatos Project at http://gatos.sourceforge.net for information on ATI video combo cards.

Freely available Linux support for TV display from video cards that have a TV-out jack is poor. That support must come from the X11 driver, not from a video device that Video4Linux supports with a device driver. Some of the combo TV-tuner/video display cards have support, including the Matrox Marvel, the Matrox Rainbow Runner G-Series,
