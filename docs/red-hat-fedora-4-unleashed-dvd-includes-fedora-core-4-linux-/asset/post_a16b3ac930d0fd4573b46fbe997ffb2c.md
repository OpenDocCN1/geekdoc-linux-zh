
> TIP  
> To learn more about the technical details of audio formats, read Chris Bagwell's Audio Format FAQ at http://www.cnpbagwell.com/audio.html.

Fedora also offers utilities for converting sound files from one format to another. Conversion utilities come in handy when you want to use a sound in a format not accepted by your current application of choice. A repository of conversion utilities resides at http://ibiblio.org/pub/linux/apps/sound/convert/!INDEX.html and includes MP3 and music CD-oriented utilities not found in Fedora. You will have to know how to compile and install from source, however. If you see something useful, have a look at http://www.rpmfind.net/ to locate a binary RPM if you don't feel up to the task.

Fedora does provide sox, a self-described sound translator that will convert music between the AIFF, AU, WAV, DAT, OGG, and WAV formats, among others. It also can be used to change many other parameters of the sound files.

Timidity is a MIDI to WAV converter and player. If you are interested in MIDI and musical instruments, Timidity is a handy application; it handles karaoke files as well, displaying the words to accompany your efforts at singing.

## Music Players

Fedora provides music players. One of the most popular is Xmms, a Winamp clone, which in the full version can play not only music, but MPEG1/2/3 video as well. Xmms supports a number of plug-ins that can add dancing, lighted oscilloscope-like displays, redirect its output to other devices, support unusual file formats, sync animations to the music, and otherwise increase its geek appeal exponentially. You can find Xmms as the Media Player item in the Sound & Video menu.

The default music player is Rhythmbox, which is designed to play music files from playlists and Internet radio stations much like Xmms. It is found in the Sound & Video menu as the Music Player menu item.

Kmid, found in the More Sound & Video Applications submenu, is a karaoke and MIDI mapper; it supports external synthesizers. MIDI mappers enable you to map MIDI channels to the synthesizer instruments you want them to control. If you enjoy karaoke, Kmid will also enable you to change the tempo of songs without changing the pitch, and permits the organization of your songs into collections with a selectable play order.

Gnome-CD is the CD Player menu item found in the Sound & Video menu. As the default CD player application, it provides a basic GUI interface for playing CDs in your CD-ROM drive.

Other music and sound-related applications can be found in the Sound & Video menu, and, of course, you are free to install your own selection of applications as well. You might have a problem adding them to the menu, however, so we provide the following tip to enable menu editing in Fedora.

> TIP

Menu editing is available in the GNOME/metacity desktop provided as the default Fedora Core desktop, but it is inexplicably disabled. To enable it, working as root perform the following steps:

```
# cd /etc/gnome-vfs-2.0/modules
# mv default-modules.conf default-modules.conf.without-menu-editing
# cp default-modules.conf.with-menu-editing default-modules.conf
```

Upon restarting GNOME, you can edit the menu by right-clicking on the menu item or by using the URL `applications:///` in Nautilus.

## Streaming Audio

Streaming audio is for playing games, listening to Internet radio, and other online audio content. Streaming audio is designed to produce an uninterrupted sound output, but it requires the system to perform a content “juggling act.” Essentially, the system’s audio buffer is continually filled with audio information, which is fed to the buffer through the system’s Internet connection. Because of server and connection capabilities, the rate of input might vary. Because audio is used at a constant rate, the trick to managing streaming audio is to always keep the buffer full, although you might not be able to fill it at a constant rate.

Streaming audio is handled in Fedora Core Linux in the .m3u format. The MPEG formats are also used for streaming audio. Although Xmms supports streaming audio, another popular application is the Real Player, available from [http://www.real.com/linux/](http://www.real.com/linux/). An excellent resource for music and sound in Linux is [http://linux-sound.org/](http://linux-sound.org/). The Network Audio section of that website contains an extensive list of streaming audio applications.

The Icecast application, not provided with Fedora Core Linux, is a popular streaming audio server. You can use Icecast to serve your MP3 music collection over your home LAN. You can learn more about Icecast at [http://www.icecast.org/](http://www.icecast.org/). A nice tutorial on Icecast is available at [http://www.linuxnetmag.com/en/issue4/m4icecast1.html](http://www.linuxnetmag.com/en/issue4/m4icecast1.html).

> TIP

You can also read Chapter 17, “Network Connectivity,” to see how to use the Network File System (NFS) to mount a remote directory of music files over your network.

## Viewing TV and Video

You can use Fedora tools and applications to view movies and other video presentations on your PC. This section presents some TV and motion picture video software tools included with the Fedora Core Linux distribution you received with this book.

In addition to the information you read here, you should review Chapter 3, “Installing Fedora,” and Chapter 6, “The X Window System,” to learn more about installing and configuring your video graphics card.

## TV and Video Hardware

To watch TV and video content on your PC, you must install a supported TV card or have a video/TV combo card installed. A complete list of TV and video cards supported by Fedora Core Linux is at http://www.exploits.org/v4/. See the Gatos Project at http://gatos.sourceforge.net for information on ATI video combo cards.

Freely available Linux support for TV display from video cards that have a TV-out jack is poor. That support must come from the X11 driver, not from a video device that Video4Linux supports with a device driver. Some of the combo TV-tuner/video display cards have support, including the Matrox Marvel, the Matrox Rainbow Runner G-Series, and the RivaTV cards. Many other combo cards lack support, although an independent developer might have hacked something together to support his own card. Your best course of action is to perform a thorough Internet search using Google.

Many of the TV-only PCI cards are supported. In Linux, however, they are supported by the video chipset they use, and not by the name some manufacturer has slapped on a generic board (the same board is typically sold by different manufacturers under different names). The most common chipset is the Brooktree Bt878 series of chips; they are supported by the bttv device driver.

If you have a supported card in your computer, it should be detected during installation. If you add it later, the Kudzu hardware detection utility should detect it and configure it. You can always configure it by hand.

To determine what chipset your card has, use the lspci command to list the PCI device information, find the TV card listing, and look for the chipset that the card uses. For example, the lspci output for our computer shows

```
# lspci
00:00.0 Host bridge: Advanced Micro Devices [AMD] AMD-760 [IGD4-1P]  System Controller (rev 13)
00:01.0 PCI bridge: Advanced Micro Devices [AMD] AMD-760 [IGD4-1P]  AGP Bridge
00:07.0 ISA bridge: VIA Technologies, Inc. VT82C686 [Apollo Super South]  (rev 40)
00:07.1 IDE interface: VIA Technologies, Inc. VT82C586B PIPC Bus Master IDE  (rev 06)
00:07.2 USB Controller: VIA Technologies, Inc. USB (rev 1a)
00:07.3 USB Controller: VIA Technologies, Inc. USB (rev 1a)
00:07.4 SMBus: VIA Technologies, Inc. VT82C686 [Apollo Super ACPI]  (rev 40)
00:09.0 Multimedia audio controller: Ensoniq 5880 AudioPCI (rev 02)
00:0b.0 Multimedia video controller: Brooktree Corporation Bt878 Video Capture  (rev 02)
```
