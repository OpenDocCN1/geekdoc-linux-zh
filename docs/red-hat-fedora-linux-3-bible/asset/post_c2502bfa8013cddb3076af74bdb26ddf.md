
This example reads all of the music tracks from the CD-ROM drive. The -B option says to output each track to a separate file. By default, the cdcd2wav command outputs the files to the WAV audio format.

Instead of extracting all songs, you can choose a single track or a range of tracks to extract. For example, to extract tracks 3 through 5, add the -t3+5 option. To extract just track 9, add -t9+9. To extract track 7 through the end of the CD, add -t7.

> **NOTE:** If you have a low-quality CD drive or an imperfect CD, cdcd2wav might not be the best ripping tool. Instead of cdcd2wav, you could use cddparanoia -B to extract songs from the CD to hard disk.

4. When cdcd2wav is done, insert a blank CD into your writable CD drive.

5. Use the cdrecord command to write the music tracks to the CD. For example:

```
# cdrecord -v dev=/dev/cdrom -audio *.wav
```

The options to cdrecord tell the command to create an audio CD (-audio) on the writable CD device located at /dev/cdrom. The cdrecord command writes all files from the current directory that end in .wav. The -v option causes verbose output.

If you want to change the order of the tracks, you can type their names in the order you want them written (instead of using *.wav). If your CD writer supports higher speeds, you can use the speed option to double (speed=2) or to quadruple (speed=4) the writing speed.

After you have created the music CD, indicate the contents of the CD on the label side of the CD. The CD should now be ready to play on any standard music CD player.

# Burning CDs/DVDs with K3b

For anyone who has sometimes struggled getting the options just right with cdrecord, the K3b CD/DVD Burning Facility is a wonderful tool. Modeled after popular CD recording tools you can find in Windows environments, K3b provides a very intuitive way to master and burn your own CDs and DVDs.

One of the best uses of K3b is to master and burn your own audio CDs and burn ISO images (perhaps containing a Linux distribution you want to try out) that you download from the Internet. To start K3b, select Sound & Video → K3b from the Applications menu. Figure 8-10 shows an example of the K3b window:

![](img/b22364e57409c2481ba806e4e6b9309c_332_0.png)

Figure 8-10: Master and burn CDs and DVDs using the K3b window.

To burn a CD image to CD using K3b, do the following:

1. Download or otherwise copy an ISO image to a directory on your hard disk. A CD image will be up to about 700MB, while a DVD image can be over 4GB.
2. From the K3b window, select Tools → CD → Burn CD Image. A Burn CD Image window appears.
3. Next to the Image to Burn box, select the folder icon to browse your file system to find the ISO image. Once you select the image, it is loaded into the Burn CD Image window, which will display information about the image, including its MD5sum.
4. Check the MD5sum and compare it with the MD5sum provided with the ISO image when you downloaded it. (There is likely a file ending with .md5 in the directory from which you downloaded the image.)
5. If the MD5sums match, continue by checking out the settings on the Burn CD Image window. I've had generally good luck using the default settings. However, I find that if I get a bad burn, often changing the speed from Auto to a slower speed that is auto detected will result in a good burn.
6. Click Start to begin burning the image to CD. When the writing is done, K3b will tell you whether it thought the burn process was successful.

There are lots of ways to use K3b. You can make a copy of a CD (Tools → CD → Copy CD) or DVD (Tools → CD → DVD → Copy DVD). You can create a new audio CD (File → New Project → New Audio CD Project, then drag-and-drop the files you want on the CD into the K3b folder and click Burn) or data CD (select that project type, drag-and-drop, and select Burn).

# Ripping CDs with Grip

The Grip window provides a more graphical method of copying music from CDs to hard disk. You can then play the songs directly from your hard disk or burn them back on to a blank CD. Besides just ripping music, you can also compress each song as you extract it on to the CD.

You can open Grip from the red hat menu by selecting **Sound & Video → Grip** (or by typing **grip** from a Terminal window). Figure 8-11 shows an example of the Grip window.

![](img/b22364e57409c2481ba806e4e6b9309c_333_0.png)

To rip audio tracks from a CD with `grip`, do the following:

1. With the Grip window open, insert a music CD into your CD drive. If you have an active connection to the Internet and the CD is known to the CD database, the title, artist, and track information appear for the CD.
2. Left-click on each track that you want to rip (that is, copy to your hard disk). A check mark appears under the Rip column for the song.
3. Click the Config tab at the top of the page, then select Encode.
4. You can select the type of encoder used to compress the music by clicking the Encoder box and selecting an encoder (by default, **oggenc** compresses files in Ogg Vorbis).
5. Click the Rip tab at the top of the page. The Rip tab appears.
6. Click one of the following:

   - **Rip+Encode** — This rips the selected songs and (if you left in the default oggenc compression as described previously) compresses them in Ogg Vorbis format. You need an Ogg Vorbis player to play the songs after they have been ripped in this format (there are many Ogg Vorbis players for Linux).
   - **Rip only** — This rips the selected songs in WAV format. You can use a standard CD player to play these songs. (When I tried this, the same song ripped in WAV was twelve times larger than the Ogg Vorbis file.)

Songs are copied to the hard disk in the format you selected. By default, the files are copied into a subdirectory of *$HOME* (such as /home/jake). The subdirectory is named for the artist and CD. For example, if the user jake were ripping the song called High Life by the artist Mumbo, the directory containing ripped songs would be /home/jake/ogg/mumbo/high_life. Each song file would be named for the song (for example, *fly_fly_fly.wav*).

At this point you can play any of the files using a player that can play WAV or Ogg files, such as XMMS. Or you can copy the files back to the CD using *cdrecord*. Because the filenames are the song names, they don't appear in the same order as they appear on the CD. So if you want to copy them back to a writable CD in the same order where they originally appeared, you may have to type each filename on the *cdrecord* command line. For example:

```
# cdrecord -v dev=/dev/cdrom -audio fly_fly.wav big_news.wav about_time.wav
```

The Grip window can also be used to play CDs. Use the buttons on the bottom of the display to play or pause, skip ahead or back, stop, and eject the CD. The Toggle track display button lets you shrink the size of the display so it doesn't take up much space on the desktop. Click Toggle disc editor to see and change title, artist, and track information.

In addition to grip, Fedora includes the Sound Juicer CD Ripper, which you can launch by selecting Sound & Video → Sound Juicer CD Ripper from the red hat menu. Sound Juicer can also extract, or rip, files from an audio CD. I found Sound Juicer had slightly better quality when ripping a CD.

# Creating CD labels with cdlabelgen

The *cdlabelgen* command can be used to create tray cards and front cards to fit in CD jewel cases. You gather information about the CD and *cdlabelgen* produces a PostScript output file that you can send to the printer. The cdlabelgen package also comes with graphics (in */usr/share/cdlabelgen*) that you can incorporate into your labels.

Here is an example of a cdlabelgen command line that you can use to generate a CD label file in PostScript format. (Type it all on one line or use backslashes, as shown here, to put it on multiple lines.)

```
cdlabelgen -c "Grunge is Gone" -s "Hop Hie*Hop" \
-i "*If You Feed Me*Sockin Years*City Road*Platinum and Copper*Fly Fly \
```
