
One good source for audio streams is `www.shoutcast.com`. Click any of the Tune In! buttons and Mozilla downloads several playlists and launches MPlayer to play the music via the playlists.

*Playlists* are files that store the locations of one or more audio and video streams. For example, if you click any of the Shoutcast streams (at `www.shoutcast.com`), Mozilla saves the playlist to the `/tmp` directory, starts MPlayer, and directs it to play the playlists. The playlist MIME type, `x-scpls`, was inserted into Mozilla as a helper application when you installed the MPlayer packages.

Alternatively, you can click the Save to disk button and save the playlist to your home directory. You can then manually start MPlayer from a terminal emulator window or the Run Program utility with the command `mplayer -playlist playlist.pls`.

![](img/8c094d1b36276212c03d10d898508a6e_179_0.png)

You can use MPlayer to play music files too. Suppose that you use *grip* in Chapter 11 to save some music to a file named `track1.wav`. Enter this command to play that file:

```
mplayer track1.wav
```

Press the Control key and then the C key (Ctrl-c) to end the session.

You can use MPlayer to listen to all sorts of streams. The entire world of Internet radio and — hopefully, soon — video broadcast is open to you. MPlayer will only become more versatile and useful.

MPlayer plays DVDs too! Use the command `grep -i dvd /var/log/dmesg` to locate the DVD device file. For example, your DVD device file should be something like `/dev/hdd`. Next, create a *soft link file* so that MPlayer knows where to find the DVD drive: `ln -s /dev/hdd /dev/dvd`. Start MPlayer, right-click the MPlayer - Video window and choose Open->Play DVD. The DVD plays.

![](img/8c094d1b36276212c03d10d898508a6e_179_1.png)

The first MPlayer RealAudio (using the RTSP protocol) plug-in was just recently released from `www.live.com/mplayer`. The plug-in is still too young for easy use, but soon will be. Keep an eye on this system. When the Live.com RTSP plug-in for MPlayer matures, you can listen to an outstanding interview with The Man himself — Linus Torvalds — by opening this URL from gmplayer or MPlayer:

![](img/8c094d1b36276212c03d10d898508a6e_179_2.png)

```
rtsp://audio.npr.org/fa/20010604.fa.rm
```

In this clip, Terri Gross, from National Public Radio, conducts an interview during the summer of 2001 on her program, “Fresh Air.” Linus discusses the development of Linux, his life in Silicon Valley, and other matters. You can also use the commercial RealPlayer8 to listen to this or any RealAudio stream. The section in Chapter 11 about plugging in plug-ins describes where to obtain the RealPlayer8 RPM package.

# Audio by proxy: Getting XMMS to work through your firewall

Firewalls are necessary to fight the evil guys who lurk on the Internet, but they can put a kink in your listening pleasure. A *firewall* is used to prevent unauthorized access from the outside — in most cases, the Internet — from reaching your computer or network.

The firewall we show you how to build in Chapter 8 and the default Red Hat firewall don't affect either of the players described in this chapter. However, many LANs are connected through *proxy* firewalls, which intercept packets sent to the Internet and rewrite them according to certain rules; our firewalls filter packets based on their source and destination addresses and ports.

(gmplayer doesn't have any mechanism specifically designed to work with proxies.)

To configure XMMS to work with proxy firewalls, follow these steps:

1.  **Start XMMS, right-click the XMMS window, and choose Options → Preferences.**
2.  **Click the Ogg Vorbis plug-in in the Input Plug-ins subwindow and click Configure.**

The Ogg Vorbis Configuration window opens. You need to enter the address of your proxy server. You may need to contact your friendly neighborhood systems administrator to get that information.

3.  **Click the Use Proxy button and enter the proxy server address in the Host sub-window.**

If your Red Hat Linux workstation sits on a network with a packet-filtering firewall, such as the one you may have installed in Chapter 8, you don't need to modify XMMS. The key is that the filtering firewall allows all outgoing TCP and UDP connections (or ports). However, if your network uses a proxy-based firewall, you may have to modify XMMS.

4.  **Click the Use Authentication radio button and enter your username and password in their respective subwindows if your proxy server requires them.**

# Launching gmplayer from the GNOME Panel

![](img/8c094d1b36276212c03d10d898508a6e_180_0.png)

Until now, you have been manually launching MPlayer. Now it's time to put gmplayer in its place on the GNOME Panel. You can create an applet launcher (an icon to click) for gmplayer on the GNOME Panel.

The *Panel* is the gray bar that rests along the bottom of your screen.

Follow these steps to create a launcher applet for gmplayer:

1.  **Right-click any blank section of the GNOME Panel and choose Add to Panel → Launcher items.**
2.  **Type a name for the gmplayer launcher icon and press the Tab key to display the Generic Name text box. Enter any name you want.**

An entry such as `Radio Player` or `Streaming Audio/Video player` describes what the launcher is meant to do.

3.  **Press the Tab key again and enter a descriptive comment in the Comment text box.**

The comment is displayed whenever you place the cursor over the MPlayer icon.

4.  **Press the Tab key one more time and type /usr/bin/gmplayer in the Command text box.**
5.  **Click the Icon button at the bottom of the Launcher window to pick an icon for the launcher.**

The Browse icons window opens and displays the generic GNOME icon images. You can select any image you want by clicking the image and then clicking the OK button. You return to the Create Launcher window.

Selecting an icon image in this step means that you can skip Steps 7 through 9, which help you find custom icon images. Skip to Step 9.

6.  **Click the Browse button to select a custom image.**

The Browse window opens.

7.  **Select any generic icon you like and click the OK button.**

The gmplayer icon is displayed in the Launcher window, ready and waiting to launch the program.

8.  **Click the Close button and the gmplayer icon is placed on the GNOME Panel.**
9.  **Click the OK button in the Launcher window and click the new gmplayer launcher you just created on the GNOME Panel.**

The new icon is inserted into the GNOME Panel and the gmplayer window opens.

You can also reach gmplayer from the GNOME menu. After you install the MPlayer packages, log out and then log in again. Click the GNOME Menu button and choose Sound & Video → More Sound & Video Applications → gmplayer.

![](img/8c094d1b36276212c03d10d898508a6e_181_0.png)

You can easily copy the gmplayer icon (or any icon) from the GNOME Panel to your desktop. Click and hold the gmplayer icon in the GNOME Panel and drag it to your desktop. Release the mouse button and the icon is copied to your desktop background. You can then right-click the desktop icon and choose Properties from the menu that pops up. The gmplayer Properties window opens and enables you to modify the icon’s look and feel.

# Chapter 13

## Going to the Office

### In This Chapter

- Introducing OpenOffice
- Using OpenOffice Writer
- Printing from OpenOffice

**R**ed Hat Linux is a great product that comes with a large base of services and applications. It has always been an outstanding platform for providing services and technical applications. But you didn’t find Red Hat, until recently, on many of the world’s workday computers; in other words, it lacked a presence on the “desktop.”

The Red Hat problem was its lack of a full-blown office suite to work with word processing documents, spreadsheets, and similar documents. Fortunately, desktop productivity suites — such as OpenOffice and its sister application, StarOffice — have taken Linux out of the back office and into the front.

## Opening Your Office

The OpenOffice desktop productivity suite does nearly everything Microsoft Office does, but for less money. How much less? Well, 100 percent less because it’s 100 percent free. Sun Microsystems, Inc., sells the version named StarOffice and also provides an open source version named — you guessed it — OpenOffice. OpenOffice is licensed under the GPL/LGPL and SISSL licenses. What do all those letters mean? They mean f-r-e-e, and they also mean that Linux can integrate office productivity features from OpenOffice because Linux and OpenOffice share the GPL license. You can find more information about the licenses at `www.openoffice.org/project/www/license.html`.

OpenOffice is not only free (did we mention that it’s free?), but it’s also powerful, providing you with these functions:
