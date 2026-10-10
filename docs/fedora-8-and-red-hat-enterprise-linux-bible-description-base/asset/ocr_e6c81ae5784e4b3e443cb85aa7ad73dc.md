In the preceding output, you can see that this drive supports reading and writing of both CDs and DVDs. Use the Spacebar to page through the output (and q to quit). Near the end of the output, you should see read and write speeds supported by the drive. Note that those are maximum *possible* speeds, so the actual maximum write speeds will depend on the CD or DVD media you are using.

The procedure for writing to DVDs is almost identical to backing up data onto a CD disk, with the following exceptions:

+   • Each backup disk can hold a lot more data (4.7GB for single-layer and 8.5GB for dual-layer DVD, as compared to 700MB for CDs).
+   • Both the DVD writer and medium are more expensive than the CD counterparts, although the cost of DVD writers has come down drastically in the past few years.

> **NOTE:** When manufacturers say 4.7GB, they are talking about 1000MB per GB, not 1024MB. Therefore, you can really only store up to about 4.3GB of data on a DVD (or, more precisely, 4,294,967,296 bytes).

There are also a few other issues you should be aware of that relate to using DVD media to record from Linux:

+   • While most new writable DVD drives today support both DVD-R and DVD+R formats, some older drives may not support DVD+R.
+   • DVD+RW media that have not been formatted must be formatted before you can write to it. However, you can use *cdrrecord* on an unformatted DVD+RW because it will automatically detect and format an unformatted disk. To force a format, you can use the *-format* option to *cdrrecord*. There is also a *dvd+rw-format* that you can use to format a DVD drive (just run *dvd+rw-format* with your DVD device as the option).
+   • You don’t need to reformat DVD+RW media more than once. Multiple reformats can make the DVD+RW media unusable.

Follow the procedure in the “Writable CD drives” section to create a file system image file (using *mkisofs*) and determine the location of your DVD-R driver. Then use the *cdrrecord* command to actually burn the DVD. Here is an example of a *cdrrecord* command line that burns a file system image called *bigimage.iso*:

```
```
# cdrrecord -v speed=2 dev=/dev/cdrom -data bigimage.iso
```
```

# ### Writing CD or DVDs with *growisofs*

Instead of doing separate *mkisofs* and *cdrrecord* commands, as just shown, you can use the *growisofs* command to combine the function of those two commands. The *growisofs* command is particularly useful for mastering of large ISO images (such as those for double-