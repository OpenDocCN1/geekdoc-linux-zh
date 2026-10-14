in Ubuntu because of licensing concerns. Even if you plan on using the Ogg Vorbis format in your future ripping and encoding endeavors, installing MP3 support is a good idea so as to cover all your audio bases. It’s also a very easy process.

The easiest way to install MP3 playback support is to double-click an MP3 file that you have on your hard disk. A window will appear, asking whether you want to search for the plug-ins necessary to play the file. Click Search, after which another window will appear, showing you what you need to install (Figure 14-1). Check both boxes in that window, click the Install button, and in the confirmation window that then appears, click Confirm. You will then be asked for your password, so provide it, and then just wait until the process is complete. Once done, you’ll be able to play not only your MP3 audio files but also MPEG and WMV videos.

![](bbox=[0.22, 0.36, 0.78, 0.72])

Figure 14-1: Ubuntu helps you find the plug-ins you need.

If you prefer, you can download and install these plug-ins quite easily via the Ubuntu Software Center by doing a search for gstreamer and then installing gstreamer0.10-ffmpeg (GStreamer ffmpeg video plugin), gstreamer0.10-fluendo-mp3 (Fluendo mp3 decoder GStreamer plugin), and gstreamer0.10-plugins-ugly (GStreamer extra plugins).

As for MP3 encoding support, which enables you to rip CDs and create your own space-saving MP3 files, well, things aren’t so automatic. But it’s not much of a chore, either, because all you need to do is use the Ubuntu Software Center to search for and install gstreamer0.10-plugins-ugly-multiverse. If you also want to give yourself AAC encoding ability, you should install gstreamer0.10-plugins-bad-multiverse as well. You will then be ready for action, as described in the next section.