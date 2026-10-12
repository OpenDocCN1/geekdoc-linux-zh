# # Burning DVDs

The new grovisofs utility makes it possible to create DVDs. Because grovisofs is still young, its graphical interface is relatively immature. We show you how to use grovisofs via a CLI. Follow these steps to copy files to a DVD:

+   1. Insert a **DVD** into your DVD burner.
+   	- You can use either the "plus" (DVD+RW) or "minus" (DVD-RAM) format DVD burner.
+   2. Open a **GNOME Terminal** emulator window by clicking the GNOME Menu and choosing **System Tools** > **Terminal**.
+   3. Run the following command to determine which **Linux** device file corresponds to your DVD writer:
+   
+   	```
+   	grep -i dvd /var/log/dmesg
+   	```
+   
+   	- You should see output similar to the following, where **hdc** is the device file you seek:
+   	```
+   	hdc: Hewlett-Packard DVD Writer 200, ATAPI CD/DVD-ROM drive
+   	```
+   4. If you want to burn tracks you ripped via Sound Juicer (in the "**Extracting CD**

**Music with Sound Juicer** section), run this command:

```
grovisofs -Z /dev/hdc -1 -R -J ~/music/*ogg
```

grovisofs writes the files to your DVD. Note that /dev/hdc corresponds to the information you obtained in Step 3.

+   5. You can **append** more files:
+   
+   	```
+   	grovisofs -M /dev/hdc -1 -R -J ~/other music/*ogg
+   	```
+   
+   6. You're not limited to burning only files. You can also write the common ISO-9660-formatted images to a DVD. Run this command to create a DVD using an ISO image:
+   
+   	```
+   	grovisofs -vdv -compat -Z /dev/hdc=Image.iso
+   	```

The easy-to-use grovisofs utility allows you to create DVDs, which now store more than 4.5GB of data — much more than CD-ROMs can handle. Future DVD formats will store more than 40GB of data.

The following instructions show how to burn Ogg music files to a writable CD.

+   1. **Log in** as any user and insert a disc (either CD-R or CD-RW) into your CD writer drive.
+   
+   2. **Double-click** your home-directory icon, in the upper-left corner of your desktop.
+   	- A Nautilus window opens, showing the contents of your home directory.
+   
+   3. Click the **Places** menu and select **CD Creator**.
+   	- The CD Creator window opens.
+   
+   4. Back in the first **Nautilus** window (your home directory), double-click the folder that contains the music files you want to record.
+   	- For instance, if you follow the directions in the previous section, "Ripping CD Music Files," you save the music in a new directory. The files are saved in Ogg format.