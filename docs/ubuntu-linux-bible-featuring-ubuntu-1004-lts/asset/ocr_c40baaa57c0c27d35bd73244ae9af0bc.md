# Part II: Ubuntu for Desktop Users

Traditionally, the most common sound server on GNOME-based systems has been ESD (Enlightened Sound Daemon, also called EsounD; www.tux.org/~ridcute/overview.html). Since Ubuntu 8.04 (and in most other up-to-date GNOME-based Linux distributions), ESD has been replaced by PulseAudio (www.pulseaudio.org), although the transition was not necessarily smooth one. Don't worry —subsequent sections discuss PulseAudio in more detail, but in my experience "it works" on current Ubuntu systems.

Just keep things confusing and infinitely flexible, other system-independent sound servers, such as the JACK Audio Connection Kit (www.jackaudio.org) and NAS (Network Audio System; www.radscan.com/nas.html), are also available and have been around for a while.

# Linux Multimedia Frameworks

GStreamer (www.gst.net) is a pipeline-based multimedia framework that can be used by applications to process the data as it is read from ALSA drivers and before it is output, either directly or through a sound server. "Pipeline-based" means that GStreamer processes audio by passing it through a sequence, or pipeline, of multiple conversion steps. GStreamer uses a plug-based architecture that makes it easy to extend GStreamer to support new audio or video formats. Originally developed for use on GNOME-based systems, GStreamer was designed to be platform-independent and is thus used on platforms that include Linux, Mac OS X, Microsoft Windows, and Solaris.

Some multimedia applications provide their own multimedia frameworks, which are therefore highly portable to other platforms and can often be accessed by other applications. Good examples of this are the MPlayer Movie Player (www.mplayer.hu), VLC Media Player (videolan.org/vlc), and the xine Multimedia Player (http://www.xine-project.org).

# What Should You Care About?

Having learned all of these acronyms, how do they affect you?

+   * If you simply want to play audio on your Ubuntu system, all you really need is ALSA (which is installed by default on Ubuntu systems).
* Ubuntu users who want to play MP3 files or watch DVDs, or who might ever encounter an audio or video format that is not open source, should install GStreamer plugin-ins to expand the core GStreamer capabilities that are present on your system.
* If you need networked sound or want to be separately control the audio levels of different audio applications, you should also take advantage of PulseAudio on Ubuntu systems (which is installed by default).