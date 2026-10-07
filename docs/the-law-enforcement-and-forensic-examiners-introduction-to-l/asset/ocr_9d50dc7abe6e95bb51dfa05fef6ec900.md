# v.4.33
A Comprehensive Beginner's Guide to Linux as a Digital Forensic Platform

```
-rw-r---- 1 root 128M May 1 18:19 NTFS_Pract_2017.E02
-rw-r---- 1 root 128M May 1 18:19 NTFS_Pract_2017.E03
-rw-r---- 1 root 117M May 1 18:19 NTFS_Pract_2017.E04
-rw-r---- 1 root 500M May 1 22:00 NTFS_Pract_2017.raw
-rw-r---- 1 root 158M May 1 22:00 NTFS_Pract_2017.raw.info
```

```
root@forensic1:~/NTFS_Pract_2017# md5sum NTFS_Pract_2017.raw
eb4393cfcc4fca856e0bdff772baa7d NTFS_Pract_2017.raw
```

At this point, we've covered dd, dc33dd, ewfacquire and common methods for checking the integrity and exporting the collected images.

All of the tools we've covered so far are great for ideal situations, where our media behaves as we expect. In addition, they all have options or built in mechanisms that would allow our acquisition to read past (or accurately 'around') any non-fatal disk errors while syncing output to the resulting image might be usable. While many practitioners suggest these options as a default for reading dd commands, I tend to argue against it. Some of the reasons for this will become more apparent in the following section.

# Media Errors - ddrescue

Now that we have a basic understanding of media acquisition and the collection of evidence images, what do we do if we run into an error? Suppose you use dd and the command exits halfway through the process with a read error?

We can construct dd to attempt to read past the errors using the conv=noerror option. In basic terms, this is using the dd command to ignore the errors that it finds, and attempt to read past them. When we specify the noerror option it is a good idea to use the sync option with it. We will "pad" the dd output where errors are found and ensure that the output is "synchronized" with the original disk. Assuming that your drive is /dev/sdc, the command will look like something:

```
root@forensic1:~# dd if=/dev/sdc of=image.raw conv=noerror,sync
```

> I would like to consider forensic examiners using the conv=noerror,sync option, however. While dd is capable of reading past errors in many cases, it is not designed to actually recover any data from those areas. There are a number of tools out there are designed specifically for this purpose. If you need to use conv=noerror,sync, then you are using the wrong tool. That is not to say it will work as advertised (with some caveats), only that there are better options, or at least important considerations.

Which brings us to ddrescue.