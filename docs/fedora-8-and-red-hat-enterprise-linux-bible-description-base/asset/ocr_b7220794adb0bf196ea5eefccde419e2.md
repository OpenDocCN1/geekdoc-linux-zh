automatically from a CD database (such as freedb.org). Or, if your CD isn't listed in the database, you can enter your own track information manually.

+   **KsCD Player (kscd)** — The KsCD player comes from the KDE desktop. To use KsCD, the kdemultimedia package must be installed. From the Applications menu (KDE desktop), select Sound & Video → KsCD (or type kscd from a Terminal window). Like gnome-cd, this player lets you get title, track, and artist information from the CD database, and lets you submit information you type in yourself to a CD database (if your CD isn't found there).

+   **Rhythmbox (rhythmbox)** — Import and manage your music collection with Rhythmbox music management and playback software for GNOME. Rhythmbox uses GStreamer and Sound Juicer to extract music from a CD, and then compresses that music using Ogg Vorbis, FLAC, or a low-quality WAV (for speech) audio format. Besides allowing you to create playlists of your music library, Rhythmbox also has features for playing Internet radio stations. Open Rhythmbox from the Applications menu by selecting Sound & Video → Music Player.

+   **XMMS (xmms)** — The X Multimedia System (XMMS) audio player provides a simple, graphical player for playing Ogg Vorbis, WAV, FLAC, and other audio formats. XMMS has a fairly simple Windows winamp-like look and feel, which you can adjust using a few dozen skins. (The xmms package is available in the Fedora repository. To add CD playing support to xmms, install the xmms-cdread package as well.)

+   **ogg123, mpg321, aplay, or play** — If you don't have access to the desktop, you can use the text-based ogg123, mpg321, or play commands. The ogg123 command comes with the vorbis-tools package, aplay is part of the alsa-utils package, and play comes with the sox package in Fedora and RHEL. The mpg321 command comes in the mpg321 package, which is available from the Livna.org RPMs site. (The mpg321 command is covered under the GPL. There is an mpg123 project, which is no longer maintained and is not fully covered under the GPL.)

The default CD audio player is Totem (totem command) for the current release. Totem is primarily a video player, so you might want to change the default to some other player that includes CDDB support and other CD-playing features. You can do that with the Removable Drives and Media window, as described in detail in the next section.

> **NOTE:** If you try some of these CD players and your CD-ROM drive is not working, see the sidebar "Troubleshooting Your CD-ROM" for further information.

# ## Automatically playing CDs

When you put an audio CD into your CD-ROM drive, a media player (totem) automatically pops up on your desktop and begins playing the CD. If you are using the GNOME desktop, you can thank the GNOME Volume Manager. The GNOME Volume Manager monitors your