# v.4.33
A Comprehensive Beginner's Guide to Linux as a Digital Forensic Autopsy

```
12840+2 records in
12842+0 records out
6575104 bytes (6.6 MB, 6.3 MiB) copied, 0.163989 s, 40.1 MB/s
dd: error reading '/dev/sdf': Input/output error
12840+3 records in
12843+0 records out
6575616 bytes (6.6 MB, 6.3 MiB) copied, 0.16426 s, 40.0 MB/s
dd: error reading '/dev/sdf': Input/output error
12840+4 records in
12844+0 records out

41943024+16 records in
41943040+0 records out
2147836480 bytes (21 GB, 20 GiB) copied, 1249.57 s, 17.2 MB/s
```

What you end up with the end of this command is an image of the entire disk, but with the errors filled in (sync)d zeros to maintain correct offsets within file systems.

Obviously, simple failure (“giving up” when errors are encountered) is not good. Any data in reading areas beyond the errors will be missed. The problem with ignoring errors and attempting to read back them (using conv=noerror) is that we are stressing a disk that is already possibly on the verge of complete failure. The fact of the matter is that you may get few chances at reading a disk that has “bad sectors”. If there is an actual physical defect, the simple act of reading the bad areas makes matters worse, leading to disk failure before other viable areas of the disk are collected. If all of these, of course, to disks with “physical” storage. Solid state storage is another matter entirely.

So, when we use conv=noerror to an imaging command, we are actually asking our imaging tools to “gr through” the bad areas. Why not skip over the bad sections altogether, in many cases recovery may be unlikely? Instead we should concentrate on recovering data from areas of the disk that are good. Once the “good” data is acquired, we can go back and attempt to collect data from the error areas, with a recovery algorithm designed with purpose.

In a nutshell, that is the philosophy behind ddrescue. Used properly, ddrescue will read the “healthy” portions of a first disk, then fall back to recovery mode - trying some of very robust logging to read data from bad sectors. It does this using the log file as a map file), which allows it to resume an imaging at any point, given a map file to work from. This is an important (perhaps the most important) point about using ddrescue - that is, with a map file you never need to read already successfully recovered sectors. When ddrescue references the map file on successive runs, it fills in the gaps, it does not “redo” work again finished.

125