v.4.33 A Comprehensive Beginner's Guide to Linux as a Digital Forensic Platform

We can unmount the /mnt/evid file system and the fuse disk image at /mnt/ewf on the same line by separating with the && This means that the second command (**fsmount**) will only execute if the first unmount is successful.

Back to our problem...To see why the jet.jpg is missing, let's try another method of obtaining a file, the **fls** command. We can use the -f option to look only at directories, and -r to do it recursively. We'll also **grep** for jet.jpg. You could use the directory MFT record numbers to download the file, which is quicker and more efficient:

```
barry@forensic1:/NTFS_Pract_2017$ fls -o 2048 -Fr NTFS_Pract_2017.E01 | grep
jet.jpg
r/r 39-128-1: Users/AlberteE/Pictures/jet.jpg
r/r 39-128-3: Users/AlberteE/Pictures/jet.jpg:unixphreat.txt
```

In the output of **fls**, jet.jpg has two entries:

+   39-128-1
39-128-3

Both entries have the same MFT record number but the attribute identifiers are different. This is an example of an Alternate Data Stream (ADS). Accessing the standard contents (39-128-1) of jet.jpg is easy, since it is an allocated file. However, we can access either data stream, the normal data or the ADS, by using the Sleuth Kit **icat**, much as we did with the files in our previous exercises. We simply call icat with the complete MFT record entry, to include the alternate identifier. Here we specify each of the data streams and send them to the **file** command using icat:

```
barry@forensic1:/NTFS_Pract_2017$ icat -o 2048 NTFS_Pract_2017.E01 39 | file - /dev/stdin: MPEG sequence, vl, progressive Y'CbCr 4:2:0 video, CIF, NTSC, NTFS 4:3, 29.97 fps, Constrained
```

In this first (default) stream, we simply use the MFT record 39 to pass the default data to file. For the second stream, we pass the full attribute (39-128-3):

```
barry@forensic1:/NTFS_Pract_2017$ icat -o 2048 NTFS_Pract_2017.E01 39-128-3 | file -n/dev/stdin: ASCII text, with CRLF line terminators
```

250