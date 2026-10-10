
## Music, Video, and Images in Linux

driver. Cameras include the Aiptek Pencam and Niss Quickpix 2 (Vendo/product ID 0553/0202). For information on the driver, refer to the Linux STV0680 USB Support page (http://stv0680-usb.sourceforge.net).

- **Ultracam Webcams** (ultracam driver) — Supports Webcams such as the IBM Ultra-Port Camera II. See the ultracam driver page (www.gutwin.org/cam/source) for information about the driver.
- **Vicam Webcams** (vicam driver) — The 3Com HomeConnect USB Webcam is supported by this driver. Refer to the driver's project page for further information (http://homeconnectusb.sourceforge.net).
- **Winbond Webcams** (w9968cf driver) — Supports the W9968cf JPEG USB dual mode camera chip from Winbond Electronics. Webcams that use that chip include the ADG-5000 Aroma Digi Pen, Ezonics EZ-802 EZMega Cam, and the Pretec DigiPen-480. Refer to the Linux Projects site (www.linux-projects.org) for further information.

Check out the following web sites for a more complete list of Webcams that are and are not supported in Linux. Keep in mind, however, that not all of the drivers for these Webcams will work in the latest kernels in CentOS.

- Linux USB Device Drivers (www.linux-usb.org/devices.html)
- Linux web cams (http://302found.com/linux/webcams/)

The Logitech QuickCam Pro 300 Webcam that I used for examples in this chapter works well with the pwc driver that comes with CentOS. To check that it was working, I ran the `lsmod` command to see that the pwc driver was loaded and associated with the videodev module:

```bash
# lsmod
pwc                43392     0
compat_ioctl32      5569   1 pwc
videodev            5120   1 pwc
```

To see information about the pwc module (which is specific to this Webcam), I typed the following `modinfo` command:

```bash
# modinfo -p pwc
dev_hint:Device node hints
leds:LED on,off time in milliseconds
compression:Preferred compression quality. Range 0 (uncompressed) to 3 (high compression)
power_save:Turn power save feature in camera on or off
trace:For debugging purposes
mbufs:Number of external (mmap(ed) image buffers
fbufs:Number of internal frame buffers to reserve
fps:Initial frames per second. Varies with model, useful range 5-30
size:Initial image size. One of sqcif, qcif, cif, cif, vga
```

## Running Ekiga

To start Ekiga, select **Applications > Internet > IP Telephone, VOIP and Video Conferencing.** To start Ekiga from a Terminal window, type `ekiga &`. If it is not installed, you can install the *ekiga* package from the DVD that comes with this book. The first time you run Ekiga, the Ekiga Configuration Assistant starts. The assistant lets you enter the following information:

- **Personal Data** — Your first name, last name, e-mail address, comment, and location. You can also select whether or not you want to be listed in the Ekiga ILS directory.
- **Connection Type** — Indicate the speed of your Internet connection (56K modem, ISDN, DSL/Cable, T1/LAN, or Custom).
- **Audio Manager** — Typically, you would choose ALSA as your audio manager.
- **Video Manager and Devices** — Typically, you would choose Video4Linux as the video manager and your Webcam as the input device.

> **NOTE** If you want to reconfigure Ekiga later, run the following command to clean out the old settings: `ekiga-config-tool --clean`. Make sure that all instances of Ekiga are stopped before running that configuration tool. In addition, be sure to shut down the panel application that may still be running even after stopping Ekiga. Run `ekiga` again to re-enter your settings.

Figure 7-10 shows the Ekiga window.

![](img/2f265415ceec72538dd3c78ffca75c10_317_0.png)

In the Ekiga window that opens, you can click on the rolodex icon to open an address book. From the address book, select “Ekiga White Pages.” By typing a name into the search filter, you can search for people who might be connected to Ekiga server by first name, last name, e-mail address, or location. Select a person from the list that appears and, if he or she accepts your call, you can begin videoconferencing. The History tab shows a log of your activities.

### Playing Video

Video recording (encoding) and playback (decoding) remain among the most contentious areas of potential litigation in Open Source software. On one hand, you have patent holders of complex video formats that might ask for royalties for Open Source codecs (even when the software was written from “scratch”). On the other hand, you have the movie industry, which has taken aim at those publishing what they had hoped were secret encryption techniques (DeCSS), to prevent the Open Source decoding of commercial movies. The problem is that the same technique that allows you to play movies in Linux also can be used to copy and share them.

> **NOTE** Codec stands for Coder/Decoder or Compressor/DECompressor, depending on whom you ask. In either case, codecs are what make it possible to process and encode audio and video on computers.

As with audio recording, if you are starting from scratch, there is an Open Source codec called Theora (www.theora.org) that you can use without paying any royalties. As of this writing, Provided you own the content you are recording, you can freely distribute that content as well and allow others to play it back. (See the sidebar “Converting Video to Theora” for details.)

When it comes to including video codecs (other than the free Theora), CentOS has taken the cautious approach. While CentOS now includes video players such as Totem (described later in this chapter), it does not include players (such as the MPlayer and Xine media players) that often are packaged with contentious codecs. If you want to play commercial movies, popular video clips, or other video content in a CentOS system, you have to get those codecs elsewhere.

This section describes some of the issues surrounding playing and creating videos in Linux. It also describes video players that come with CentOS, as well as those you can obtain to play a wide variety of video content.

### Examining Laws Affecting Video and Linux

I need to start out by reminding everyone that I am not a lawyer, so you need to take responsibility yourself regarding any software you put on your computers. However, there are several themes that have arisen in regard to playing video content with Open Source software in Linux:

- Licensing fees for patented codecs may be required. While many video codecs are covered by patents, some patent holders don’t charge for personal use. However, you should check current policies of companies who own patents on codecs you plan to use, as the terms of use are constantly changing. For example, this statement that was once posted on the DivX web site is no longer there: ‘Personal use of DivX video software is free. Commercial use is not and requires that you obtain a commercial use license from DivXNetworks.’ (Refer to the DivX web site, www.divx.com, for information on DivX licensing.)
- Because MPEG-2 and MPEG-4 video formats are covered by a variety of patents, groups of patent holders have joined together to charge licensing fees for related encoders and decoders. These efforts are not sponsored by standards organizations that spearheaded the creation of those formats and may not cover every patent holder related to the software you are paying for. See the MPEG Industry Forum for details on MPEG patent issues (www.m4if.org/patents).
- Remember that there are now ways to purchase codecs for many popular audio/video formats for use with Linux. See the section “Extending Freedom to Codecs” for information on purchasing codecs from Fluendo.
- Unauthorized copying of copyright-protected material is never legal. Even legal video codecs do not make it legal to copy commercial movies and other protected content and distribute them to others. There are questions as to whether or not, for example, it is legal to make a personal backup copy of a DVD movie (a commonly accepted legal practice with computer software). But any re-distribution of movie, music, or other media content is not legal without the owner’s permission.

Because patenting eliminates trade secret protection for the subject matter disclosed in the patent (or published patent application), many people have raised the question of why someone can’t freely distribute libdvdcss (based on DeCSS decryption) to play DVD movies. Without copyright or patent coverage on CSS, it should not be illegal to distribute libdvdcss, and there’s nobody to pay a license fee to for using it. In regard to libdvdcss, another issue arose in the United States: the Digital Millennium Copyright Act (DMCA). DMCA might make DeCSS illegal because the technology is used to break an encryption scheme to circumvent copyrighted material.

As for the software patent issues, those are being fought on several fronts besides those relating to multimedia content. As noted earlier, the contention held by many Open Source proponents is that software should be copyrighted and not patented (see the section “Understanding Multimedia and Legal Issues in Linux” earlier in this chapter).

With all that said, the next parts of this chapter go on to describe which players are available to play a wide range of video content in Linux. It is up to you to work out the maze of which codecs are free for you to use and in what ways.

### Understanding Video Content Types

Before launching into the video players themselves, I want to try to clear up a bit of confusion relating to video file formats and codecs:

- **Video File Formats**— A video file format essentially describes the structure of a video file for combining audio and video content. That structure can also define such things as subtitles and how audio and video are synchronized. However, a variety of video and audio codecs may have been used to encode that content. So, just because you can play
