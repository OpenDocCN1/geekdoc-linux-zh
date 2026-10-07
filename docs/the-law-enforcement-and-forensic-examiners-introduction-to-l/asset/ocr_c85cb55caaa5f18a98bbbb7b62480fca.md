# v.4.33 A Comprehensive Beginner's Guide to Linux as a Digital Forensic Platform

91481 91482 91483 91484 91485 91486 91487

The information istat shows values directly from the MFT $STANDARD_INFORMATION attribute (which contains the basic meta data for a file) as well as the $FILE_NAME attribute and basic information for other attributes that are part of an MFT entry. The data blocks that contain the actual content are listed at the bottom of the output (for Non-Resident data).

Take note of the fact that there is a separate attribute identifier for the $FILE_NAME attribute, 48-4. It is interesting to know we can access the contents of each attribute using the icat command.

The 48-4 attribute stores the file name. By piping the output of icat to xxd we can see the contents of this attribute, allowing us to view individual attributes for each MFT entry. Its, this may not be of much interest in this particular instance, but you should understand that attributes can be accessed by providing the full attribute identifier.

```
barry@forensic1:~/NTFS_Pract_2017$ icat -o 2048 NTFS_Pract_2017.E01 216-48 | xxd
00000000: 0000 0000 0100 d4cf 7b2 72bc d201 ......{...
00000010: 5ecf 093d 9eec c601 f0c3 72bf d201 \ . . .{...
00000020: f0c3 ce7f 72bc d201 00f0 0000 0000 0000
00000030: d5e9 0000 0000 2000 0000 0000 0000 0000
00000040: 1100 4200 6900 6700 4200 6900 6b00 6500 ..B.i.g..B.i.k.e..
00000050: 4200 4800 3100 3100 3700 2e00 6a00 B.H.1.0.1.7...j.
00000060: 7000 p.g.
```

The same idea is extended to other attributes of a file, most notably the "Alternate Data Streams" or ADS. By showing the existence of multiple attribute identifiers for a given file, the Sleuth Kit gives us a way of detecting potentially hidden data. We do this in our next exercise.

# Sleuth Kit Exercise #5 – NTFS Examination: ADS

First, to see what we are discussing here, in case the reader is not familiar with alternate data streams, we should compare the output of a normal file listing with that obtained through a forensic utility.

Obviously, examining a system, it may be useful to get a look at all of the files contained in an image. We can do this two ways. The first way would be to simply mount our image with the loop back data and get a file listing. We will do this to compare a method using standard command line utilities that were used in the method using the Sleuth Kit tools.

247