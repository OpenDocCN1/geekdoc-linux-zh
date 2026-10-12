# Sound Cards

Fedora supports a wide variety of sound hardware and software. Two models of sound card drivers compete for prominence in today’s market:

+   * ALSA, the Advanced Linux Sound Architecture, which is entirely open source
+   * OSS, the Open Sound System, which offers free and commercial drivers

Fedora uses ALSA because ALSA is the sound architecture for the 2.6 series kernels.
ALSA supports a long list of sound cards. You can review the list at http://www.alsa-project.org/alsa-doc/. If your sound card is not supported, it might be supported in the commercial version of OSS. You can download a trial version of commercial software and test your sound card at http://www.opensound.com/download.cgi.

Fedora detects most sound cards during the original installation. If you add or replace a sound card after the initial install, the *Kudzu New Hardware Configuration* utility automatically detects and configures it at the next reboot. To configure the sound card at any other time, use the *system-config-soundcard* graphical tool. The graphical tool can be found under the Administration menu as the Soundcard Detection menu item. For additional details about configuring your sound card, refer to Chapter 4.

# Recording Sound

Fedora provides a number of tools that enable you to control volume, mix, and other sound recording functions. The *Kmix* sound mixer (available when you install the KDE window manager) acts as a virtual mixing board, taking sound inputs from different sources, enabling you to adjust their individual volumes, mute them, and listen to them through your sound card.

If you need to control sound from the command line, use the *alsamixer* command, which can be used to adjust balance or volume in text mode using the left and right cursor keys to select a channel and the up and down keys to adjust the volume.

```
$ alsamixer
```

# Sound Formats

A number of formats exist for storing sound recordings. Some of these formats are associated with specific technologies, and others are used strictly for proprietary reasons. Fedora supports several of the most popular sound formats, including

+   * raw (*.raw*)—More properly known as *headerless format*, audio files using this format contain an amorphous variety of specific settings and encodings. All other sound files contain a short section of code at the beginning—a header—that identifies the format type.