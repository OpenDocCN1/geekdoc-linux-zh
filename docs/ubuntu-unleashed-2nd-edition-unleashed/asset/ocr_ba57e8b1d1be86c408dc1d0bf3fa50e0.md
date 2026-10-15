long lacking from manufacturers, and there is still no single standard for the sound subsystem in Linux.

In this section, you learn about sound cards, sound file formats, and the sound applications provided with Ubuntu.

# Sound Cards

Ubuntu supports a wide variety of sound hardware and software. Two models of sound card drivers compete for prominence in today's market:

+   ALSA, the Advanced Linux Sound Architecture, which is entirely open source

+   OSS, the Open Sound System, which offers free and commercial drivers

Ubuntu uses ALSA because ALSA is the sound architecture for the 2.6 series kernels.

ALSA supports a long list of sound cards. You can review the list at http://www.alsa-project.org/alsa-doc/. If your sound card is not supported, it might be supported in the commercial version of OSS. You can download a trial version of commercial software and test your sound card at http://www.opensound.com/download.cgi.

Ubuntu detects most sound cards during the original installation. If you add or replace a sound card after the initial install, Ubuntu will automatically detect and configure it at the next reboot.

# Recording Sound

Ubuntu provides a number of tools that enable you to control volume, mix, and other sound recording functions. The Kmix sound mixer (available when you install the KDE window manager or Kubuntu) acts as a virtual mixing board, taking sound inputs from different sources, enabling you to adjust their individual volumes, mute them, and listen to them through your sound card.

If you need to control sound from command line, use the alsamixer command as seen in Figure 10.6, which can be used to adjust balance or volume in text mode using the left and right cursor keys to select a channel and the up and down keys to adjust the volume.

```
$ alsamixer
```

# Sound Formats

A number of formats exist for storing sound recordings. Some of these formats are associated with specific technologies, and others are used strictly for proprietary reasons. Ubuntu supports several of the most popular sound formats, including

+   raw (.raw)—More properly known as headerless format, audio files using this format contain an amorphous variety of specific settings and encodings. All other sound files contain a short section of code at the beginning—a header—that identifies the format type.