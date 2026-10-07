
# v.4.33 A Comprehensive Beginner's Guide to Linux as a Digital Forensic Platform

No extension, and ewfacquirestream automatically appends an E01 extension to the resulting file. To get a complete list of options, look at the man pages, or run the command with the -h option.

Back on the subject system we use our standard "send the data across the wire from a subject computer" command...

```
root@bootdisk:~# dd if=/dev/sda | nc 192.168.55.20 2525
```

Once the acquisition completes (you'll need to stop the ewfacquirestream process on the collection system when the dd command on the subject system), you can look at the resulting files, and compare the hashes. Since we used shalsum previously, we'll re-run with md5sum ewververify output:

```
root@bootdisk:~# md5sum /dev/sda
c96c510404d99b4684e50a6995443c9a /dev/sda
-rw-r--r 1 root root 1.5G May 09:50 nc_wf_image.E01
-rw-r--r 1 root root 1.5G May 09:50 nc_wf_image.E02
-rw-r--r 1 root root 1.5G May 09:50 nc_wf_image.E03
-rw-r--r 1 root root 1.5G May 09:50 nc_wf_image.E04
-rw-r--r 1 root root 1.5G May 09:50 nc_wf_image.E05
-rw-r--r 1 root root 1.5G May 09:50 nc_wf_image.E06
-rw-r--r 1 root root 1.5G May 09:50 nc_wf_image.E07
-rw-r--r 1 root root 1.5G May 09:50 nc_wf_image.E08
-rw-r--r 1 root root 293M May 09:50 nc_wf_image.E09
```

```
root@forensic1:~# ewverify nc_wf_image.E01
ewverify 20140608
```

Verify started at: May 06, 2017 09:51:52
...
Verify completed at: May 06, 2017 09:55:50

Read: 12 GiB (1288401888 bytes) in 3 minute(s) and 58 second(s) with 51 MiB/s (5413823 bytes/second).

```
MD5 hash stored in file:
c96c510404d99b4684e50a6995443c9a
MD5 hash calculated over data:
c96c510404d99b4684e50a6995443c9a
```

```
ewverify: SUCCESS
```

...and our verification is successful.

v.4.33 A Comprehensive Beginner's Guide to Linux as a Digital Forensic Platform

# Over the Wire – Other Options

Here've covered the very basics and mechanics of imaging media over a network pipe. netcat is not your solution to this, though it is one of the simpler options and is widely available on most boot disks and Linux systems.

In reality, you might want to consider whether your data went encrypted as it traverses the network. In our example, we may have been connected via a crossover cable (interface to interface) or through a standalone network hub. What if you are in a situation where many of connection is collect? Or over enterprise hardware (switches, etc.)? In that case you would want encryption. For that you could use cryptcat, or ssh. Now that you understand the basic mechanics of this technique, you are urged to explore other tools and methods. There are projects out there like ddd https://sourceforge.net/projects/ddd/ and air (https://sourceforge.net/projects/air-image/) you might want to explore, for more than just network imaging. Compression on the fly with

Another useful capability while imaging is compression. Considering our concern for forensic application here, we will be sure to manage our compression technique so that we can verify our hashes without decompress and write our images before checking them.

For this exercise, we will use the GNU gzip application. gzip is a command line utility that allows us manage some fairly granular control over the compression process. There are other compression utilities (zip, xz, etc.), but we will concentrate on gzip for the reasons we learned dd and vi... always available, and starting point to learn the command line concepts. Most source packages for software is minimally available in a gz compressed format, but I urge you to explore other compression options on your own.

First, for the sake of familiarity, let's look at the simple use of gzip on a single file and explore some of the options at our disposal. I have created a directory called testcomp and I've copied the image file NTFS_Pract_2017.raw into that directory to practice. This gives me an uncluttered place to experiment. First, let's double check the hash of the image:

```
root@forens1:\# mkdir testcomp

root@forens1:\# cp nt NTFS_Pract_2017.raw testcomp/

root@forens1:\# cd testcomp

root@forens1:~/testcomp# ls -lh
total 501M
-rw-r--r-- 1 root 500M 6 12:10 NTFS_Pract_2017.raw
```

```
root@forens1:~/testcomp# sha1sum NTFS_Pract_2017.raw
094123df4792b18a1f064f1e2fc609028695f85 NTFS_Pract_2017.raw
```

Now, in its most simple form, we can call gzip and simply provide the name of the file we compressed. This will replace the original file with a compressed file that has a .gz suffix appended.

```
root@forensic:~/testcomp# gzip NTFS_Pract_2017.raw

root@forensic:~/testcomp# ls -lh
total 61M
-rw-r--r-- 1 root 61M May 6 12:10 NTFS_Pract_2017.raw.gz
```

So now we have replaced our original 500M file with a 61M file that has a .gz extension. To decompress the resulting .gz file:

```
root@forensic:~/testcomp# gzip -d NTFS_Pract_2017.raw

root@forensic:~/testcomp# ls -lh
total 500M
-rw-r--r-- 1 root 500M May 6 12:10 NTFS_Pract_2017.raw
```

```
root@forensic:~/testcomp# shasum NTFS_Pract_2017.raw
094123df4792b18a1f64f1e26902855 NTFS_Pract_2017.raw
```

We decompressed the file and replaced the .gz file with the original image. A check of the hash shows that all is in order. Suppose we like to compress a file but leave the original intact. We can use the gzip command with the -c option. This writes to stdout instead of replacement file. When using this option we need to redirect the output to a filename of our choosing here a sample using this technique:

```
root@forensic:~/testcomp# ls -lh
total 51M
-rw-r--r-- 1 root 500M May 6 12:10 NTFS_Pract_2017.raw
```

```
root@forensic:~/testcomp# gzip -c NTFS_Pract_2017.raw > NewImage.gz

root@forensic:~/testcomp# ls -lh
total 51M
-rw-r--r-- 1 root 500M May 6 12:10 NTFS_Pract_2017.raw
-rw-r--r-- 1 root 61M May 6 12:32 NewImage.gz
```

```
root@forensic:~/testcomp# gzip -cd NewImage.gz > Newcompressed.raw
```

```
root@forensic1:~/testcomp$ ls -lh
total 1G
-rw-r--r-- 1 root root 500M May 6 12:10 NTFS_Pract_2017.raw
-rw-r--r-- 1 root root 61M May 6 12:33 NewImage.gz
-rw-r--r-- 1 root root 500M May 6 12:33 Newcompressed.raw
```

```
root@forensic1:~/testcomp# shaisum Newcompressed.raw
094123df4792b18a1f0f64f1e2fc6028655 Newcompressed.raw
```

In the above output, we see that the first listing shows the image file. We then compress using gzip -c which writes to standard output. We redirect that output to a new file (name of our choice). The second listing shows that the original file remains, and the compressed file is created. We then use gzip -cd to decompress the file, redirecting the output to a new file and this preserving the compressed file.

These are very basic options for the use of gzip. reason why the -c option allows us to compress a file and pipe the output to hash algorithm. In a more practical sense, this allows us to create a compressed image and check the hash of that image without writing the file.

If we go back to a single image file in our directory, we can do this action. Remove all the files we just created (using the rm command) and leave the single original dd image. Now we will create a single compressed file from that original image and then check the hash of the compressed file to ensure its validity:

```
root@forensic1:~/testcomp# ls -lh
total 501M
-rw-r--r-- 1 root root 500M May 6 12:10 NTFS_Pract_2017.raw
```

```
root@forensic1:~/testcomp# gzipisum NTFS_Pract_2017.raw
```

```
root@forensic1:~/testcomp# ls -lh
total 61M
-rw-r--r-- 1 root root 61M May 6 12:10 NTFS_Pract_2017.raw.gz
```

```
root@forensic1:~/testcomp# cd NTFS_Pract_2017.raw.gz | shaisum
094123df4792b18a1f0f64f1e2fc60286555 -
```

```
root@forensic1:~/testcomp# ls -lh
total 61M
-rw-r--r-- 1 root root 61M May 6 12:10 NTFS_Pract_2017.raw.gz
```

# v.4.33 A Comprehensive Beginner's Guide to Linux as a Digital Forensic Platform

First we see that we have the correct hash. Then we compress it with a simple gzip command that replaces the original file. Now, all we want to do next is check the hash of our compressed image without writing out a new image. We can do this using gzip -c (standard out) -d (decompress), passing the name of our compressed file but piping the output to our hash algorithm (in this shaisam). The result shows the correct hash of the output stream, where the output stream is signified by the -

Okay, now that we have a basic grasp of gzip to compress, decompress, and verify hashes, let's put it to work "on the fly" using dd to create a compressed image. We will then check the compressed image's value against an original hash.

Find a small thumb drive or other media to image. I'll be using a 8GB USB stick. Clear out the testcomp directory so we have a clean place to write our image (or wherever we have the space to write).

Obtaining a dd image on the fly is a matter of streaming and redirecting that output through a pipe to the gzip command and our resulting image can then be checked. Consider the following. The physical device we have as an example in this case is /dev/sdi (if we are using a device to follow along, remember to use lssci and lsblk to find the correct device).

```
root@forensic1:~/testcomp shaisam /dev/
21e8e63bfc9c3fa782339567dd94bbb2cfc /dev/
```

```
root@forensic1:~/testcomp# dd if=/dev/sdi gzip -c > sdi_image.raw
156958571+0 records in
156958571+8 records out (8.0 GB, 7.5 GiB) copied, 283.091 s, 28.4 MB/s
```

```
root@forensic1:~/testcomp# ls -lh
total 2.8G
-rw-r--r-- 1 root root 2.8G sdi_image.raw
```

```
root@forensic1:~/testcomp# gzip -cd sdi_image.raw | shaisam
21e8e66bfc9c3fa782339567dd94bbb2cfc
```
