# 528 Part IV Running Applications

Songs are copied to the hard disk in the format you selected. By default, the files are copied into a subdirectory of $HOME/ogg (such as /home/jake/ogg). The subid is named for the artist and CD. For example, if the user jake was ripping the song "High Life" by the artist Mumbo, the directory containing ripped songs would be /home/jake/ogg/mumbo/high_life. Each is named for the song (for example, fly_fly.wav).

+   7. Now you can play any of the files using a player that can play WAV or Ogg files, such as XMMS. Or you can copy the files to a CD using cdrecord. Because the filenames are the same names, they don't appear in the same order as they appear on the CD, if you want to copy them back to a writable CD in their original order, you may have to type each filename on the cdrecord command line. For:

```
# cdrecord -dev=/cdrom --audio fly_fly.wav
big_new.wav about_time.wav
```

The Grip window can also be used to play CDs. Use the buttons on the bottom of the display to play or pause, skip ahead or back, and stop, eject the CD. The toggle track display button lets you shrink the size of the display so it takes less space on the desktop. Click toggle disc editor to see and change title, artist, and track information.

# Creating Labels with cdlabel

The cdlabel can be used to create tray cards and front cards to fit in CD jewels. You gather information about the CD and cdlabel produces a PostScript output file that you can send to the printer. The cdlabel package also comes with graphics (in /usr/share/cdlabel) that you can incorporate into your labels.

Here's an example of a cdlabel command line that generates a CD label in PostScript format (you can type it all on one line or use backslashes, as shown to out):

```
cdlabel -c "Grunge is Gone" -s "Yep HipHop"
-i "If You Feed Me SockingCity RoadPlatinum and Copper%% Fly \
Fly%%Best Man Spins& A Headache In Put Feelin%%Dreams Go \
Blue%%$Mildest Schemes" -o yeppay
```

In this example, the title of the CD is identified by -c "Grunge is Gone" and the artist by -s "Yep HipHop" option. The tracks are entered after the -i option, with each line separated by a % sign. The output file is sent to the file yep.ps with the -o option. To view and print the result, use the evince command like this:

```
$ evince yep.ps
```

The result of this example is shown in Figure 20-7.