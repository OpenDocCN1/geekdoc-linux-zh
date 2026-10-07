```
root@forensic1:~# ewinfo EncaseImage.E01
ewwfinfo 20140608
```

Acquiring information
Description: TestImage
Examiner name: Susan B. Analyst
Acquisition date: Fri Feb 17 13:59:50 2017
System date: Fri Jan 13 16:10:42 2017
Operating system used: Windows 7
Software version used: 7.10.05
Password: N/A
Model: ST2500
Serial number: 03-016831-C
Device label: WT055 12
Extents: 0

EWF information
File format: unknown
Sectors per chunk: 64
Error granularity: 64
Compression method: deflate
Compression level: best compression
Set identifier: ff582a89-3aba-cf46-a634-75edf9c15a97

Media information
Type: physical
Is physical: yes
Bytes per sector: 512
Number of sectors: 2500844416
Media size: 119 GiB (128022740992 bytes)

Digest hash information
MD5: 46c4d29a3ba96fffb8d7690949dea1b

Also note that the MD5 value shown is the value of the data. NOT the images themselves. Hashing the image files will not allow you to verify against the hash of the original media - the E0* files contain meta data and do not represent an exact copy of the source media. If you want to verify the hash of the data after it's moved, you need to use a tool like ewfverify.

Hashing the data in EWF files requires a tool that recognizes the metadata associated with an EWF file and parse and hash the original data. For this use we ewfverify.

```
root@forensic1:~# ewfverify case1.disk2.E01
ewffverify 20140608
```