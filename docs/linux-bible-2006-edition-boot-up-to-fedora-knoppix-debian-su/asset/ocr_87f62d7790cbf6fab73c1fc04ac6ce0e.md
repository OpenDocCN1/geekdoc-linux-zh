# 248 Part III ♦ Choosing and Installing a Linux Distribution

in the middle for some reason. A wget command to download a KNOPPIX CD image (starting from the directory you want to download) might look like this:

```
$ wget -c ftp.tux.org/pub/linux/knopPIX_V4.0.2CD-2005-09-23-EN.iso
```

If the download slows down before it is finished, the -c option allows wget to begin where the download left off, so if you are 640MB into when it stopped, it adds back the last 10MB.

You might also want to look into a facility called BitTorrent (http://bittrent.com). BitTorrent lets you download a file to your computer by grabbing bits of that from multiple computers on the network that are downloading the file at the same time. For the privilege, you use your upload capacity to share the file with others as you are downloading.

During times of high demand with a Linux distribution, BitTorrent can be the best way to go. Recent articles have portrayed BitTorrent as a tool for illegal activities, such as downloading copyrighted materials (movies, music, and so on). Because Linux distributions contain only software covered under various open source licenses, there is no legal problem with using BitTorrent to distribute distributions. Check out www.linuxtracker.org for a list of Linux distributions that can be downloaded with BitTorrent.

If you are on a dial-up modem, you should strongly consider purchasing Linux CDs (or getting them from a friend) if we don't have what you want on the CD or DVD with this book. You might be able to download the 700MB CD in a couple hours on a DSL or cable connection. On a dial-up line, you might be waiting the whole day or more per CD. For a large, multi-CD distribution, available disk space can also become a problem (although, with today's large hard disks, it's not as much of a problem as it used to be).

# Burning the Distribution to CD

With the CDs copied to your computer, you can proceed to verify their contents and burn them to CD. All you need is a CD burner on your computer.

With Linux, you can use the md5sum command to verify the.

If you are using Windows to validate the contents of the Linux CD, you can get the MD5Summer utility (www.md5summer.org) to verify each CD image.

Assuming you downloaded the MD5 file associated with each CD image, in the same directory as your CD images, run the md5sum command to verify the image. For example, to verify the KNOPPIX CD shown previously in the wget example, you would type:

```
$ md5sum KNOPPIX_V4.0.2CD-2005-09-23-EN.iso
1188f6d48c9f1af837297ef4c5 KNOPPIX_V4.0.2CD-2005-09-23-EN.iso
```