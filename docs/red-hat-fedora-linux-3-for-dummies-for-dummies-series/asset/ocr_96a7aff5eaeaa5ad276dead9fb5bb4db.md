You can also use MPlayer to listen to Internet audio streams. The entire world of Internet radio and (soon, we hope) video broadcasts is open to you. MPlayer will only become more versatile and useful.

+   Open a GNOME Terminal window by clicking GNOME Menu and selecting System Tools:Terminal.

+   Enter the following command in the Terminal window:
+   `mplayer http://64.202.98.55:80/wr/1`

You'll get to listen to Temple University's (Philadelphia, PA, U.S.A.) jazz and classical station. They use actual human beings to program and play music.

MPlayer plays DVDs too! With MPlayer, your Fedora Core computer becomes a DVD player. The following instructions show how simple the process is:

+   Pop a DVD into your computer.

+   Click the GNOME Menu and select System Tools:Terminal.
+   A GNOME Terminal window opens.

+   Run the following command to determine whether your computer is DVD-capable:
+   `grep -i dvd /var/log/dmesg`

If you have DVD-capable player, you see output similar to the following text:
`hdc: Hewlett-Packard DVD Writer 200, ATAPI CD/DVD-ROM drive` 
`hdd: ATAPI CDROM 48X, ATAPI CD/DVD-ROM drive` 
`hdc: ATAPI 32X DVD-ROM CD-R/RW drive, 2048kB Cache, UDMA(33)`

+   Make note of your DVD device file.
+   In this case, the DVD device file is `/dev/hdc`.

+   Use the information you determined about your DVD to customize the following command:
+   `mplayer dvd:// --dvd-device /dev/hdc`

Your DVD will start playing! You can play bonus tracks by entering the track number after the dvd:// option. For instance, to play track number 2, use the command `mplayer dvd://2 --dvd-device /dev/hdc`. Get your popcorn ready!

You can download a graphical interface to MPlayer called gMplayer. Use the MPlayer download instructions in this chapter to get and install gMplayer.