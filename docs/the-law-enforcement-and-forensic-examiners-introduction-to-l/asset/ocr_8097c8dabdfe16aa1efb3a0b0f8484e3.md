v.4.33 A Comprehensive Beginner's Guide to Linux as a Digital Forensic Platform

# # Sleuth Kit Exercises

This section remains one of the most popular sections of this document, providing hands on exercises for TSK and a sample of its tools.

Like all of the other exercises in this document, I'd suggest you follow along if you can. Using these commands on your own is the only way to really learn the techniques. Read the included man pages and feel free the options to get other output. The image files used in the following examples are available for download, and some have already been downloaded and used early in the guide.

There are a number of ways to tackle the problems. In some cases we'll use affuse or ewfmount to fuse mounted images from EWF files or split files. We'll do it for practice, feel free to run the tools directly on the image files themselves (there will be demonstrations of both). Practice and experiment.

We'll also use some of the older image files that were used in previous versions of the guide. While the images are old and the file systems somewhat deprecated, we use them here because they provide a perfect vehicle for demonstrating tool usage. You'll understand this bit more as we progress. We can compare output on some of the newer images and understand the limitations.

For the following set of exercises, we'll use the able2 image, one of the older but more educational images we've used. Create a directory for the able2 image and then cd into the directory. As usual, download with wget and check the hash, making sure it matches what we have:

```
barry@forensic1:-$ mkdir able2
barry@forensic1:-$ cd able2
barry@forensic1:~/able2$ wget http://www.linuxleo.com/Files/able2.tar.gz
...
barry@forensic1:~/able2$ shasum able2.tar.gz
a093ec9ead6054665b89aa82140803790be97a6e able2.tar.gz
```

Untar the image and let's get started. Get your hands on the keyboard and feel along.

211