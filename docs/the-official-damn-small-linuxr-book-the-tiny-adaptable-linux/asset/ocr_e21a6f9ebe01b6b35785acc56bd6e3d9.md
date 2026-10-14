+   2. Create a working directory to contain all of your files and directories and change to it:
+   # mkdir remaster
+   # cd remaster

+   3. Copy over the scripts from the /chapter11 directory on the enclosed CD-ROM.
+   # cp -a /cdrom/chapter11/remaster/* .
+   # cp /cdrom/chapter11/remaster/.bash_profile .

+   4. Create directories:
+   # mkdir source master iso
+   # mkdir source/KNOPPIX/

+   5. Copy the contents of the CD-ROM to the proper directories:
+   # cp -Rp /KNOPPIX/* source/KNOPPIX
+   # cp -Rp /cdrom/index.html master/
+   # cp -Rp /cdrom/boot/ master/

+   6. Perform a final cleanup by removing the existing KNOPPIX image, and then sync all files:
+   # rm master/KNOPPIX/KNOPPIX
+   # sync

As a result of the preceding steps, you now have your remastering working directory environment properly set up. After the setup scripts are copied to the working directory, you can automate the setup of the image remastering process by running the setupFromCD script contained in the working directory.

The setupFromCD script is shown here:

```
#!/bin/sh
rm -rf source master iso
mkdir source master iso
mkdir source/KNOPPIX
cp -Rp /KNOPPIX/* source/KNOPPIX/
cp -Rp /cdrom/* master/
rm master/KNOPPIX/KNOPPIX
sync
```

At this point, all files have been copied from the DSL CD-ROM to the source and master directories. I also use one other text file called release.txt. This is where I place the version number for the release I am working on, for example:
ds1-3.3

As you can see, release.txt is a simple, one-line text file. However, this makes it easy to change release numbers without having to remember where inside the main image file to update.