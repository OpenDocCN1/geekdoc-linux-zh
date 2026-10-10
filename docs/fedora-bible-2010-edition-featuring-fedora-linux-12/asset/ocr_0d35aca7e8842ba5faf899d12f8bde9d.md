+   1. Download or otherwise copy an ISO image to a directory on your hard disk. A CD image will be up to about 700MB, while a DVD image can be over 4GB.
+   2. From the K3b window, select Tools → Burn CD Image. A Burn CD Image window appears.
+   3. Next to the Image to Burn box, select the folder icon to browse your file system to find the ISO image. After you select the image, it is loaded into the Burn CD Image window, which will display information about the image, including its MDSum.
+   4. Check the MDSsum and compare it with the MDSsum provided with the ISO image when you downloaded it. (There is likely a file ending with `md5` in the directory from which you downloaded the image.)
+   5. If the MDSsums match, continue by checking out the settings on the Burn CD Image window. I’ve had generally good luck using the default settings. However, I find that if I get a bad burn, often changing the speed from Auto to a slower speed that is auto-detected will result in a good burn.
+   6. Click Start to begin burning the image to CD. When the writing is done, K3b tells you whether it thought the burn process was successful.

The descriptions for burning CDs apply to DVDs as well (provided you have a DVD burner). Remember that you are going to need a lot more temporary space on your hard disk to work with DVDs than you would to work with CDs.

# Creating audio and data CDs with Brasero

Brasero, shown in Figure 7-8, provides the default GNOME application for creating CDs. Brasero can burn CDs as well as DVDs and offers a number of advanced features. You can preview the audio tracks, normalize the volume, and check the integrity of the disks. In addition, Brasero offers a CD cover editor to allow you to create the tray cards and front cards to fit into CD jewel cases.

See http://projects.gnome.org/brasero/ for more on Brasero.

# Creating CD labels with cdlabelgen

The cdlabelgen command can be used to create tray cards and front cards to fit in CD jewel cases. You gather information about the CD and cdlabelgen produces a PostScript output file that you can send to the printer. The cdlabelgen package also comes with graphics (in /usr/share/cdlabelgen) that you can incorporate into your labels. Install the package by typing yum install cdlabelgen.