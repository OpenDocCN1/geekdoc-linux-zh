# v.4.33 A Comprehensive Beginner's Guide to Linux as a Digital Forensic Platform

```
...
-rw-r--r-- lp/lp 1996 1996-11-02 16:39 lrk3/z2.c
```

gzip: stdin, trailing garbage ignored
tar: Child returned status 2
tar: Error is not recoverable: exiting now

There is still much information that can be cleaned from the recovery of this file. We can see the README is one of those files recovered. We can use this to define strings for us to search and discover where the archive was decompressed and extracted (which we did earlier in our physical search exercise). This is one of the reasons to use more than one carving utility. Differences in output can strengthen our analysis.

One question you might find yourself asking "How do I efficiently compare output from two different tools to get an accurate count of files recovered?”. In our very small sample produced by the exercises it's a fairly simple job. We just compare the images in a graphical viewer. There are a little over a dozen images to review. If, however, we were to carve a disk image with hundreds of unallocated image files, the comparison would be far more difficult. To address this, let's have a look at a simple program that will do the work for us.

# Comparing and De-duplicating Carve Output

Obviously this is not a simple matter of comparing file names. The files are carved from the data blocks without any regard to directory entries or other file system information. So the tools use their own naming. Interestingly photorec included the name of the original lkrn.tar.gz name of the archive in its output. This is because the name of the file is part of the file metadata (run file f012904_lkrn.tar.gz and you'll see the gzip headers name).

One can also compare hashes. If hashes match, regardless of file name, we know have two of the same files. One simple way to do this is to hash all the files in each directory (photorec_out/ scalp_out/) and write them to a file. We then sort this file by hash and look for duplicates. This can be done in one command. Note that we use f* and for md5sum in each directory so that we get the carve outputs and not the log/audit files from each file.

```
barry@forensic:~/carve photorec_out.f/ | scalp_out/ | sort
11983800a177c174c45b15edc909a photorec_out.f/f012156.gif
11983800a177c174c45b15edc909a scalp_out/00000000.jpg
2d74def42fbcc0c8c1a32750f5f05 photorec_out.f/f012904_lkrn.tar.gz
357ca99e65ca2b179el7c5a0290b1f94 photorec_out.f/f012262.jpg
357ca99e65ca2b179el7c5a0290b1f94 scalp_out/00000004.jpg
473a641c3253ba3a6a45759b2bc707ae photorec_out.f/f012206.jpg
```

282