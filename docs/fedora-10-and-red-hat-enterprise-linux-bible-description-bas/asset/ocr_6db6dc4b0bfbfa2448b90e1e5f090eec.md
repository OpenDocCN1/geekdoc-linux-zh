# 550 Part III: Administering Fedora and RHEL

Device seems to be: Generic mmc2 DVD-R/DVD-RW.

Drive capabilities, per MMC-3 page 2A:

+   - Does read CD-R media
- Does write CD-R media
- Does read CD-RW media
- Does write CD-RW media
- Does read DVD-ROM media
- Does read DVD-R media
- Does write DVD-R media
- Does not read DVD-RAM media
- Does not write DVD-RAM media
- Does support test writing

In the preceding output, you can see that this drive supports reading and writing of both CDs and DVDs. Use the Spacebar to page through the output (and q to quit). Near the end of the output, you should see and write speeds supported by the drive. Note that those are maximum possible speeds, so the actual maximum speed will depend on the CD or DVD you are using.

The procedure for writing to DVDs is almost identical to backing up data onto a CD disk, with the following exceptions:

+   - Each backup disk can hold more data (4.7GB for single-layer and 8.5GB for dual-layer DVD, as compared to 700MB for CDs).
- Both the DVD writer and media are more expensive than the CD counterparts, although the cost of DVD writers has come down drastically in the past years.

> NOTE: When manufacturers say 4.7GB, they are talking about 1000MB per GB, 1024MB. Therefore, you can only store up to 4.3GB of data on a DVD (or, more precisely, 4,294,296,296 bytes).

There are a few other issues you should be aware of that relate to using DVD media to record from Linux:

+   - While new writable drives today support both DVD-R and DVD+R formats, some older drives may not support DVD+R.
- DVD+RW media that have not been formatted before you can write to it. However, you can use cdrecord on an unformatted DVD+RW because it will automatically detect and format an unformatted disk. For a format, you can use the -format option to cdrecord. There is also a dvd+rw-format with your DVD device that you can use to format a DVD drive (just run dvd+rw-format with your DVD device as option).