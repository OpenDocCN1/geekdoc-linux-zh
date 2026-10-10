This shows that both 32-bit IO and DMA are off. To turn them on, type:

```
# hdparm -c 1 -d 1 /dev/sda
/dev/sda:
  I/O support    = 1 (32-bit)
  using_dma      = 1 (on)
```

If you have problems with the DMA setting, run the command without the -d 1 option. Now, test the disk again:

```
# hdparm -t /dev/sda
Timing buffered disk reads: 64 MB in  2.2 seconds = 28.83 MB/sec
```

As you can see from this example, buffered disk reads of 64MB went from 19.31 seconds to 2.2 seconds after changing the parameters described. Playback should be much better now.

+   * **Xine won't play particular media.** Messages such as *no input plug-in* mean that either the file format you are trying to play is not supported or it requires an additional plug-in (as is the case with playing DVDs). If the message is *maybe yvx is a broken file*, the file may be a proprietary version of an otherwise supported format. For example, I had a QuickTime video fail that required an SVQ3 codec (which is currently not supported under Linux), although other QuickTime files will play fine.

If a particular multimedia format is not supported, but you have Windows Dynamic Link Libraries, or DLLs, available that support it, you can add those DLL files to the /usr/lib/win32 directory. Some of these codec DLLs are available from http://www.mplayerhq.hu/design7/dload.html#binary_codecs in a package called *essential*. Choose a mirror site from the table under the Binary Codec Packages heading.

> **NOTE:** The CrossOver PlugIn (described in Chapter 8) can be used to play a variety of content, including the version of QuickTime just mentioned.

# ## Using Totem movie player

The Totem movie player (http://www.gnome.org/projects/totem/) comes with the GNOME desktop environment. In Fedora, Totem can play video in Theora format with Vorbis audio. Totem is based on GStreamer (http://gstreamer.freedesktop.org) so it can be used with other video software from that project. In particular, free and fee-based codecs that you can purchase from http://www.fluendo.com for playing a variety of commercial audio/video formats will work with Totem.

Totem also supports a xine backend that allows it to play a wide range of video content (in other words, anything xine supports). To play commercial DVD movies you will need to install the gstreamer-plugins-ugly package from the rpmfusion.org repository and the libdvcs package from the livna.org repository.