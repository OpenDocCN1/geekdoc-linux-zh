# v.4.33 A Comprehensive Beginner's Guide to Linux as a Digital Forensic Platform

First we see that we have the correct hash. Then we compress it with a simple gzip command that replaces the original file. Now, all we want to do next is check the hash of our compressed image without writing out a new image. We can do this using gzip -c (standard out) -d (decompress), passing the name of our compressed file but piping the output to our hash algorithm (in this shaisam). The result shows the correct hash of the output stream, where the output stream is signified by the -

Okay, now that we have a basic grasp of gzip to compress, decompress, and verify hashes, let's put it to work "on the fly" using dd to create a compressed image. We will then check the compressed image's value against an original hash.

Find a small thumb drive or other media to image. I'll be using a 8GB USB stick. Clear out the testcomp directory so we have a clean place to write our image (or wherever we have the space to write).

Obtaining a dd image on the fly is a matter of streaming and redirecting that dd output through a pipe to the gzip command and our resulting image's hash can then be checked using the same method we used. Consider the following. The physical device we have as an example in this case is /dev/sdi (if we are using a device to follow along, remember to use lssci and lsblk to find the correct device file).

```
root@forensic1:-~/testcomp shaisam /dev/sdi
21e8e63bfc9c3fa782339567dd94bbb2cfc /dev/
```

```
root@forensic1:-~/testcomp dd if=/dev/sdi gzip -c > sdi_image.raw
156958571+0 records in
156958571+8 records out (8.0 GB, 7.5 GiB) copied, 283.091 s, 28.4 MB/s
```

```
root@forensic1:-~/testcomp ls -lh
total 2.8G
-rw-r--r-- 1 root root 2.8G sdi_image.raw
```

```
root@forensic1:-~/testcomp gzip -cd sdi_image.raw | shaisam
21e8e663bfc9c3fa782339567dd94bbb2cfc
```

In the above command there is no "output file" specified, just as when we piped the output to netcat in our "over the we" section. We then follow up with our integrity check by decompressing the file to standard output and hashing the stream. The hashes match, so we can see that we used dd to acquire a compressed image (2.8G vs. 8 GB device), and verified our acquisition without the need to decompress (and write to disk) first.

143