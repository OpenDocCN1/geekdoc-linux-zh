# v.4.33
nA Comprehensive Beginner's Guide to Linux as a Digital Forensic Platform

...
CONTENT INFORMATION
----------------------------------------------------------------------
Sector Size: 512
Cluster Size: 4096
..

As expected, the keyword is in the only NTFS partition which resides at offset 2048 (sectors). We can complete the math and determine the block the keyword resides in all at once:

```
barry@forensic1:~/NTFS_Pract_2017$ echo "(42659865-(2048*512))/4096" | bc
103893
```

For review, this reads: "Take our offset to the keyword in our data (426596865), subtract the offset to the start of the partition (2048*512), and divide the resulting value by our file system block size (4096). Our file system block is 103893.

```
barry@forensic1:~/NTFS_Pract_2017$ blstat -o 2048 NTFS_Pract_2017.E01 103893
Cluster: 103893
Not Allocated
```

```
barry@forensic1:~/NTFS_Pract_2017$ find -o 2048 -d 103893 NTFS_Pract_2017.E01
248-128-2
```

We can see that blstat tells us the cluster (block) is unallocated, and find shows us that the meta-data structure (MFT entry) associated with that block (-d 103893) is 248-128-2.

```
barry@forensic1:~/NTFS_Pract_2017$ icat -o 2048 NTFS_Pract_2017.E01 248 | file -
/dev/stdin D: Composite Document File V2 Document, Little Endian, Os: Windows, Version 5.1, Code page: 1252, Template: Normal, Last Saved by: buckle, Revision Number: 2, Name of Creating Application: Microsoft Word 10.0, Last Printed: 02:05, Create Time: Tue Nov 21 21:41:00 1995, Last Saved Time/Date: Wed Oct 25 23:14:00 2006, Number of Pages: 2, Number of Words: 822, Number of Characters: Security: 0
```

Piping icat through the file command shows we have a Microsoft Word document. Note that when we pass the MFT record to icat, we use only the record number, 248 rather than the entire attribute since we are looking for the default attribute anywhere, which is $DATA.

254