
gThumb also has the ability to work with individual images via functions in the Image menu. You can rotate an image to the left or right, flip (spin on a horizontal axis) or mirror (spin on a vertical axis), resize, and change the color, hue, and brightness/contrast attributes, just to name a few.

You can also convert images from one format to another with the Tools | Convert Format menu option, which opens the Convert Format dialog, shown in **Figure 33**.

The Convert Format function has a lot of versatility, in that it not only provides for converting between four popular formats, but also offers several options for what to do with the original file.

![](img/50a238d93c7edbdc4387d5ff7f6b7b3c_275_0.png)

**Figure 32.** Adding a custom category to gThumb Image Viewer.

![](img/50a238d93c7edbdc4387d5ff7f6b7b3c_275_1.png)

**Figure 33.** The Convert Format function allows you to convert an image to another format and then decide what to do with the original file.

## Summary

Digital imagery is an area that continues to get more popular. The advances in hardware are part of the reason: Digital, pocket-size cameras are rapidly approaching the quality of silver halide film, and the computer processing power needed to handle the huge amounts of data required continues to grow. The other part of the picture is increasingly sophisticated and powerful software. I’ve just touched on the possibilities here, but as you’ve seen, a Linux desktop can more than hold its own in this area.

The purpose of this chapter is to get you started with Linux on your desktop, but of course there’s a lot more than what I can cover here. In addition, new versions of Fedora Core are released on a regular basis. I’ll keep you up to date by writing new articles as well as posting updates related to this book. These materials can be found on Hentznerwerke’s Web site, [www.hentznerwerke.com](http://www.hentznerwerke.com). Click “Catalog” and navigate to the page for *Linux Transfer for Windows Power Users*.

# Chapter 11

## Multimedia: Audio (and Video)

The classic examples of multimedia applications are listening to music (audio) and watching movies (video). Multimedia, unlike other popular end-user applications like word processing, spreadsheets, and e-mail, puts a strain on hardware and requires software that’s more sophisticated and powerful than a simple office suite or Web browser. As a result, Linux hasn’t always kept up with Windows in this arena. In this chapter, I’ll explore what a power user can do with multimedia today.

The media has been abuzz over the last year about how Hollywood is moving toward Linux in a big way: Every month brings another report about how a major studio or project has moved to a farm of off-the-shelf Linux machines to replace their previous (that’s spelled “expensive”) workstations for digital media. Indeed, 2003 saw animation studios such as Pixar, Industrial Light and Magic, and Dreamworks all move to Intel-based computers running Linux. However, these installations aren’t for the faint-hearted; for example, the Pixar move involved eight blade servers containing 1024 2.8 GHz Xeon processors. In many cases, bucketloads of custom software are also involved.

This detail—the level of sophistication involved in these moves—is sometimes overlooked in the enthusiasm of those reporting the stories, and thus leads to unrealistic expectations on the part of regular computer users.

Deploying multimedia functions on the Linux desktop is still a mixed bag. Sound—listening to your favorite Led Zeppelin tune, downloading the latest Enya demo, or reminiscing to an ancient Firesign Theatre booleet that a friend just ripped for you—is ready for prime time no matter where you are. But video capabilities are erratic and immature. Between beta-quality software, competing formats, and inept digital rights management (or, as some refer to it, “digital restriction management”" techniques, it’s a tussle whether you’ll be able to properly play an MPEG of your cousin’s wedding in Fiji that he posted on his Web site before leaving on his honeymoon, or if the new Matrix Regurgulated DVD will display at all.

But we’re getting there. Remember, a couple of years ago, the experts all stated that Linux would never be usable on the desktop.

## Audio

Listening to music or other audio files is nearly a prerequisite with a computer these days; indeed, I haven’t played music on a stereo system in years. Naturally, you’ll want to be able to use audio on your Fedora Core system. Here’s what you have to do.

### Testing the sound card

The first thing you’ll want to do is make sure your sound card works and is recognized by Fedora Core. I’m making this sound like a bigger deal than it really is; normally you’ll do the sound-card detection during installation and won’t have any problems. If you skipped that step during installation, or if you’ve since changed your sound card and need to check it out again, here’s how.

Select Main Menu | System Settings | Soundcard Detection. You’ll be prompted for the root password, because you’re messing with the system in general, and not just your own settings. Once you enter the password, you’ll be greeted by the Audio Devices screen, shown in Figure 1.

![](img/50a238d93c7edbdc4387d5ff7f6b7b3c_279_0.png)

Figure 1. The Fedora Core Audio Devices dialog allows you to test your sound card.

If a physical device was found in the computer, it’ll be identified and you can click the “Play test sound” button to see if Fedora Core can send sounds through it. You should hear a tone in the right speaker, then a tone in the left speaker, and then a tone in both speakers at the same time.

Then you’ll be asked, “Did you hear the sample sound?”

If yes, you’re all set; if not, you’ll get a message that says, “Automatic detection of the sound card did not work. Audio will not be available on the system. Please click OK to continue.”

I’ve only had the sound-card detection fail on one machine in two years, and that was on an old, old box with a terribly antiquated sound card. I went to the local computer store and picked up a new Sound Blaster for $30 and all was good again.

### Playing a CD with CD Player

Playing a CD on Fedora Core is essentially a trivial process. Stick the CD into the CD-ROM drive, wait a few seconds for the drive to spin up, and the CD Player applet will appear, as shown in Figure 2.

![](img/50a238d93c7edbdc4387d5ff7f6b7b3c_279_1.png)

Figure 2. The CD Player applet that comes with Fedora Core.

If you've used a CD player or VCR before, you'll be able to understand the controls in short order. The CD-style controls at the bottom of the screen provide standard functionality: previous track, rewind, play/pause, stop, fast forward, next track, and eject. Above the controls are the **Track** Editor button, which opens the CDBB **Track** Editor screen shown in **Figure 3**; the **Preferences** button; and a drop-down combo box that allows you to select and play a specific track on the CD.

The slider above those three buttons is a progress bar that shows you how far through the song the player has moved. The slider in the upper right corner is the volume control, and the display screen shows you information about the current track.

If you forget any of these, you can noodle them again by moving your mouse over the control and reading the tooltip.

If you close CD Player while a CD is in the drive, you can open it again via Main Menu | Sound and Video | CD Player.

![](img/50a238d93c7edbdc4387d5ff7f6b7b3c_280_0.png)

*Figure 3. The CDBB Track Editor that's part of the CD Player.*

### Moving CDs to disk, so you can keep them with you

While some folks are content to pop CDs in and out of the drive, others prefer to copy the contents of their CDs to a hard disk. Doing so not only saves you from lugging a bunch of CDs around (I know some folks who have hundreds of CDs on a hard disk), but also saves wear and tear on the drive. Getting a track (I don't call them "songs" because all this applies to other types of digital audio, such as recordings of the Boston Pops and George Carlin comedy routines) from a CD to a hard disk is not simply a matter of copying a file from the CD, as it is with other types of data files.

Files on an audio CD are commonly stored in a format called CDDA, with an extension of CDA. If you view the contents of an audio CD, you'll see a list of files with names like Track01.cda, Track02.cda, and so forth, and the file size is typically 44 bytes. The rest of the
