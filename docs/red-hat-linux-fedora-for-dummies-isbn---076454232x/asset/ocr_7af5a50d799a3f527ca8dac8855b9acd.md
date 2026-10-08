+   MPEG-1/Layer 3 (MP3): MP3 is a popular but proprietary codec used for both storing and streaming audio.

Ogg/Vorbis: This new up-and-coming open source streaming format is unencumbered by any copyrights or patents, like other formats are.

Microsoft Media Server (MMS): You can listen to radio broadcasts that use the popular MMS format with MPlayer. Previously, you needed to use the Microsoft client to listen to MMS streams.

Digital Versatile Disc (DVD): You can play DVDs from your computer with MPlayer.

RealAudio: You need to download, compile, and install the RTSP package to use RealAudio.

MPlayer is not now included in the Red Hat Linux distribution. We hope that it will be later, but for now you have to obtain it from its developers. These steps describe how to download, install, and use MPlayer:

+   1. Log in, open Mozilla, and go to `www.mplayerhq.hu/homepage/download.html`.
2. Click the latest Red Hat RPM version.
At the time this book was written, the latest Red Hat RPMS was found in the MPlayer Red Hat 7.x RPM packages. The 7.x packages work on Red Hat 10 systems.
3. Download each of these packages:
`mplayer`
`mplayer-common`
`mplayer-gui`
`mplayer-skins`
and this font package:
`MPlayerISO-885901-font`
At the time this edition of the book was written, the most recent MPlayer RPM package was version 0.92. You may see — and should use — the most recent version available.
4. Open a GNOME Terminal window and change to root:
`su -`
Enter the root password when prompted.
5. Install the package:
`rpm -ivh --nodeps mplayer*`