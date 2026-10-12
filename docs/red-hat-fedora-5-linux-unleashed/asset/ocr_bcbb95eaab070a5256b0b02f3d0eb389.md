proprietary, but free codecs do exist. Here is a list of the most common video formats and their associated file extensions:

+   - `.mpg`—The MPEG video format; also known as `.mpg`
+   - `.qt`—The QuickTime video format from Apple
+   - `.mov`—Another QuickTime video format
+   - `.avi`—The Windows audio visual format

> An RPM that provides a Divx codec for Linux can be found at http://www.freshrpms.net/. Divx is a patented MPEG-4 video coder that is the most widely used codec of its type. It allows for compression of MPEG-2 video by a factor of 8. See http://www.divx.com/ for more information.
> 
> The Getcodecs application is a Python script with a GUI interface that downloads, installs, and configures your Fedora system with multimedia codecs not provided by Fedora, such as MP3, Divx, and DVD codecs. The script can be obtained from http://sourceforge.net/projects/getcodecs/

If you need to convert video from one format to another, you use encoder applications called grabbers. These applications take raw video data from a video device such as a camera or TV card, and convert it to one of the standard MPEG formats or to a still image format, such as JPEG or GIF. Fedora does not supply any encoder applications (other than gptopampg which encodes MPEG-1 video), but you can find them at http://www.freshrpms.net/ or another online source (see the "Reference" section at the end of this chapter).

# ## Viewing Video in Linux

Because of the patent and licensing issues mentioned earlier, the capability to play video files has been removed from Fedora. This functionality can be restored if you install the full version of the applications described in this section from FreshRPMs at http://www.freshrpms.net/. There you can find multimedia applications such as OgIe, Xine, AlsaPlayer, Gstreamer, Grip, Mplayer, VCDImager, VideoLAN-client, Xmmx, and Zapping.

You can use Linux software to watch TV, save individual images (take snapshots) from a televised broadcast, save a series of snapshots to build animation sequences, or capture video, audio, or both. The following sections describe some of the ways in which you can put Linux multimedia software to work for you.

The naatun viewer is provided with Fedora to use as an embedded viewer in the Konqueror browser. naatun is set up as the default association for the video file formats it plays. Open a video file in Konqueror or Nautilus, and the video is shown in the viewer it is supported. The viewer provides basic start, stop, and fast-forward VCR-type functions.