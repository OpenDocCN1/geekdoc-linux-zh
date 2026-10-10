# Music, Video, and Images in Linux

a video file that is marked as MPEG (mpg), Audio Video Interleaved (.avi), QuickTime (.mov), RealMedia (.rm), Windows media (.wvm), Advanced Streaming Format (.asf), or other file format, it doesn't mean that you can play all video files marked as such.

+   Video and Audio Coders — Coders are used to encode and decode video and audio content. A video encoded entirely with free software might use Theora to encode the video and Ogg Vorbis to encode the audio. Popular video coders include MPEG-4, DivX, Xvid, RealVideo, and MJPEG.

Not all video coders and file formats are suitable for streaming video. For example, AVI and MPEG-2 are not streamable. However, RealMedia, MPEG-4, and ASF format can be streamed, which reduces the load on a server and means you do not have to download an entire video to start watching. Check the descriptions of video players in the following sections for information on which players can support which coders.

If you have a video file on your hard disk and you'd like to know what type of content it contains, you can use the file command. Here's an example of the file command for checking the contents of a movie trailer:

```
```
$ file movie.avi
movie.avi: RIFF (little-endian) data, AVI, 640 x 272, 23.98 fps, video: DivX 3, audio: MPEG-1 Layer 3 (stereo, 44100 Hz)
```
```

This example shows that the file contains DivX 3 video and MPEG-1 Layer 3 audio. The size of the video is 640 x 272 pixels. Video was captured at 23.98 frames per second. This can lead you to the type of video player you need to play the content. Given that the right coders are installed, MPlayer, Xine, VLC, or several other players would be able to play this content.

# Converting Video to Theora

There are not yet many tools for creating Theora video. To get a video to try out, I shot a video with my Sony Handycam, which stores video in 30-minute, 1.4-GB mini-DVDS. I downloaded a tool recommended from the Theora.org site, called *ffmpeg2theora* ([www.v2v.cc/~/j/ffmpeg2theora](www.v2v.cc/~/j/ffmpeg2theora)). My video camera stored my home movie as a VOB file, which I copied to my hard disk and converted to Theora/Ogg Vorbis as follows:

```
```
$ ffmpeg2theora VTS_01_1.VOB
 Input #0, mpeg, from 'VTS_01_1.VOB':
   Duration: 00:00:00.6, start: 0.197311, bitrate: -2147483 kb/s
   Stream #0:0: Video: mpeg2video, 704x480, 29.97 fps, 9300 kb/s
   Stream #0:1: Audio: ac3, 48000 Hz, stereo, 256 kb/s
```
```