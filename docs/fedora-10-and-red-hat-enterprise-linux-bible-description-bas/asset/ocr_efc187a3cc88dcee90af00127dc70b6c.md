# Part II: Using Fedora and RHEL

+   Xine won't play particular media. Messages such as no input plug-in mean that the format you are trying to play is not supported or it requires an additional plug-in (as is the case with playing DVDs). If the message is maybe xyx is a broken file, the file may a proprietary version of an otherwise supported format. For example, I had a QuickTime video that failed to SVQ3 codec (which is currently not supported under Linux), although other QuickTime files will play fine.

If a particular media is not supported, but you have Windows dls available to support it, you can add dls files to the /usr/lib/win32 directory. Some of these codec dls are available from
http://www.mplayer.org/design/7/dload.html#binary_codecs in a package called essential. Choose a chooser from the table under the Binary Codec Packages heading.

> NOTE: The CrossOver Plugin (described in Chapter 9) can be used to play a variety of content, including the version of QuickTime just mentioned.

# Using Totem movie player

The Totem movie player (http://www.gnome.org/projects/totem) comes with the GNOME desktop environment. In Fedora and RHEL, Totem can play video in Theora format with Ogg Vorbis audio. Totem is based on GStreamer (http://gstreamer.freedesktop.org) so it can be used with other video software from that project. In particular, free and fee-based codecs that you can purchase from http://www.fluendo.com for playing a variety of commercial audio/video formats will work with Totem.

Totem also supports a xine backend that allows it to play a wide range of video content (in other words, anything xine supports). To play commercial DVD movies, however, you need to replace the version of Totem that comes with Fedora and the totem-xine package available from Livna.org. From that repository, you can add the libdvdcs, libdvdnav, and xine-lib-extras-nonfree packages (provided the software is legal where you are).

Besides common controls you would expect with a movie player (play, pause, skip forward, backwards, and so on), Totem lets you create playlists, take a snapshot of the current frame, and adjust the volume. You can change preferences, which let you add proprietary plug-ins, select your DVD device, and balance color. Figure 8-13 shows an example of the Totem window.