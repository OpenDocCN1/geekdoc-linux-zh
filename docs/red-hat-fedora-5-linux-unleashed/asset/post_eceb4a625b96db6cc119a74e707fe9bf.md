
![](img/2045828cf45e5632bf056f9ca99d6755_311_0.png)

FIGURE 10.6 Rhythmbox can handle podcasts, Internet radio stations, CDs, and local sound files.

> Menu editing is available in the GNOME metadata desktop provided as the default Fedora Core desktop. All you have to do is right-click on the Fedora Applications button and select Edit Menus. You can then select and deselect options as appropriate.

## Streaming Audio

Streaming audio is for playing games, listening to Internet radio, and other online audio content. Streaming audio is designed to produce an uninterrupted sound output, but it requires the system to perform a content juggling act. Essentially, the system's audio buffer is continually filled with audio information, which is fed to the buffer through the system's Internet connection. Because of server and connection capabilities, the rate of input might vary. Because audio is used at a constant rate, the trick to managing streaming audio is to always keep the buffer full, although you might not be able to fill it at a constant rate.

Streaming audio is handled in Fedora in the .m3u format. The MPEG formats are also used for streaming audio. Although Xmsm supports streaming audio, another popular application is Real Player, available from http://www.real.com/linux/. An excellent resource for music and sound in Linux is http://linux-sound.org/. The Network Audio section of that website contains an extensive list of streaming audio applications.

The Icecast application, not provided with Fedora, is a popular streaming audio server. You can use Icecast to serve your MP3 music collection over your home LAN. You can learn more about Icecast at http://www.icecast.org/. A nice tutorial on Icecast is available at http://www.linuxnetmag.com/en/issue4/m4icecast1.html.

> **TIP**
> You can also read Chapter 18, "Network Connectivity," to see how to use the Network File System (NFS) to mount a remote directory of music files over your network.

## Viewing TV and Video

You can use Fedora tools and applications to view movies and other video presentations on your PC. This section presents some TV and motion picture video software tools included with the Fedora Core Linux distribution you received with this book.

In addition to the information you read here, you should review Chapter 3, "Installing Fedora," and Chapter 6, "The X Window System," to learn more about installing and configuring your video graphics card.

### TV and Video Hardware

To watch TV and video content on your PC, you must install a supported TV card or have a video/TV combo card installed. A complete list of TV and video cards supported by Fedora is at http://www.expolots.org/~v4/l/. See the Gatos Project at http://gatos.sourceforge.net for information on ATI video combo cards.

Freely available Linux support for TV display from video cards that have a TV-out jack is poor. That support must come from the X11 driver, not from a video device that Video4Linux supports with a device driver. Some of the combo TV-tuner/video display cards have support, including the Matrox Marvel, the Matrox Rainbow Runner G-Series, and the RivaTV cards. Many other combo cards lack support, although an independent developer might have hacked something together to support his own card. Your best course of action is to perform a thorough Internet search using Google.

Many of the TV-only PCI cards are supported. In Linux, however, they are supported by the video chipset they use, and not by the name some manufacturer has slapped on a generic board (the same board is typically sold by different manufacturers under different names). The most common chipset is the Brooktree Bt8xx series of chips; they are supported by the bttv device driver.

If you have a supported card in your computer, it should be detected during installation. If you add it later, the Kudzu hardware detection utility should detect it and configure it. You can always configure it by hand.

To determine what chipset your card has, use the lspci command to list the PCI device information, find the TV card listing, and look for the chipset that the card uses. For example, the lspci output for our computer shows:

```bash
# lspci
00:00.0 Host bridge: Advanced Micro Devices [AMD] AMD-760 [IGD4-1P]
    - System Controller (rev 13)
00:01.0 PCI bridge: Advanced Micro Devices [AMD] AMD-760 [IGD4-1P]
    - AGP Bridge
00:07.0 ISA bridge: VIA Technologies, Inc. VT82C686 [Apollo Super South]
    - (rev 40)
00:07.1 IDE interface: VIA Technologies, Inc. VT82C586B PIPC Bus Master IDE
    - (rev 06)
00:07.2 USB Controller: VIA Technologies, Inc. USB (rev 1a)
00:07.3 USB Controller: VIA Technologies, Inc. USB (rev 1a)
00:07.4 SMBus: VIA Technologies, Inc. VT82C686 [Apollo Super ACPI]
    - (rev 40)
00:09.0 Multimedia audio controller: Ensoniq 5880 AudioPCI (rev 02)
00:0b.0 Multimedia video controller: Brooktree Corporation Bt878 Video Capture
    - (rev 02)
00:0b.1 Multimedia controller: Brooktree Corporation Bt878 Audio Capture
    - (rev 02)
00:0d.0 Ethernet controller: Realtek Semiconductor Co., Ltd. RTL-8029(AS)
00:0f.0 FireWire (IEEE 1394): Texas Instruments TSB12LV23 IEEE-1394
    - Controller
00:11.0 Network controller: Standard Microsystems Corp [SMC]
    - SMC2602W E2ZConnect
01:05.0 VGA compatible controller: nVidia Corporation NV15 [GeForce2 Ti]
    - (rev a4)
```

Here, the lines listing the multimedia video controller and multimedia controller say that our TV board uses a Brooktree Bt878 Video Capture chip and a Brooktree Bt878 Audio Capture chip. This card uses the Bt878 chipset. Your results will be different, depending on what card and chipset your computer has. This card happened to be an ATI All-in-Wonder VE (also known as ATI TV-Wonder). (The VE means *Value Edition*; hence, there is no TV-out connector and no radio chip on the card; what a value!) The name of the chipset tells us that the card uses the bttv driver.

In the documentation directory, we find a file named **CARDLIST**, and in that file is the following entry, among others:

```
card=64 - ATI TV-Wonder VE
```

There are 105 cards listed as well as 41 radio cards, including:

```
card=0 - *** UNKNOWN/GENERIC ***
```

which is what we would have used had we not known the manufacturer's name for our card.

The file named Modules.conf, located in the same directory, gives us the following example of information to place in our /etc/modules.conf file:

```
# i2c
alias char-major-89 i2c-dev
options i2c-core i2c_debug=1
options i2c-algo-bit bit_test=1

# bttv
alias char-major-81 videodev
alias char-major-81-0 bttv
options bttv card=2 radio=1
options tuner debug=1
```

All we need do is enter this information into /etc/modules.conf and change the value for card=2 to card=64 to match our hardware. We can delete the reference to the radio card (radio=1) because we do not have one and leave the other values alone. Then we must execute:

```
# depmod -a
```

to rebuild the modules dependency list so that all our modules are loaded automatically. When finished, all we need do is execute:

```
# modprobe bttv
```

and our TV card should be fully functional. All the correct modules will be automatically loaded every time we reboot. Fedora is clever enough to detect and configure a supported TV card that is present during installation.

![](img/2045828cf45e5632bf056f9ca99d6755_314_0.png)

> Other useful documentation can be found in /usr/src/linux-2.6/Documentation/video4linux. After you have identified a driver for a device, it does not hurt to look at the source code for it because so little formal documentation exists for many drivers; much of it is in the source code comments.

The development of support for TV cards in Linux has coalesced under the Video4Linux project. The Video4Linux software provides support for video capture, radio, and teletext devices in Fedora Core.

## Video Formats

Fedora recognizes a variety of video formats. The formats created by the MPEG group, Apple, and Microsoft dominate, however. At the heart of video formats are the codecs—the encoders and decoders of the video and audio information. These codecs are typically
