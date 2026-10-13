
## Viewing MPEG Video Files

FreeBSD has a number of tools available in the ports that can read MPEG video files; MPEG represents a fairly large proportion of the video content that's available on the Internet today and because it's an open standard with freely available codecs (unlike Windows Media Player and older versions of QuickTime), shareware tools that can read MPEG files are plentiful.

Probably the best bet for viewing most modern MPEG files is mpeg2play, which is available in the ports at /usr/ports/graphics/mpeg2play. This utility, which runs (naturally) under X, will play back both the MPEG-1 files that one usually finds online and MPEG-2 files which can be extracted (though usually illegally) from DVD discs.

Running mpeg2play is fairly self-explanatory; simply feed it the name of a file to play:

```
# mpeg2play myfile.mpg
```

This will open the movie in a new window in your desktop environment, with controls available in another window.

The mpeg2play port is rather old, however, and has not been updated in some time. Look in /usr/ports/graphics for other tools with mpeg in their names; new MPEG playback utilities might become available with time.

## DivX Video Files

Possibly the most common format on the Internet today for the openly traded video content that makes up most file-sharing traffic is DivX. This codec, usually embedded in Windows AVI files, is based on the emerging MPEG-4 standard and offers very good compression rates while preserving good quality. The codec is developed by volunteers whose Web site is at http://www.divx.com.

To play back DivX content, you will need to install linux-divxplayer. This program is available in the ports in /usr/ports/graphics/linux-divxplayer. It operates using FreeBSD's built-in Linux compatibility mode; although programs written for Linux usually pose no problems to FreeBSD, some applications that are heavy on graphics, sound, or other intensive device manipulation—which indeed describes DivX video—might cause some instability. Be aware that this might be the case, particularly considering that at the time of this writing, the version of linux-divxplayer is only 2.0.1!

After installing the linux-divxplayer port, which will install a few related dependency ports, you will be able to open DivX AVI files as follows:

```
# divxPlayer myfile.avi
```

Enjoy!

## Playing DVDs

It used to be only a pipe dream that users could watch DVD video discs under Linux or FreeBSD; however, this is no longer the case, thanks to the developers of a program called Ogle.

The first thing you need in order to run Ogle, naturally, is a DVD drive. FreeBSD will recognize most common IDE/ATA DVD drives as /dev/acd0, just as with regular CD-ROM drives.

Armed with this equipment, all you should need to do is install the Ogle port, which includes its GUI, available at /usr/ports/graphics/ogle-gui. (This port implicitly installs the command-line /usr/ports/graphics/ogle port.) Once this is done, type ogle to start up the Ogle GUI.

With the DVD you want to watch in the drive, use the menu command Open to open the device /dev/acd0. (You can also use the Open dialog to open the contents of a VIDEO_TS folder, if you have copied the contents of a DVD to your hard drive, by specifying /path/to/VIDEO_TS as the target.) You might also be able to use the Open Disc menu command, which will automatically open the DVD in the drive without your having to specify the device name.

Ogle has many features that you are probably accustomed to using in standard DVD players, including menus, full-screen mode, title/chapter search, and a number of high-quality audio formats. However, a few features are missing at this time, such as the ability to seek back and forth through the video with a slider, and reverse playback. Ogle will undoubtedly continue to evolve however; and in the meantime, the basics ought to work quite well.

## Summary

In this hour, you learned how to configure sound support in FreeBSD by adding the pcm device driver to the kernel, and also creating device nodes for sound support. We then looked at a small sample of the sound applications available for FreeBSD.

Multimedia hardly stops with sound playback, however; and so we looked at the basics of CD burning, MPEG and DivX video playback, and DVD playback—all features that are central to multimedia as we are accustomed to it today.

## Q&A

**Q** FreeBSD doesn't support my sound card. What can I do?

**A** All may not be lost. There is a third-party vendor that makes sound drivers for FreeBSD. You can check them out at `www.opensound.com`. These sound drivers support more cards than the native FreeBSD drivers. The drivers are not free, but the cost might be worth it if they are the only way you can get sound support working in FreeBSD.

**Q** I have a SCSI CD burner. The burncd utility doesn't seem to work.

**A** That's because SCSI drives need to use the `cdrrecord` utility, not `burncd`. Install it from `/usr/ports/sysutils/cdtools`; then, refer to the man `cdrrecord` page for details on using it, or refer back to Hour 8 when we discussed it in the context of storage systems.

**Q** MPEG video files don't seem to have any sound, or the sound behaves very oddly.

**A** MPEG is rather odd, as a format, in that its video and audio tracks are “multiplexed”—they don't exist as separate tracks, but instead are woven together in a way that often confounds playback software. You might try the `splitmpg` port (`/usr/ports/graphics/splitmpg`) to separate out the audio and video tracks, and then play them back through separate utilities at the same time. This can have very odd results, though, such as the audio and video playing back at slightly different speeds.

**Q** Ogle crashed my machine!

**A** DVD playback is a very device-intensive process; support for DVD drives is still quite new in FreeBSD, and there is bound to be some instability as complete functionality for playing back DVD content is integrated into the system. Keep an eye on the FreeBSD mailing list (such as `freebsd-stable` or `freebsd-current`, either of which you can subscribe to by sending a message to `majordomo@freebsd.org`), and watch for others posting questions or reporting similar problems. The more people who use FreeBSD to watch DVDs, the more pressure there will be on the developers to make it stable.

**Q** My DVD of The Matrix won't play properly.

**A** This is to be expected; certain DVDs won't even play properly in many hardware DVD players! As Ogle continues to develop, it will likely support more and more advanced playback features. As it is, however, your best bet is to trust it only with the more bare-bones DVDs in your collection.

## Workshop

In this interactive section, we will test your understanding of multimedia in FreeBSD with quiz questions and exercises designed to pique your curiosity about what else can be discovered within this hour’s topic.

### Quiz

- 1. The line that needs to be added to the kernel configuration file for sound support is
- A. `device sound`
- B. `device snd`
- C. `device pcm`
- D. None of the above
- 2. The command to create the sound device nodes is
- A. `./MAKEDEV snd`
- B. `./MAKEDEV snd0`
- C. `./MAKEDEV pcm`
- D. `./MAKEDEV sound`
- 3. The utility you need in order to create an ISO disk image to burn onto a data or MP3 CD is what?
- A. `burncd`
- B. `cdrecord`
- C. `mkisofs`
- D. Ogle
- 4. If you have an IDE/ATA CD-R or CD-RW drive, what tool will you use to burn CDs?
- A. `cdrecord`
- B. `mkisofs`
- C. XMMS
- D. `burncd`
- 5. How much data can you typically fit onto a CD-R?
- A. 650MB
- B. 4.7GB
- C. 700MB
- D. 250MB
- 6. What's the device name for a typical DVD-ROM drive in FreeBSD?
- A. /dev/acd0
- B. /dev/dvd0
- C. /dev/dvd
- D. /cdrom/cdrom0

### Quiz Answers

- 1. The correct answer is C.
- 2. The correct answer is B.
- 3. The correct answer is C.
- 4. The correct answer is D.
- 5. Either A or C is correct.
- 6. The correct answer is A. C is typically the answer for Linux.

### Exercises

- 1. MPEG-4 is likely to be the wave of the future when it comes to open video formats widely traded on the Internet. Research which utilities you might use in FreeBSD to play back MPEG-4 content, and also see if you can discover which tools available for other platforms can create MPEG-4 files. Knowing what most of the world will likely be using ought to help you keep prepared with your own system.
- 2. Experiment with Ogle, using the command-line version of the program; for instance, you can start Ogle with the `ogle -u cli /dev/acd0` command rather than going through the graphical menu. See the Ogle Web site for further details and documentation, at http://www.dtek.chalmers.se/groups/dvd/.
- 3. Determine what steps are necessary for creating either standard audio CDs or MP3 data CDs; try writing a script, in shell or Perl, that lets you select audio files from a list until their combined size would be too large to fit on a CD. Then, have the script burn the CD using the appropriate commands, as we have discussed in this hour's lesson.
