# # 19 – Archiving And Backup

One of the primary tasks of a computer system’s administrator is keeping the system’s data secure. One way this is done is by performing timely backups of the system’s files. Even if you’re not system administrators, it is often useful to make copies of things and to move large collections of files from place to place and from device to device.

In this chapter, we will look at several common programs that are used to manage collections of files. There are the file compression programs:

+   - `gzip` – Compress or expand files
+   - `bzip2` – A block sorting file compressor

The archiving programs:

+   - `tar` – Tape archiving utility
+   - `zip` – Package and compress files

And the file synchronization program:

+   - `rsync` – Remote file and directory synchronization

# ## Compressing Files

Throughout the history of computing, there has been a struggle to get the most data into the smallest available space, whether that space be a memory, storage devices or network bandwidth. Many of the data services that we take for granted today, such as portable music players, high definition television, or broadband Internet, owe their existence to effective *data compression* techniques.

Data compression is the process of removing *redundancy* from data. Let’s consider an imaginary example. Say we had an entirely black picture file with the dimensions of one hundred pixels by one hundred pixels. In terms of data storage (assuming twenty-four bits, or three bytes per pixel), the image will occupy thirty thousand bytes of storage:

```
100 * 100 * 3 = 30,000
```

An image that is all one color contains entirely redundant data. If we were clever, we could encode the data in such a way that we simply describe the fact that we have a block