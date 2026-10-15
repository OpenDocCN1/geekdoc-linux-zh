
![](img/e464b828c497c99e41f61d4c55f1c0db_240_0.png)

FIGURE 10.2 The simple to use, yet extremely powerful, GnomeBaker.

## X-CD-Roast

X-CD-Roast, shown in Figure 10.3, is a standalone CD and DVD creator provided with Ubuntu, but is not installed by default. When installed using synaptic, it can be found in the Sound and Video menu as X-CD-Roast, or it can be launched from the command line, like this:

```
$ xcdroast &
```

When you first start it, you will need to put sudo in front of the command so you can correctly configure X-CD-Roast. Once the first scan of the CD/DVD devices has been completed, it begins with a dialog warning you to enter the Setup dialog, which will be the only button presented to you in the next screen other than Exit. The application auto-detects your CD/DVD drive, but you must tell it which drive (if you have more than one) is the writing drive and select the users who are allowed to use the application. The dialogs for setting this information are straightforward and easy to follow. Make certain that you choose a default directory for temporary image storage that offers enough room to store several images.

## Serpentine

Serpentine (see Figure 10.5) is a tool that allows you to create your own Audio discs by either selecting audio files or by using playlists that you have created in Rhythmbox. It is limited in that it only allows you to create audio discs, but it is very straightforward to use. Just make sure that you are legally entitled to write any audio files to a CD!

![](img/e464b828c497c99e41f61d4c55f1c0db_242_0.png)

FIGURE 10.5   Create your own CD compilations using Serpentine.

## Sound and Music

Linux historically had a reputation of lacking good support for sound and multimedia applications in general. However, great strides have been made in recent years to correct this, and support is now a lot better than it used to be. (It might make you smile that Microsoft no longer supports the Microsoft Sound Card, but Linux users still enjoy support for it, no doubt just to annoy the folks in Redmond.) UNIX, however, has always had good multimedia support as David Taylor, UNIX author and guru, points out:

> > “The original graphics work for computers was done by Evans & Sutherland on Unix systems. The innovations at MIT’s Media Lab were done on Unix workstations. In 1985, we at HP Labs were creating sophisticated multimedia immersive work environments on Unix workstations, so maybe Unix is more multimedia than suggested. Limitations in Linux support doesn't mean Unix had the same limitations. I think it was more a matter of logistics, with hundreds of sound cards and thousands of different possible PC configurations.”

That last sentence sums it up quite well. UNIX had a limited range of hardware to support; Linux has hundreds of sound cards. Sound card device driver support has been long lacking from manufacturers, and there is still no single standard for the sound subsystem in Linux.

In this section, you learn about sound cards, sound file formats, and the sound applications provided with Ubuntu.

### Sound Cards

Ubuntu supports a wide variety of sound hardware and software. Two models of sound card drivers compete for prominence in today's market:

- ALSA, the Advanced Linux Sound Architecture, which is entirely open source
- OSS, the Open Sound System, which offers free and commercial drivers

Ubuntu uses ALSA because ALSA is the sound architecture for the 2.6 series kernels.

ALSA supports a long list of sound cards. You can review the list at http://www.alsa-project.org/alsa-doc/. If your sound card is not supported, it might be supported in the commercial version of OSS. You can download a trial version of commercial software and test your sound card at http://www.opensound.com/download.cgi.

Ubuntu detects most sound cards during the original installation. If you add or replace a sound card after the initial install, Ubuntu will automatically detect and configure it at the next reboot.

### Recording Sound

Ubuntu provides a number of tools that enable you to control volume, mix, and other sound recording functions. The Kmix sound mixer (available when you install the KDE window manager or Kubuntu) acts as a virtual mixing board, taking sound inputs from different sources, enabling you to adjust their individual volumes, mute them, and listen to them through your sound card.

If you need to control sound from command line, use the alsamixer command as seen in Figure 10.6, which can be used to adjust balance or volume in text mode using the left and right cursor keys to select a channel and the up and down keys to adjust the volume.

```
$ alsamixer
```

### Sound Formats

A number of formats exist for storing sound recordings. Some of these formats are associated with specific technologies, and others are used strictly for proprietary reasons. Ubuntu supports several of the most popular sound formats, including

- raw (.raw)—More properly known as headerless format, audio files using this format contain an amorphous variety of specific settings and encodings. All other sound files contain a short section of code at the beginning—a header—that identifies the format type.
