
Therefore, you can use TVtime to view Webcams as well as receive television channels. The following sections describe how to choose a TV capture card and use TVtime to watch television on your desktop.

> **NOTE:** TVtime will not display output from some low-quality Webcams. To use your Webcam, consider obtaining the xawtv package, which is available by typing `yum install xawtv`.

## Getting a supported TV card

Video4Linux is the video interface included with Fedora. It supports a variety of TV capture cards and cameras.

To see a list of supported TV cards that you can use with TVtime, refer to the `CARDLIST` and `Cards` files. To view these files, you need to have the kernel-doc package installed. You’ll find the `CARDLIST.tuner` file in the following location on your Linux system:

```
/usr/share/doc/kernel-4-doc*/Documentation/video4linux/
```

The `CARDLIST.bttv` file applies to the Video4Linux bttv driver, which lists many TV capture cards by card number, name, and sometimes by chip set. Also, the `CARDLIST.tuner` lists tuner types that might be associated with different TV cards.

Video4Linux is designed to auto-detect your TV capture card and load the proper modules to activate it. So, physically install the TV-card hardware (with the appropriate connection to your TV reception), boot Fedora, and run the `tvtime` command as described in the next section. You should be able to see video displayed on your TVtime window.

If your card appears not to be working, here are a few things you can try:

- To see if your TV card was properly seated in its slot and detected by Linux, type the following:

```
$ /sbin/lspci | less
```

This will show you a list of all valid PCI cards on your computer. If nothing shows up for the card that says something like “Multimedia video controller,” you probably have a hardware problem. My Hauppauge WinTV Go card (with Brooktree chipset support) appears as:

```
Multimedia video controller: Brooktree Corporation Bt878 Video Capture
```

- It is possible that the card is there, but the right card type is not being detected. Improper detection is most likely the issue if you have a card for which there are several revisions, with each requiring a different driver. If you think your card is not being properly detected, find your card in the `CARDLIST` files. Then add the appropriate line to the `/etc/modprobe.conf` file. For example, to add a Prolink PV-BT878P, revision 9B card, add the following line to `/etc/modprobe.conf`:

```
options bttv card=72
```

You can also add other options listed in the *Insmod-options* file for the btv driver. If you are still having problems getting your card to work, a mailing list is available on which you can ask questions about Video4Linux issues:

```
http://listsman.redhat.com/mailman/listinfo/video4linux-list
```

One possible reason that you don't see any video when you try to run TVtime or other video applications is that some other person or video application already has the video driver open. Only one application can use the video driver at a time in Fedora. Another quirk of Video4Linux is that the first person to open the device on your system becomes the owner. So you might need to open the permissions of the device file (such as /dev/video0) to allow people other than the first person to use it to access the video4linux driver (for example, chmod 666 /dev/video0).

## Starting TVtime

To start up the TVtime viewer, simply select the TVtime Television Viewer choice from the Sound & Video menu. Or, type the following from a Terminal window on your desktop:

```
$ tvtime &
```

A video screen should appear in a window on the desktop. Click the left mouse button on the window to see the current channel number, current time, and current video source (Television, Composite1, and so on). Click the right mouse button to see the onscreen Setup menu. If your card seems to have been detected and the needed modules were properly loaded, but you don't see any video, try using the keyboard arrow keys to step forward until you find a valid channel. If that doesn't work, try going through the following adjustments (most important, the video source and television standard), to get TVtime working properly:

- **Configuration input** — This choice allows you to change the video source, choose the television standard (which defaults to NTSC for the USA), and change the resolution of the input. To change the video source to Composite1, S-Video, Television, or other input source, right-click the TVtime window, select Input configuration → Change video Source. To change Television standard, select Television standard and choose NTSC (U.S.), PAL (Europe), or other available settings.

- **Set up the picture** — Adjust the brightness, contrast, color, and hue. Right-click the TVtime window, select Picture settings, and then choose Brightness, Contrast, Saturation, or Hue to adjust those attributes.

- **Adjust the video processing** — You can control the attempted frame rate, configure the deinterlacer, or add an input filter. Right-click the TVtime window, select Video processing, and then choose Attempted framerate (to slow the frame rate) or a Deinterlacer option (to change other processing features). You can also try Input filters to do some fun things like invert color, flip the video as though in a mirror image, or put the video in black and white (using Chroma killer).

If you view television often from your computer, consider adding an icon to your panel (right-click the panel and select Add to Panel Application Launcher Sound & Video TVtime). With TVtime running, you can put it on top by right-clicking the title bar and selecting On Top.

## Selecting channels in TVtime

With video input working and the picture adjusted to your liking, you should set up your channels. Right-click the TVtime window, select Channel management Scan channels for signal. TVtime will scan for all available channels and note which ones have active signals. Once channels have been scanned, you can use your mouse wheel to change among the active channels. If TVtime missed an active channel, use your keyboard arrow keys to go to the missed channel and select Channel management Current channel active in list.

> **TIP:** The xmrlv project provides a means of identifying and downloading TV listings for your area. TVtime includes support for xmrlv listing files, allowing you to display current television shows and station names while you go through TVtime channels. It can be tricky getting xmrlv going. If you are interested, I suggest you start at the XMLTV project site (http://xmltv.org/index.php/Main_Page).

## Video conferencing and VOIP with Ekiga

The Ekiga application (formerly called GnomeMeeting) enables you to communicate with other people over a network through video, audio, and typed messages. Because Ekiga supports the H323 protocol, you can use it to communicate with people using other video-conferencing clients, such as Microsoft NetMeeting, Cu-SeeMe, and Intel VideoPhone. Besides video conferencing, Ekiga also supports VOIP and IP telephony, to make telephone calls over the Internet.

To be able to send video, you need a Webcam that is supported in Linux. Although not all Webcams are supported in Linux, you still have a few dozen models to choose from. The following sections show you how to set up your Webcam and use Ekiga for video conferencing.

## Getting a supported Webcam

As with support for TV capture cards, Webcam support is provided through the Video4Linux interface. Some of the supported cameras have a parallel-port interface, although most Webcams currently supported in Linux require a USB port.

Finding a Webcam to work in Linux is a bit of an adventure. Few (if any) Webcams come with Linux drivers or specs to allow open source developers to create those drivers. Webcam drivers that have been created often have limited features and sometimes break with new kernel releases. Also, Webcam vendors sometimes switch the chip sets they are using without changing the Webcam’s name. And there are times when the same Webcam is marketed under different names.
