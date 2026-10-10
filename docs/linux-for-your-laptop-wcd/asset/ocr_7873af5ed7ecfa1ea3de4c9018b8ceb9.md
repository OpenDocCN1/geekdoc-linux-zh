# **XMMS Rules!**

Without a doubt, one of the best .mp3 players for Linux and X11 is the _xmms_ client. This program uses playlists of files to play, offers equalizer controls for fine-tuning sound, and collapses to a nifty, ultra-small control panel that is sure to please any mobile Linux user looking to maximize screen real estate.

Although you can use the command line to create .mp3 files, a much easier way to rip audio CDs into .mp3 format is to use a graphical interface client that will build the necessary command lines automatically and save your files with several mouse clicks.

# **Using the krabber Client**

One of the easiest-to-use graphical clients for converting audio CDs to .mp3 files is the _krabber_ KDE client. This program uses various installed rippers and encoders to offer choices in settings, such as quality and the name of each track. Another great feature is that if you have an active Internet connection, _krabber_ automatically saves and uses your audio CD’s title, artist, and track information after retrieval from a remote server!

To get started, insert an audio CD in your notebook’s CD-ROM drive. Then start the _krabber_ client from the command of an X11 terminal window like this:

```
$ krabber &
```

Note that if you want your files named automatically, you should also have an active Internet connection. When _krabber_ starts for the first time on your computer, it checks for required files, such as ripping and encoder utilities. After the program starts, you’ll see the window shown in Figure 18.13.

Select Settings, CDDB settings. In the Krabber Configuration dialog box, select the CDDB tab. Click on the Enable Remote CDDB item, select a CDDB remote server, click on Update, and click on OK. (Note that this dialog box is very similar to the one shown in Figure 18.10.)

Next, click on button 1 to choose your music. You’ll see a list of tracks. To rip the entire CD, click on the Take All button. The _krabber_ client then displays your tracks, queries a remote CD database server, and then displays the name of the CD, along with the name of each track on the CD, as shown in Figure 18.14.