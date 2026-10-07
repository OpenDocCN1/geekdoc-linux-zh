# v:4.33 A Comprehensive Beginner's Guide to Linux as a Digital Forensic Platform

Disk home.blkls - 95 MB / 91 Mib - CHS 12 225 63 (RO), sector size=512

Elapsed time 0h0m0s
Pass 1 (blockSize=1024) STATUS_EXT2_ON
photorec_out.1/f0012156.gif 12156-12205
photorec_out.1/f0012206.jpg 12206-12261
photorec_out.1/f0012262.jpg 12262-12293
photorec_out.1/f0012294.bmp 12294-12863
photorec_out.1/f0012294.gz 12904-186965
Elapsed time 0h0m0s
Pass 1 +5 files
jpg: 2/4 recovered
bmp: 1/1 recovered
gif: 1/1 recovered
gz: 1/1 recovered
Total: 5 files found

12196 sectors contains unknown data, 2 invalid files found and rejected.

PhotoRec exited normally.

Like scalpel, the log output provides suitable information for inclusion in a report if needed, note that the offset locations for each carved file are given in sector offset rather than byte offset (multiply each offset given above by 512 to get the offsets with the scalpel audit.txt file).

Have a look at the output of photorec:

```
barry@forensic1:-/carve$ ls photorec_out.1/
f0012156.gif f0012206.jpg f0012294_lrkn.tar.gz
f0012206.jpg f0012294.bmp report.xml
```

The contents of the output show photorec f0012294_lrkn.tar.gz. If you recall your able_3 exercise, you'll remember that this was a file of some interest. photorec is useful for more than just a few images. If you try/extract the file, you'll find corrupted. Some of it, however, is still recoverable.

```
barry@forensic1:-/carve$ tar tzvf photorec_out.1/f0012294_lrkn.tar.gz
drwxr-xr-x -lp 0 1998-10-01 18:48 lrk3/
-rxr-xr-x -lp 742 1998-06-27 11:30 lrk3/1
-rw-r--r-- -lp 716 1996-11-02 16:38 lrk3/MCONFIG
-rw-r--r-- -lp 6833 1998-10-03 05:02 lrk3/Makefile
-rw-r--r-- -lp 6364 1996-12-27 22:01 lrk3/README
```

281