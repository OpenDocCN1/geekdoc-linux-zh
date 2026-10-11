
## Chapter 18

### If Music Be the Food of Love . . . (Ubuntu Linux Multimedia)

Playing music on your Linux system is only the beginning of the multimedia experience. After all, multimedia isn't just about music. It represents a cornucopia of sensory experience delivered digitally, comprised of text, audio, video, and endless combinations of the three.

Most modern Linux installations offer an impressive selection of programs to satisfy your cravings for the multimedia experience, from audio to video and everything in between. These programs include sound control systems, CD players, recorders, MIDI programs of varying flavors, music synthesizers, video players, music notation programs, and . . . the list goes on.

In this chapter, I'm going to cover some of the more popular multimedia tools for your Linux system. So, as old William Shakespeare might have said, "If music be the food of love, then multimedia must represent the smorgasbord."

## Adjusting the Levels

Think back for a moment to those days of old when Mom or Dad would yell into your bedroom to "TURN THAT NOISE DOWN!" Doesn't that bring back memories? In particular, it brings back the memory that sometimes you just have to crank the tunes.

Most music or multimedia players you are likely to use under Linux have some kind of a volume control. Your speaker system likely has one, as well. There is, however, a third set of controls you should know about: the GNOME volume control. Look over to the right of the top panel and you should see an icon that looks like a speaker. Click that speaker icon and a simple volume slider appears (see Figure 18-1). This provides you with a fast means of making volume-level adjustments.

![](img/0e9cf4c65a042f4a9bea644dc50153a7_342_0.png)

Under certain circumstances, you'll want finer control over the levels of certain devices, at least better than the single slider can provide. Either double-click the top panel speaker icon or right-click the icon and select Open Volume Control from the drop-down menu. A Volume Control three-tabbed mixer panel appears with your system sound card's name alongside (see Figure 18-2).

The various sliders correspond to various levels, from that of your hardware's master levels to the PCM output, microphone inputs (under the Capture tab), and so on. Pause your mouse pointer over the sliders and a message describing the slider's function appears at the bottom of the window.

![](img/0e9cf4c65a042f4a9bea644dc50153a7_343_0.png)

**Figure 18–2** The GNOME volume control can be configured to show multiple levels.

> *Note* The number of sliders and controls vary from sound card to sound card and they may not all be activated by default. Click Edit on the menu bar, then select Preferences. Check boxes representing the possible input and output sources appear. To add one to your mixer control panel, check the appropriate box.

Now that you can easily modify the level of *noise* coming from your speakers, it’s time to get some music on.

## Playing Audio CDs with the Sound Juicer

Try this. Get your hands on your favorite music CD and pop it into your Ubuntu system’s CD drive. As I write this, I’ve got my Pink Floyd *Echoes* album handy, so I’ll use that as an example. A few seconds later, the Sound Juicer application window appears (see Figure 18–3). Sound Juicer, which you can also start from the Sound & Video menu under Applications on the top panel, is the default CD player for Ubuntu.

![](img/0e9cf4c65a042f4a9bea644dc50153a7_344_0.png)

**Figure 18-3** The Sound Juicer is a multiuse multimedia application. Aside from being the default Ubuntu CD player, it is also a CD ripper.

Along the top, there are fields identifying the Title of the CD, the Artist, and the Genre. Directly below this information is a list of all the songs on that CD. Because I mentioned that this is the default CD player, I cover this aspect of the program first. Notice that all of the songs are selected when the CD is inserted (the check box to the left of the title).

Click the Play button, sit back, and enjoy the music. Each song on the CD is then played in sequence. As songs are played, the Play button turns into a Pause button. To skip a song, just double-click the song title you want to hear and Sound Juicer abandons your current selection and jumps to the track of your choice. Next to the track number, a little speaker icon appears showing you the song being played. The track title also appears in Sound Juicer's title bar.

Sound Juicer is also a CD ripper, allowing you to make personal copies of your music to play on your Linux system or on a portable player. I’ll cover this in detail shortly, but I want to wrap up CD playing. That means I’m going to leave the Sound Juicer behind for a moment so I can tell you about another CD player.

## A Simpler CD Player

Although it doesn’t come up automatically, and you can’t find it in the Applications menu, Ubuntu has another CD player that you might prefer, the GNOME CD player. If all you want to do is play your CDs and you want a simple, easy-to-use interface, look no further. Press <Alt+F2> to bring up your quick-start application starter and type in `gnome-cd`. The CD player launches (see Figure 18-4). Click the Play button, sit back, and enjoy.

![](img/0e9cf4c65a042f4a9bea644dc50153a7_345_0.png)

> **Tip** If you can’t find the CD player, install it with Synaptic. Look for and install the `gnome-media` package.

On the left of the player, just above the Pause button, there’s a button with a tool icon. Click this button to bring up the CD player preferences dialog. Next to that is the standard list of controls to skip over songs, fast forward, or stop. On the far right of the CD player, there’s a vertical slider control. That’s a volume control.

After the GNOME CD player has started, look in your top panel’s notification area and you see a small icon that looks like a CD. Left-click the icon and the CD player disappears into the panel. Right-click the applet and you have access to the basic CD player controls such as Previous, Next, Stop, Play, and so on (see Figure 18-5).

![](img/0e9cf4c65a042f4a9bea644dc50153a7_346_0.png)

**Figure 18-5** The GNOME CD’s top panel applet provides some handy, out-of-the-way, controls.

## Ripping and Burning Songs

Over the years, we have all purchased a lot of music CDs or, as some of us still call them, *albums*. Many of those albums, unfortunately, had only two or three songs we really liked, so playing the whole album wasn’t what we wanted. As a result, we created collections of our favorite songs on tape and played the tapes, instead.

These days, with the help of our Linux systems, we can create our own collections from those albums we purchased and create CD collections of those songs we want to hear. Furthermore, if you have lots of disk space and you spend a lot of time at your computer, nothing beats a collection of songs ready to play without having to change CDs all the time. Pulling songs from a CD and saving them to your system as digital images is what is commonly referred to as *ripping*. The *burning* happens when you take a collection of songs and, well, burn them to a CD.

## Intermezzo: Digital Audio Formats

Before I get into the mechanics of ripping and burning songs, I’d like to spend a small amount of time discussing music formats. When you purchase a CD, the songs on that CD are in a format not generally used by your system. In fact, when we copy songs to disk from a CD, we always encode it into another, usually more compact format. The format we transfer to is identified by a three-letter extension on the filename. The most common format extensions are .wav, .mp3, and (more recently) .ogg.

The WAV format is one originally created by Microsoft. It is extremely common but not the most efficient in terms of compression. On the other hand, the MP3 format (from the Motion Pictures Experts Group, a.k.a. MPEG) owes its popularity to the high compression ratio it uses—about 12:1. The newcomer on the block is the OGG (or Ogg Vorbis) format. Like MP3, it boasts a high compression rate, but unlike MP3, it is completely unencumbered by patents.

To give you an idea of the compression values, I ripped a 3-minute, 46-second song to WAV format. It came in at 39,866,444 bytes, whereas the same song in OGG format required only 3,438,407 bytes. If you do the math, that is a ratio of 11.6:1. Pretty impressive reasons for not using WAV format files.

## Using Sound Juicer as a CD Ripper

Every time you put in a new audio CD, every song is selected, either for play or for extraction by Sound Juicer. Earlier, I had you play the songs, but clicking the Extract button is pretty much all you need to do to get those songs onto your hard drive. Alternatively, you can select individual songs by clicking the check boxes to the left of each song.

When the process starts, the Play button is grayed out and the Extract button changes to a Stop button in case you want to cancel the process. At the bottom of the Sound Juicer window, on the left side, is a graphical progress bar. Directly to the right of that, the estimated time is indicated along with the speed at which the process is taking place (see Figure 18-6). The resulting songs are saved in your home folder using the following format:

```
/home/username/artist_name/album_name/track_title.ogg
```
