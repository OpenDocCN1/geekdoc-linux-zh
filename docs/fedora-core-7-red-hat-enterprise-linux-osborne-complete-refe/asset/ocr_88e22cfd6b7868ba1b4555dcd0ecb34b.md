plug-ins. You can find out more information about GStreamer and its supporting packages at **gstreamer.freedesktop.org**.

You can obtain additional GStreamer plug-in and supporting packages from either **Livna** or **Freshrpms**.

The current version of GStreamer is 1.0. The supporting packages can be confusing. For version 1.0, GStreamer establishes four different support packages called the base, the good, the bad, and the ugly. The **base** package is a set of useful plug-ins that are reliable. The **good** package is a set of supported and tested plug-ins that meet all licensing requirements. Both the base and good packages are part of the Fedora repository and are installed by default. The **bad** is a set of unsupported plug-ins whose performance is not guaranteed and may crash, but still meets licensing requirements. The **ugly** package contains plug-ins that work fine but may not meet licensing requirements, such as for DVD support. These you will find on Freshrpms or GStreamer repositories.

+   * **The base** Reliable, commonly used plug-ins (Fedora repository)
* **The good** Additional reliable and useful plug-ins (Fedora repository)
* **The ugly** Reliable but not fully licensed plug-ins (DVD/MP3 support)
* **The bad** Possibly unreliable but useful plug-ins (possible crashes)

To download and install the GStreamer plug-in packages, just search for **gstreamer** on Add/Remove Software (Pirut). If you have enabled either Livna or Freshrpms repositories, you will also see entries for the ugly and bad packages. Alternatively, you could use the following Yum command to install all plug-ins at once. Be sure to include the asterisk to match on all the plug-in packages. Your architecture (i586, i686, or x86_64) will automatically be detected.

```
yum install gstreamer-plugins*
```

Other plug-ins for GStreamer 1.0 that you may want to include are **ffmpeg** and **pitfdll**, **gstreamer-ffmpeg**, and **gstreamer-pitfdll**. **ffmpeg** provides several popular codecs, including Ogg and .264. The **pitfdll** package provides support for media files in proprietary formats like Microsoft's WM9.

# ### MPlayer

MPlayer is a very popular multimedia player. You can find out more about MPlayer at **www.mplayerhq.hu**. If this is your first multimedia package, numerous supporting packages will be selected. Assuming the configuration for a repository that carries MPlayer has been installed, you can then use Pirut or the **yum** command to select, download, and install MPlayer. For more details, check the MPlayer documentation.

If all goes well, MPlayer will be installed with an entry in your Applications | Sound And Video menu.

To install MPlayer from the command line, just enter

```
yum install mplayer
```

Yum will then retrieve the needed packages, including a long list of dependent packages.