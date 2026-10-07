# v4.33
A Comprehensive Beginner's Guide to Linux as a Digital Forensic Platform

-e wordlist - enable scanner wordlist
-e xor - enable scanner xor

These scanners enabled by default; disable with -x:
-x accts - disable scanner accts
-x aes - disable scanner aes
-x base64 - disable scanner base64
-x elf - disable scanner elf
-x email - disable scanner email
-x exif - disable scanner exif

You can also get a slightly more descriptive output on the scanners by doing the same as above with -H instead of -h.

There are a lot of options to go through. Some we'll cover as we go through a sample exercise, and others we'll skip over and explore on your own. The simplest way to run bulk_extractor-235 is to leave everything default and simply provide an output directory for the results. This can take awhile, but it provides the best overall intelligence on the disk contents. For now, we are going to reduce the output by limiting the scanners and providing a single search term. This will allow us to isolate the results and spend some time talking about the output files.

+   Some of the more important options to remember when running bulk_extractor are:
- o output_dir Directory to write the results (bulk_extractor will create this)
- e <scanner> Enable <scanner>
- E <scanner> Disable ALL scanners except <scanner>
- x <scanner> Disable <scanner>

The easiest way to explain the options is to run the command and check the output. We ended the last session on NTFS physical string searching by doing a simple grep for the term "Uranium-235" in our NTFS E01 image set. The results returned nothing. Now we'll run the same again using bulk_extractor. The command with the following options: Note that bulk_extractor runs on the EWF files if installed:

```
barry@forensics1$: bulk_extractor -E zip -find f "Uranium-235" -o blk_out
NTFS_Pract_2017/NTFS_Pract_2017.E01
bulk_extractor version: 1.5.5
Hostname: forensics1
Input file: NTFS_Pract_2017/NTFS_Pract_2017.E01
Output directory: bl_out
Disk Size: 524288000
Threads: 1
08:27:15 Offset 67MB (12.80%) Done in 0:00:12 at 08:27:27
...
08:27:26 Offset 318MB (60.80%) Done in 0:00:08 at 08:27:34
```

259