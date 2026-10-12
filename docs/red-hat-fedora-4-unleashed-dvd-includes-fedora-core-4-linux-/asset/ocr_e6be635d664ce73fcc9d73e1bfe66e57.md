All we need do is enter this information into `/etc/modules.conf` and change the value for `card=2` to `card=64` to match our hardware. We can delete the reference to the radio card (`radio=2`) because we do not have one and leave the other values alone. Then we must execute

```
# depmod -a
```

to rebuild the modules dependency list so that all our modules are loaded automatically. When finished, all we need do is execute

```
# modprobe bttv
```

and our TV card should be fully functional. All the correct modules will be automatically loaded every time we reboot. Fedora is clever enough to detect and configure a supported TV card that is present during installation.

> **TIP**
> 
> Other useful documentation can be found in `/usr/src/linux-2.6/Documentation/_video4linux`. After you have identified a driver for a device, it will not hurt to look at the source code for it because so little formal documentation exists for many drivers; much of it is in the source code comments.

The development of support for TV cards in Linux has coalesced under the Video4Linux project. The Video4Linux software provides support for video capture, radio, and Teletext devices in Fedora Core.

# Video Formats

Fedora recognizes a variety of video formats. The formats created by the MPEG group, Apple, and Microsoft dominate, however. At the heart of video formats are the *codecs*—the encoders and decoders of the video and audio information. These codecs are typically proprietary, but free codecs do exist. Here is a list of the most common video formats and their associated file extensions:

+   - `.mpeG`—The MPEG video format; also known as `.mpg`
+   - `.qt`—The QuickTime video format from Apple
+   - `.mov`—Another QuickTime video format
+   - `.avi`—The Windows audio visual format

> **TIP**
> 
> An RPM that provides a DivX codec for Linux can be found at `http://www.freshrpms.net/`. DivX is a patented MPEG-4 video codec that is the most widely used codec of its type. It allows for compression of MPEG-2 video by a factor of 8. See `http://www.divx.com/` for more information.