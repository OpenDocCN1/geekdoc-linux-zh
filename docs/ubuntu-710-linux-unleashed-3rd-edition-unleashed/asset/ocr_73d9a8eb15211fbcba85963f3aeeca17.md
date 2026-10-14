The development of support for TV cards in Linux has coalesced under the Video4Linux project. The Video4Linux software provides support for video capture, radio, and teletext devices in Ubuntu.

# Video Formats

Ubuntu recognizes a variety of video formats. The formats created by the MPEG group, Apple, and Microsoft dominate, however. At the heart of video formats are the codecs—the encoders and decoders of the video and audio information. These codecs are typically proprietary, but free codecs do exist. Here is a list of the most common video formats and their associated file extensions:

+   - `.mpeg`—The MPEG video format; also known as `.mpg`
+   - `.qt`—The QuickTime video format from Apple
+   - `.mov`—Another QuickTime video format
+   - `.avi`—The Windows audio visual format

TIP

An RPM that provides a DivX codec for Linux can be found at http://www.freshrpms.net/. Divx is a patented MPEG-4 video codec that is the most widely used codec of its type. It allows for compression of MPEG-2 video by a factor of 8. See http://www.divx.com/ for more information.

The GetCodecs application is a Python script with a GUI interface that downloads, installs, and configures your Ubuntu system with multimedia codecs not provided by Ubuntu, such as MP3, Divx, and DVD codecs. The script can be obtained from http://sourceforge.net/projects/getcodecs/.

If you need to convert video from one format to another, you use encoder applications called *grubbers*. These applications take raw video data from a video device such as a camera or TV card, and convert it to one of the standard MPEG formats or to a still image format, such as JPEG or GIF. Ubuntu does not supply any encoder applications (other than `pptm mpeg`, which encodes MPEG-1 video), but you can find them at http://www.freshrpms.net/ or another online source (see the “Reference” section at the end of this chapter).

# Viewing Video in Linux

Out of the box, Ubuntu does not support any of the proprietary video codecs due to licensing restrictions. However this functionality can be restored if you install the full version of the applications described in this section from the Universe repository. There you can find multimedia applications such as Ogle, Xine, AslaPlayer, Gstreamer, Grip, Mplayer, VCDImager, VideoLAN-client, Xmms, and Zapping.