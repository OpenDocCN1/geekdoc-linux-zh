
## Viewing Video in Linux

proprietary, but free codecs do exist. Here is a list of the most common video formats and their associated file extensions:

- `.mpg`—The MPEG video format; also known as `.mpg`
- `.qt`—The QuickTime video format from Apple
- `.mov`—Another QuickTime video format
- `.avi`—The Windows audio visual format

> An RPM that provides a Divx codec for Linux can be found at http://www.freshrpms.net/. Divx is a patented MPEG-4 video coder that is the most widely used codec of its type. It allows for compression of MPEG-2 video by a factor of 8. See http://www.divx.com/ for more information.
>
> The Getcodecs application is a Python script with a GUI interface that downloads, installs, and configures your Fedora system with multimedia codecs not provided by Fedora, such as MP3, Divx, and DVD codecs. The script can be obtained from http://sourceforge.net/projects/getcodecs/

If you need to convert video from one format to another, you use encoder applications called grabbers. These applications take raw video data from a video device such as a camera or TV card, and convert it to one of the standard MPEG formats or to a still image format, such as JPEG or GIF. Fedora does not supply any encoder applications (other than gptopampg which encodes MPEG-1 video), but you can find them at http://www.freshrpms.net/ or another online source (see the "Reference" section at the end of this chapter).

Because of the patent and licensing issues mentioned earlier, the capability to play video files has been removed from Fedora. This functionality can be restored if you install the full version of the applications described in this section from FreshRPMs at http://www.freshrpms.net/. There you can find multimedia applications such as Ogle, Xine, AlsaPlayer, Gstreamer, Grip, Mplayer, VCDImager, VideoLAN-client, Xmm, and Zapping.

You can use Linux software to watch TV, save individual images (take snapshots) from a televised broadcast, save a series of snapshots to build animation sequences, or capture video, audio, or both. The following sections describe some of the ways in which you can put Linux multimedia software to work for you.

The nathan viewer is provided with Fedora to use as an embedded viewer in the Konqueror browser. Nathan is set up as the default association for the video file formats it plays. Open a video file in Konqueror or Nautilus, and the video is shown in the viewer it is supported. The viewer provides basic start, stop, and fast-forward VCR-type functions.

You can watch MPEG and DVD video with Xine. Xine is a versatile and popular media player that is not included with Fedora. Xine is used to watch AVI, QuickTime, OGG, and MP3 files (the latter disabled in Fedora).

### MACROMEDIA FLASH

The Macromedia Flash plug-in for the Mozilla browser is a commercial multimedia application that isn't provided with Fedora, but many people find it useful. Macromedia Flash enables you to view Flash content at websites that support it. The Mozilla plug-in can be obtained from http://macromedia.mpulg.org/. Both .rpm and .tar.gz files are provided.

Download the file for Linux and, if using the .tar.gz file, uncompress it with:

```bash
tar zxvf install_flash_player_6_linux.tar.gz
```

This produces a directory named flashplayer_installer. Install the plug-in with:

```bash
./install_flash_player_6_linux/flashplayer_installer
```

and follow the screen prompts to install it and make it available to the Mozilla browser.

Having trouble with the Macromedia Flash plug-in for Mozilla? Just manually copy the files flashplayer.xpt and libflashplayer.so to /usr/lib/mozilla/plugins. An .rpm file for Flash that should install without problems is available from http://macromedia.mpulg.org/.

Another interesting video viewer application is MPlayer (not provided by Fedora), a movie player for Linux. MPlayer can use Win32 codecs and it supports a wider range of video formats than Xine, including Divx and some RealMedia files. MPlayer also uses some special display drivers that support Matrox, 3Dfx, and Radeon cards and can make use of some hardware MPEG decoder boards for better MPEG decoding. Look for Fedora packages at http://www.MPlayerHQ.hu/homepage/; a Win32 codec package is also available, as well as other codec packages and a GUI interface.

## Viewing Television with Linux

You can configure a number of video input sources to feed television images to your computer. You can use any supported TV device as described previously to connect cable TV, an Xbox, Sega Dreamcast, PS/2, or even an external television antenna to your computer and view the images on your video display.

Fedora provides the tvtime TV viewing application to enable you to watch Battlestar *Galactica* without leaving your computer.

### NOTE

The *kdetv* application (formerly known as QrVision) is steadily growing in terms of both popularity and features and is worth a look. It can be downloaded from http://www.kdetv.org/.

Start tvtime from the command line:

```bash
tvtime &
```

Right-clicking on it toggles the display of the Options menu. Adjust the settings to suit your hardware.

```bash
scantv
```

The *tvtime* configuration file details are contained in the man page for *tvtime*.

An alternative TV-viewing application available at FreshRPMs.Net is Zapping, a GNOME viewer that supports Video4Linux, Video4Linux2, and Xvideo and is extensible in functionality through plug-ins. The home page is http://zapping.sourceforge.net/.

## Personal Video Recorders

The best reason to attach a television antenna to your computer, however, is to use the video card and the computer as a personal video recorder.

The commercial personal video recorder, TiVo, uses Linux running on a PowerPC processor to record television programming with a variety of customizations. TiVo has a clever interface and wonderful features, including a record/playback buffer, programmed recording and pause, slow motion, and reverse effects. Fedora does not provide any of the many applications that attempt to mimic the TiVo functionality on a desktop PC running Linux. However, several such applications, including DVR, The Linux TV Project, and OpenPVR, are listed at http://www.explorts.org/v4l/. These projects are in development and do not provide .rpm files, so you have to know how to download from CVS and compile your own binaries. For something a little easier, check out MythTV at http://www.mythtv.org/; a Fedora .rpm file should be available from FreshRPMs.Net.

### LINUX, TiVO, AND PVRS

Some TiVo users say that using this Linux-based device has changed their lives. Indeed, the convenience of using a personal video recorder (PVR) can make life a lot easier for inveterate channel surfers. Although PVR applications are not included with Fedora Core Linux, open source developers are working on newer and better versions of easy-to-install and easy-to-use PVR software for Linux. For more information about TiVo, which requires a monthly charge and a phone line (or broadband connection with a newer TiVo2), browse to http://www.tivo.com/. Unrepentant Linux hardware hackers aiming to disembowel or upgrade a TiVo can browse to http://www.9thtee.com/tivohackers.htm or read the TiVo Hack FAQ at http://www.tivofaq.com/hack/faq.html. A PVR makes viewing television a lot more fun!

A number of Linux sites are devoted to PVR software development. Browse to the DVR project page at http://dvr.sourceforge.net/.

## DVD and Video Players

You can now easily play DVDs using Fedora as long as you install the appropriate software. (Fedora doesn’t provide any.) Browse to http://www.videolan.org/, and then download, build, and install the vlc client.

You must have a CPU of at least 450MHz and a working sound card to use a DVD player. The default Fedora kernel supports the DVD CD-ROM file system. As mentioned earlier, Xine and MPlayer do a great job of playing DVD files.

### NOTE

> The VideoLAN HOWTO found at http://videolan.org/ discusses the construction of a network for streaming video. Although you might not want to do that, a great deal of useful information about the software and hardware involved in the enterprise can be generalized for use elsewhere, so it is worth a look. The site also contains a link to a HOWTO about cross-compiling on Linux to produce a Windows binary.

## ENABLING JAVA

Some multimedia content relies on Sun’s Java and Java web browser plug-ins.

Getting the Java plug-in to work correctly with the Mozilla browser can be a challenge. Download the latest version (versions prior to 1.4.1 do not work) from http://java.sun.com/. (You can find a modified .rpm version of the files at http://dag.wieers.com/packages/j2re/.) As root, make the downloaded file executable with `chmod +x` and unpack it with:

```bash
rpm -ivh j2re-1.4.2_05-linux-i586.rpm
```

To make the Java plug-in work with Mozilla, you need to link it correctly:

```bash
ln -s /usr/java/j2re1.4.2_05/plugin/i386/ns610-gcc32/lib/javaplugin_oji.so /usr/lib/mozilla/plugins/
```

You might also need to link the Java binary into /usr/bin:

```bash
ln -s /usr/java/j2re1.4.2_05/bin/java /usr/bin/java
```

Java can be difficult to install properly because of PATH problems. Here’s a way to do it correctly: Edit your /etc/profile file to add the following lines. This informs the system where the Java executable is found.

```bash
JAVA_HOME=/usr/java/j2re1.4.2_05
PATH=/usr/java/j2re1.4.2_05/bin:$PATH
```

You can also find numerous multimedia goodies at http://freshrpms.net/ and at http://www.cs.trinity.edu/pub/fc2-Software-Additions//. The multimedia applications that used to be part of Fedora before its merger with Red Hat are now housed at http://rpm.livna.org/. To add this repository to yum, add to /etc/yum.conf the lines
