```
#dosemu floppy image
drive m: file="/var/lib/dosemu/diskimage"
#dosemu hdimage
drive n: file="/var/lib/dosemu/diskimage" offset=8832
#Atari ramdisk image
drive o: file="/tmp/atari_rd" offset=136
mtools_lower_case=1
```

# Copying Files to a DOS Partition

Once the DOS hard disk partitions are referenced, you can then use their drive letters to copy files to and from them to your Linux partitions. The following command copies the file mydoc.html to the c: partition in the directory webstuff and renames it mydoc.htm. Notice the use of forward slashes instead of backward slashes.

```
$ mcopy mypage.html c:/webstuff/mypag.htm
```

Because of the differences in the way DOS and Linux handle newlines in text files, you should use the -t option whenever copying a DOS text file to a Linux partition. The following command copies the mydoc.txt file from the c:/project directory to the /newdocs directory:

```
$ mcopy -t c:/project/mydoc.txt /newdocs
```